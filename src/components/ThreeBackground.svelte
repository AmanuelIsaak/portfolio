<script lang="ts">
    import { onMount } from "svelte";

    // A lightweight, pointer-reactive particle field rendered with Three.js.
    // Designed to be a *background*: it never captures pointer events, caps the
    // pixel ratio, thins out on small screens, pauses when off-screen or when the
    // tab is hidden, and honours prefers-reduced-motion. Three is imported
    // dynamically so it stays out of the SSR bundle and off the critical path.

    let canvas: HTMLCanvasElement;
    let container: HTMLDivElement;

    onMount(() => {
        let disposed = false;
        let raf = 0;
        let cleanupFns: Array<() => void> = [];

        // Bail gracefully if WebGL is unavailable — the CSS gradient fallback stays.
        const probe = document.createElement("canvas");
        const hasWebGL = !!(
            probe.getContext("webgl2") || probe.getContext("webgl")
        );
        if (!hasWebGL) return;

        const reduceMotion = window.matchMedia(
            "(prefers-reduced-motion: reduce)",
        ).matches;

        const init = async () => {
            const THREE = await import("three");
            if (disposed) return;

            const {
                Scene,
                PerspectiveCamera,
                WebGLRenderer,
                BufferGeometry,
                BufferAttribute,
                ShaderMaterial,
                Points,
                Color,
                AdditiveBlending,
                NormalBlending,
                Vector2,
            } = THREE;

            const scene = new Scene();

            const camera = new PerspectiveCamera(
                55,
                container.clientWidth / container.clientHeight,
                0.1,
                100,
            );
            camera.position.set(0, 0, 6.2);

            const renderer = new WebGLRenderer({
                canvas,
                alpha: true,
                antialias: false,
                powerPreference: "high-performance",
            });
            renderer.setClearColor(0x000000, 0);

            const pixelRatioCap = window.innerWidth < 768 ? 1.5 : 2;
            const dpr = Math.min(window.devicePixelRatio || 1, pixelRatioCap);
            renderer.setPixelRatio(dpr);
            renderer.setSize(container.clientWidth, container.clientHeight, false);

            // ---- particle field ---------------------------------------------
            // Particle budget scales with viewport so phones stay smooth.
            const area = window.innerWidth * window.innerHeight;
            const count = Math.round(
                Math.max(1800, Math.min(6000, area / 320)),
            );

            const positions = new Float32Array(count * 3);
            const colors = new Float32Array(count * 3);
            const scales = new Float32Array(count);
            const seeds = new Float32Array(count);

            // Brand gradient: rose → orange → amber.
            const cInner = new Color("#fb7185");
            const cMid = new Color("#f97316");
            const cOuter = new Color("#fbbf24");
            const tmp = new Color();

            const R = 4.3;
            for (let i = 0; i < count; i++) {
                // Random direction on a sphere, biased toward a thick outer shell.
                const u = Math.random();
                const v = Math.random();
                const theta = 2 * Math.PI * u;
                const phi = Math.acos(2 * v - 1);
                const r = R * (0.42 + 0.58 * Math.cbrt(Math.random()));

                let x = r * Math.sin(phi) * Math.cos(theta);
                let y = r * Math.sin(phi) * Math.sin(theta);
                let z = r * Math.cos(phi);
                x *= 1.3; // widen
                z *= 0.75; // flatten depth a touch

                positions[i * 3] = x;
                positions[i * 3 + 1] = y;
                positions[i * 3 + 2] = z;

                // Colour by normalised radius, then add a little brightness jitter.
                const t = Math.min(1, r / R);
                if (t < 0.5) tmp.copy(cInner).lerp(cMid, t * 2);
                else tmp.copy(cMid).lerp(cOuter, (t - 0.5) * 2);
                const b = 0.7 + Math.random() * 0.5;
                colors[i * 3] = tmp.r * b;
                colors[i * 3 + 1] = tmp.g * b;
                colors[i * 3 + 2] = tmp.b * b;

                // Mostly small dust, a few bright "stars".
                scales[i] =
                    Math.random() < 0.05
                        ? 2.4 + Math.random() * 2.6
                        : 0.5 + Math.random() * 1.1;
                seeds[i] = Math.random();
            }

            const geometry = new BufferGeometry();
            geometry.setAttribute("position", new BufferAttribute(positions, 3));
            geometry.setAttribute("aColor", new BufferAttribute(colors, 3));
            geometry.setAttribute("aScale", new BufferAttribute(scales, 1));
            geometry.setAttribute("aSeed", new BufferAttribute(seeds, 1));

            const isDark = () =>
                document.documentElement.classList.contains("dark");

            const material = new ShaderMaterial({
                transparent: true,
                depthWrite: false,
                blending: isDark() ? AdditiveBlending : NormalBlending,
                uniforms: {
                    uTime: { value: 0 },
                    uSize: { value: 16 },
                    uPixelRatio: { value: dpr },
                    uAlpha: { value: isDark() ? 0.9 : 0.55 },
                },
                vertexShader: /* glsl */ `
                    uniform float uTime;
                    uniform float uSize;
                    uniform float uPixelRatio;
                    attribute float aScale;
                    attribute float aSeed;
                    attribute vec3 aColor;
                    varying vec3 vColor;
                    varying float vFade;

                    void main() {
                        vColor = aColor;
                        vec3 p = position;

                        // Independent organic drift per particle.
                        float t = uTime * 0.22;
                        float s = aSeed * 6.2831853;
                        p.x += sin(t + s) * 0.18;
                        p.y += cos(t * 0.9 + s) * 0.18;
                        p.z += sin(t * 1.1 + s * 0.5) * 0.18;

                        vec4 mvPosition = modelViewMatrix * vec4(p, 1.0);
                        gl_Position = projectionMatrix * mvPosition;

                        // Size attenuation — keep visual size stable across DPR.
                        gl_PointSize = uSize * aScale * uPixelRatio;
                        gl_PointSize *= (1.0 / -mvPosition.z);

                        // Fade particles that drift behind the camera plane.
                        vFade = smoothstep(-1.0, 3.0, mvPosition.z + 7.0);
                    }
                `,
                fragmentShader: /* glsl */ `
                    uniform float uAlpha;
                    varying vec3 vColor;
                    varying float vFade;

                    void main() {
                        float d = length(gl_PointCoord - vec2(0.5));
                        if (d > 0.5) discard;
                        float alpha = smoothstep(0.5, 0.0, d);
                        alpha = pow(alpha, 1.5);
                        gl_FragColor = vec4(vColor, alpha * uAlpha * vFade);
                    }
                `,
            });

            const points = new Points(geometry, material);
            scene.add(points);

            // ---- interaction & lifecycle ------------------------------------
            const pointer = new Vector2(0, 0);
            const pointerTarget = new Vector2(0, 0);

            const onPointerMove = (e: PointerEvent) => {
                pointerTarget.x = (e.clientX / window.innerWidth - 0.5) * 2;
                pointerTarget.y = (e.clientY / window.innerHeight - 0.5) * 2;
            };
            if (!reduceMotion) {
                window.addEventListener("pointermove", onPointerMove, {
                    passive: true,
                });
                cleanupFns.push(() =>
                    window.removeEventListener("pointermove", onPointerMove),
                );
            }

            // Keep blending/opacity in sync with the active theme.
            const themeObserver = new MutationObserver(() => {
                material.blending = isDark()
                    ? AdditiveBlending
                    : NormalBlending;
                material.uniforms.uAlpha.value = isDark() ? 0.9 : 0.55;
                material.needsUpdate = true;
            });
            themeObserver.observe(document.documentElement, {
                attributes: true,
                attributeFilter: ["class"],
            });
            cleanupFns.push(() => themeObserver.disconnect());

            const resize = () => {
                const w = container.clientWidth;
                const h = container.clientHeight;
                camera.aspect = w / h;
                camera.updateProjectionMatrix();
                renderer.setSize(w, h, false);
            };
            const resizeObserver = new ResizeObserver(resize);
            resizeObserver.observe(container);
            cleanupFns.push(() => resizeObserver.disconnect());

            // Only render while the canvas is actually on screen.
            let inView = true;
            const io = new IntersectionObserver(
                ([entry]) => {
                    inView = entry.isIntersecting;
                    if (inView && !reduceMotion && !raf) loop();
                },
                { threshold: 0 },
            );
            io.observe(container);
            cleanupFns.push(() => io.disconnect());

            const onVisibility = () => {
                if (document.hidden) {
                    cancelAnimationFrame(raf);
                    raf = 0;
                } else if (inView && !reduceMotion && !raf) {
                    loop();
                }
            };
            document.addEventListener("visibilitychange", onVisibility);
            cleanupFns.push(() =>
                document.removeEventListener("visibilitychange", onVisibility),
            );

            const clock = new THREE.Clock();

            const render = () => {
                pointer.x += (pointerTarget.x - pointer.x) * 0.04;
                pointer.y += (pointerTarget.y - pointer.y) * 0.04;
                // Gentle pointer parallax + slow autorotation.
                points.rotation.y += 0.0006;
                points.rotation.x = pointer.y * 0.25;
                points.rotation.z = pointer.x * 0.12;
                material.uniforms.uTime.value = clock.getElapsedTime();
                renderer.render(scene, camera);
            };

            const loop = () => {
                if (disposed) return;
                render();
                raf = requestAnimationFrame(loop);
            };

            if (reduceMotion) {
                render(); // single static frame, no animation
            } else {
                loop();
            }

            cleanupFns.push(() => {
                cancelAnimationFrame(raf);
                geometry.dispose();
                material.dispose();
                renderer.dispose();
            });
        };

        // Defer the heavy Three.js download/setup until the browser is idle so
        // the rest of the page hydrates first — keeps low-end phones snappy.
        const ric = (window as Window & {
            requestIdleCallback?: (cb: () => void, opts?: { timeout: number }) => number;
            cancelIdleCallback?: (id: number) => void;
        }).requestIdleCallback;
        if (typeof ric === "function") {
            const id = ric(() => init(), { timeout: 1800 });
            cleanupFns.push(() =>
                (window as Window & {
                    cancelIdleCallback?: (id: number) => void;
                }).cancelIdleCallback?.(id),
            );
        } else {
            const t = setTimeout(() => init(), 200);
            cleanupFns.push(() => clearTimeout(t));
        }

        return () => {
            disposed = true;
            cleanupFns.forEach((fn) => fn());
            cleanupFns = [];
        };
    });
</script>

<div
    bind:this={container}
    class="absolute inset-0 -z-10 overflow-hidden pointer-events-none"
    aria-hidden="true"
>
    <canvas bind:this={canvas} class="h-full w-full"></canvas>
</div>
