# Unidad 8

## Apply: Aplicación 


### **Actividad 05: Diseño e implementación de una pieza visual transferida**


**1. Herramienta elegida.**

R/ Se seleccionó **Three.js con WebGPU y TSL** (Three.js Shading Language). La elección se fundamentó en el trabajo de Bruno Simon, quien ha sido un referente artístico y técnico para el autor. Esta actividad permitió abordar el manejo de partículas con TSL, un interés técnico y artistico que para mi siempre ha sido muy llamativo.

**2. Sistema transferido.**

R/ Se implementó la transferencia de un sistema de **Flow Field** combinado con **Random Walkers** que actúan como atractores de el millon de particulas procesadas.

**3. Contexto profesional concreto.**

R/ La pieza se proyectó como un componente visual para instalaciones digitales inmersivas. este tipo de arte trabajado con web gpu me encanta y siempre he tenido como la gana oculta de no dedicarme solo a lo tecnico si no convivir con lo artistico y estoy seguro tomo esa desicion sere artista tecnico de three pq aparte de todo me encanta que casi cualquier persona lopueda ver y experimentar obras en la mayria de computadores.

**4. Concepto visual.**

R/ Aunque la intención inicial era crear rayos de atracción, la iteración técnica y el ajuste de parámetros transformaron la pieza en una representación de un **tornado o remolino de energía**, donde las fuerzas absorven particulas de manera orgánica, ademas como comportamiento emergente terminaron apareciendo eventualmente patrones de rastro particulares o pequenos cucloides con actitudes muy particulares y llamativas, recuerda mucho a spectro patronum de harry poter.

**5. Referencias.**

R/ La lógica del buffer de partículas en TSL se inspiró en el código de ejemplo desarrollado por Bruno Simon: [WebGPU TSL Compute Attractors Particles]
(https://threejs.org/examples/?q=particles#webgpu_tsl_compute_attractors_particles).



https://co.pinterest.com/pin/504614333265918301/

https://co.pinterest.com/pin/794955771768920789/



<img width="540" height="540" alt="image" src="https://github.com/user-attachments/assets/93841826-f1a0-45cf-a009-276a5b1f614d" />



<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/0a807ad2-21e0-41b5-85d9-e04fae92f4d9" />



**6. Bocetos.**


R/


<img width="414" height="349" alt="161acf12-b22e-4bcf-b44d-0586ac10f6c5" src="https://github.com/user-attachments/assets/6b2cdd2a-731a-42b9-b767-e3adec9838d8" />


<img width="684" height="713" alt="fdcd8d34-01a7-405e-8bce-90cf9db97f4f" src="https://github.com/user-attachments/assets/c1c827de-dc86-4447-8ec7-29f32b96af45" />


**7. Explicación de la transferencia.**


R/ El proceso consistió en migrar la lógica de cálculo de CPU (típica en p5.js) hacia la **GPU** mediante TSL. En lugar de procesar partículas individualmente con ciclos, se crearon buffers (`instancedArray`) para gestionar un millón de partículas directamente en la gpu. Se definió una función de cómputo que aplica a cada partícula la dirección del *Flow Field* (calculada con ruido 3D) y la fuerza de atracción de los *walkers*, ha pesar de no terminar de interiorisar el manejo de tsl si ha sido una gran motivacion para profundizar y aprovechar la gpu pa evitar cuellos de botella por cpu.

**8. Mapa de decisiones.**


- **Sistema**: Combinación de Flow Field base y Walkers como atractores.
- **Herramienta**: Three.js WebGPU, seleccionada por su rendimiento para manejar grandes volúmenes de datos sin comprometer la fluidez del navegador.
- **Visualidad**: Estética de partículas brillantes con estela en tonos azul y amarillo sobre fondo negro para resaltar el concepto de energía.
- **Interacción**: Controles en tiempo real mediante una GUI (lil-gui) para manipular velocidades, radios y fuerzas durante la ejecución.

**9. Mapa de presentación.**


R/ La visualización se realiza en pantalla completa en el navegador. La presentación inicia permitiendo que el sistema evolucione de forma autónoma hasta formar el tornado mientras la cámara ejecuta un `autoRotate`. Eventualmente, se utiliza la GUI para demostrar la reactividad del sistema ante cambios de parámetros, manteniendo la limpieza visual de la obra.

**10. Evidencia del uso de IA.**


R/ se utilizo principalmente para comprender el sitema del referente inicial, capturar el manejo de buffer y particulas del referente, y para traducir las intenciones tecnicas desde codigo tradicional de cpu para tranformarlo y acoplarlo a la arquitectura de tsl.


<img width="684" height="713" alt="fdcd8d34-01a7-405e-8bce-90cf9db97f4f" src="https://github.com/user-attachments/assets/a759c28c-a81c-4648-b314-16d4b0991b88" />


<img width="414" height="349" alt="161acf12-b22e-4bcf-b44d-0586ac10f6c5" src="https://github.com/user-attachments/assets/625f6387-0998-4336-ba5f-74748aa4587e" />


**7. Explicación de la transferencia.**


R/ Pasar esto de p5.js a TSL me costo demasiado y no lo termine de apropiar pq ya no se calcula cada partícula en el CPU con un ciclo `for` normal. Acá se crea buffers (`instancedArray`) para un millón de partículas directo en la memoria de la GPU. Con TSL definí una función de cómputo (`compute`) q le aplica a cada partícula la dirección del Flow Field (calculada con ruido 3D) y tmbn le suma una fuerza para q persiga el rastro q dejan los dos walkers.

**8. Mapa de decisiones.**

R/

- **Sistema**: Flow Field base + Walkers q actúan como atractores.
- **Herramienta**: Three.js WebGPU, pq es lo único q aguanta manejar 1 millón de partículas sin q se trabe el navegador.
- **Visualidad**: Partículas brillantes con estela (azul y amarillo) sobre fondo negro para resaltar ese look de energía pura del tornado.
- **Interacción**: Controles en tiempo real con una GUI (lil-gui) para poder jugar en vivo con velocidades, radios y fuerzas.

**9. Mapa de presentación.**


 R/ Se muestra la pieza corriendo a pantalla completa. La presentación arranca dejando q el sistema fluya solo para q se vaya armando el tornado, mientras la cámara hace el giro en automático. Ya después, para mostrar q el sistema es reactivo, abro la GUI un momento, le muevo los parámetros de fuerza o velocidad en vivo y usando las funciones de los botones qwer para mostrar diferentes comportamientos que la obra puede tomar y la vuelvo a esconder para dejar la obra andando sola.

 
**10. Evidencia del uso de IA.**


R/ me apoye bastante con antigravity sobretodo para comprender el codigo del referente de bruno simons, extraer la logica de tsl y particulas y lograr traducir de codigo normal de js  y la logica qu conosia de flowfields y random walkers y reestructurarlo para aplicarlo a la logica de tsl y manejo de objetos a travez del buffer.

**video**
https://drive.google.com/file/d/1SVv9lumhmWPuIjC50l9CZ7YfvLaP2hkh/view?usp=sharing

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
    <title>Flow Field Particles · WebGPU</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #000;
            overflow: hidden;
        }

        canvas {
            display: block;
        }

        #info {
            position: absolute;
            top: 16px;
            left: 50%;
            transform: translateX(-50%);
            color: rgba(255, 255, 255, 0.22);
            font: 12px/1.6 monospace;
            text-align: center;
            pointer-events: none;
            white-space: nowrap;
        }
    </style>

    <script type="importmap">
    {
        "imports": {
            "three":         "https://cdn.jsdelivr.net/npm/three@0.176.0/build/three.webgpu.js",
            "three/webgpu":  "https://cdn.jsdelivr.net/npm/three@0.176.0/build/three.webgpu.js",
            "three/tsl":     "https://cdn.jsdelivr.net/npm/three@0.176.0/build/three.tsl.js",
            "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.176.0/examples/jsm/"
        }
    }
    </script>
</head>

<body>
    <div id="info"></div>

    <script type="module">
        import * as THREE from 'three/webgpu';
        import {
            float, If, Loop, color,
            instanceIndex, mix,
            instancedArray, uniformArray, Fn, uint, uniform, hash,
            vec3, vec4,
            floor, fract
        } from 'three/tsl';
        import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
        import { GUI } from 'three/addons/libs/lil-gui.module.min.js';

        // ── constants ─────────────────────────────────────────────────────
        const MAX_COUNT = Math.pow(2, 20); // 1M — buffers allocated once
        const TRAIL_LENGTH = 48;              // historical positions per walker
        const TRAIL_DT = 0.05;           // seconds between trail samples

        // ── module-level handles ──────────────────────────────────────────
        let camera, scene, renderer, controls, updateCompute, scatterCompute, scatterSeedUniform;
        let fieldTimeUniform, boundRadiusUniform;
        let isScattering = false;

        // Trail uniforms (set inside init, used in updateWalker)
        let trailPositions1, trailActiveCount1;
        let trailPositions2, trailActiveCount2;

        // Sprites
        let halo1, core1, halo2, core2;

        let particleMesh;
        const clock = new THREE.Clock();
        let totalTime = 0;
        let timeSpeedJS = 0.05;

        // ── Walker 1 ──────────────────────────────────────────────────────
        let walkerSpeed1 = 5.85;
        const wPos1 = new THREE.Vector3(1.0, 0.5, 0.2);
        const wVel1 = new THREE.Vector3(1.0, 0.6, 0.4).normalize().multiplyScalar(5.85);
        const wTarget1 = new THREE.Vector3(1.0, 0.6, 0.4).normalize();
        let wSteerTimer1 = 0, wSteerInt1 = 1.2;
        const trail1Data = Array.from({ length: TRAIL_LENGTH }, () => new THREE.Vector3(0, -9999, 0));
        let trailCount1JS = 0, trailTimer1JS = 0;

        // ── Walker 2 ──────────────────────────────────────────────────────
        let walkerSpeed2 = 5.25;
        const wPos2 = new THREE.Vector3(-1.0, -0.5, 0.8);
        const wVel2 = new THREE.Vector3(-0.6, 0.9, -0.4).normalize().multiplyScalar(5.25);
        const wTarget2 = new THREE.Vector3(-0.6, 0.9, -0.4).normalize();
        let wSteerTimer2 = 0, wSteerInt2 = 0.9;
        const trail2Data = Array.from({ length: TRAIL_LENGTH }, () => new THREE.Vector3(0, -9999, 0));
        let trailCount2JS = 0, trailTimer2JS = 0;

        // ─────────────────────────────────────────────────────────────────
        init().catch(err => {
            document.getElementById('info').style.cssText +=
                ';color:#f55;font-size:14px;top:40%;position:absolute;white-space:pre-wrap;max-width:80%;left:10%';
            document.getElementById('info').textContent = '⚠ Error:\n' + err;
            console.error(err);
        });

        async function init() {

            camera = new THREE.PerspectiveCamera(35, window.innerWidth / window.innerHeight, 0.1, 200);
            camera.position.set(0, 6, 16);
            scene = new THREE.Scene();

            renderer = new THREE.WebGPURenderer({ antialias: true });
            renderer.setPixelRatio(window.devicePixelRatio);
            renderer.setSize(window.innerWidth, window.innerHeight);
            renderer.setAnimationLoop(animate);
            renderer.setClearColor('#000000');
            document.body.appendChild(renderer.domElement);
            await renderer.init();

            controls = new OrbitControls(camera, renderer.domElement);
            controls.enableDamping = true;
            controls.autoRotate = true;
            controls.autoRotateSpeed = 1.35;
            controls.minDistance = 2;
            controls.maxDistance = 60;

            window.addEventListener('resize', onWindowResize);

            // ── UNIFORMS ──────────────────────────────────────────────────
            const fieldScale = uniform(0.79);
            const fieldStrength = uniform(0);
            const maxSpeed = uniform(6.8);
            const damping = uniform(0.008);
            const particleScale = uniform(0.009);
            const colorSlow = uniform(color('#0000ff'));
            const colorFast = uniform(color('#ffea00'));

            boundRadiusUniform = uniform(5.0);
            fieldTimeUniform = uniform(0.0);

            // Shared walker force params
            const walkerRadius = uniform(2.0);
            const walkerStrength = uniform(7.5);

            // Trail uniforms — arrays written from JS every TRAIL_DT seconds
            trailPositions1 = uniformArray(trail1Data, 'vec3');
            trailActiveCount1 = uniform(0, 'uint');
            trailPositions2 = uniformArray(trail2Data, 'vec3');
            trailActiveCount2 = uniform(0, 'uint');

            // ── PARTICLE BUFFERS ──────────────────────────────────────────
            const positionBuffer = instancedArray(MAX_COUNT, 'vec3');
            const velocityBuffer = instancedArray(MAX_COUNT, 'vec3');

            // ── 3D VALUE NOISE ────────────────────────────────────────────
            const makeValueNoise3D = (seedOffset) => Fn(([p]) => {
                const pi = floor(p);
                const pf = fract(p);
                const uf = pf.mul(pf).mul(float(3).sub(pf.mul(2)));
                const hc = (dx, dy, dz) => {
                    const ix = float(1000).add(pi.x.add(dx)).toUint();
                    const iy = float(1000).add(pi.y.add(dy)).toUint().mul(uint(1619));
                    const iz = float(1000).add(pi.z.add(dz)).toUint().mul(uint(31337));
                    return hash(ix.add(iy).add(iz).add(uint(seedOffset)));
                };
                const n000 = hc(0, 0, 0); const n100 = hc(1, 0, 0);
                const n010 = hc(0, 1, 0); const n110 = hc(1, 1, 0);
                const n001 = hc(0, 0, 1); const n101 = hc(1, 0, 1);
                const n011 = hc(0, 1, 1); const n111 = hc(1, 1, 1);
                const nx00 = mix(n000, n100, uf.x); const nx10 = mix(n010, n110, uf.x);
                const nx01 = mix(n001, n101, uf.x); const nx11 = mix(n011, n111, uf.x);
                const nxy0 = mix(nx00, nx10, uf.y); const nxy1 = mix(nx01, nx11, uf.y);
                return mix(nxy0, nxy1, uf.z).mul(2).sub(1);
            });

            const N1 = makeValueNoise3D(0);
            const N2 = makeValueNoise3D(7919);
            const N3 = makeValueNoise3D(15731);

            // ── CURL NOISE ────────────────────────────────────────────────
            const curlNoise = Fn(([worldPos]) => {
                const t = fieldTimeUniform.mod(10000);
                const p = worldPos.mul(fieldScale).add(vec3(t.mul(0.15), t.mul(0.09), t.mul(0.12)));
                const eps = float(0.1), eps2 = float(0.2);
                const dA3_dy = N3(p.add(vec3(0, eps, 0))).sub(N3(p.sub(vec3(0, eps, 0)))).div(eps2);
                const dA2_dz = N2(p.add(vec3(0, 0, eps))).sub(N2(p.sub(vec3(0, 0, eps)))).div(eps2);
                const dA1_dz = N1(p.add(vec3(0, 0, eps))).sub(N1(p.sub(vec3(0, 0, eps)))).div(eps2);
                const dA3_dx = N3(p.add(vec3(eps, 0, 0))).sub(N3(p.sub(vec3(eps, 0, 0)))).div(eps2);
                const dA2_dx = N2(p.add(vec3(eps, 0, 0))).sub(N2(p.sub(vec3(eps, 0, 0)))).div(eps2);
                const dA1_dy = N1(p.add(vec3(0, eps, 0))).sub(N1(p.sub(vec3(0, eps, 0)))).div(eps2);
                return vec3(dA3_dy.sub(dA2_dz), dA1_dz.sub(dA3_dx), dA2_dx.sub(dA1_dy));
            });

            // ── INIT COMPUTE ──────────────────────────────────────────────
            const seed = uint(Math.floor(Math.random() * 0xffffff));

            const initFn = Fn(() => {
                const pos = positionBuffer.element(instanceIndex);
                const vel = velocityBuffer.element(instanceIndex);

                // Random direction × random radius → fills sphere
                const rawX = hash(instanceIndex.add(seed)).sub(0.5);
                const rawY = hash(instanceIndex.add(seed).add(uint(0x4444))).sub(0.5);
                const rawZ = hash(instanceIndex.add(seed).add(uint(0x8888))).sub(0.5);
                const rawPos = vec3(rawX, rawY, rawZ);
                const rawLen = rawPos.length().add(0.0001);
                const r = hash(instanceIndex.add(seed).add(uint(0xcccc))).mul(boundRadiusUniform);
                pos.assign(rawPos.div(rawLen).mul(r));
                vel.assign(vec3(0));
            });

            const initCompute = initFn().compute(MAX_COUNT);
            renderer.compute(initCompute);

            const reset = () => {
                renderer.compute(initCompute);
                trailCount1JS = 0; trailActiveCount1.value = 0;
                trailCount2JS = 0; trailActiveCount2.value = 0;
                trail1Data.forEach(v => v.set(0, -9999, 0));
                trail2Data.forEach(v => v.set(0, -9999, 0));
            };

            // ── UPDATE COMPUTE ────────────────────────────────────────────
            const massVar = hash(instanceIndex.add(uint(0xabcdef))).remap(0.25, 1.0);
            const N_f = float(TRAIL_LENGTH);

            // Trail attraction helper — shared logic for both walkers
            const applyTrail = (trailPos, trailCount, pos, vel, dt) => {
                Loop(trailCount, ({ i }) => {
                    const tp = trailPos.element(i);
                    const toTrail = tp.sub(pos);
                    const tDist = toTrail.length();
                    const tFalloff = float(1).sub(tDist.div(walkerRadius)).clamp(0, 1);
                    const ageWt = N_f.sub(i.toFloat()).div(N_f);
                    vel.addAssign(
                        toTrail.div(tDist.add(0.001))
                            .mul(tFalloff.mul(tFalloff))
                            .mul(walkerStrength)
                            .mul(ageWt)
                            .mul(dt)
                    );
                });
            };

            const updateFn = Fn(() => {
                const dt = float(1.0 / 60.0);
                const pos = positionBuffer.element(instanceIndex);
                const vel = velocityBuffer.element(instanceIndex);

                // Weak base curl field
                vel.addAssign(curlNoise(pos).mul(fieldStrength).mul(dt));

                // Both walkers' trail attraction
                applyTrail(trailPositions1, trailActiveCount1, pos, vel, dt);
                applyTrail(trailPositions2, trailActiveCount2, pos, vel, dt);

                // Speed cap
                const spd = vel.length();
                If(spd.greaterThan(maxSpeed), () => {
                    vel.assign(vel.normalize().mul(maxSpeed));
                });

                vel.mulAssign(damping.oneMinus());
                pos.addAssign(vel.mul(dt));

                // ── Spherical bound with reflection ───────────────────────
                const pLen = pos.length().add(0.0001);
                const pRad = boundRadiusUniform;
                If(pLen.greaterThan(pRad), () => {
                    const pNorm = pos.div(pLen);          // outward unit normal
                    const vRadial = pNorm.x.mul(vel.x)
                        .add(pNorm.y.mul(vel.y))
                        .add(pNorm.z.mul(vel.z)); // dot(vel, normal)
                    If(vRadial.greaterThan(0), () => {
                        // reflect: v -= 2 * vn * n
                        vel.subAssign(pNorm.mul(vRadial.mul(2.0)));
                    });
                    pos.assign(pNorm.mul(pRad.mul(0.995)));
                });
            });

            updateCompute = updateFn().compute(MAX_COUNT);

            // ── SCATTER COMPUTE ───────────────────────────────────────────
            scatterSeedUniform = uniform(0, 'uint');
            const scatterFn = Fn(() => {
                const vel = velocityBuffer.element(instanceIndex);
                const s = scatterSeedUniform.add(instanceIndex);
                const rx = hash(s).sub(0.5);
                const ry = hash(s.add(uint(0x1111))).sub(0.5);
                const rz = hash(s.add(uint(0x2222))).sub(0.5);
                vel.assign(vec3(rx, ry, rz).normalize().mul(maxSpeed));
            });
            scatterCompute = scatterFn().compute(MAX_COUNT);

            // ── MATERIAL ──────────────────────────────────────────────────
            const material = new THREE.SpriteNodeMaterial({
                blending: THREE.AdditiveBlending,
                depthWrite: false
            });
            material.positionNode = positionBuffer.toAttribute();
            material.colorNode = Fn(() => {
                const vel = velocityBuffer.toAttribute();
                const t = vel.length().div(maxSpeed).clamp(0, 1);
                return vec4(mix(colorSlow, colorFast, t), 1);
            })();
            material.scaleNode = massVar.mul(particleScale);

            particleMesh = new THREE.InstancedMesh(new THREE.PlaneGeometry(1, 1), material, MAX_COUNT);
            particleMesh.count = Math.pow(2, 20); // default: 1M rendered
            scene.add(particleMesh);

            // ── WALKER VISUALS ────────────────────────────────────────────
            const glowTex = buildGlowTexture();
            halo1 = makeSprite(glowTex, 0.38); core1 = makeSprite(glowTex, 0.06);
            halo2 = makeSprite(glowTex, 0.38); core2 = makeSprite(glowTex, 0.06);
            scene.add(halo1); scene.add(core1);
            scene.add(halo2); scene.add(core2);

            // ── GUI ───────────────────────────────────────────────────────
            const gui = new GUI({ title: 'Flow Field' });
            gui.close();
            const p = {
                fieldScale: fieldScale.value,
                fieldStrength: fieldStrength.value,
                timeSpeed: timeSpeedJS,
                maxSpeed: maxSpeed.value,
                damping: damping.value,
                particleSize: particleScale.value,
                boundRadius: boundRadiusUniform.value,
                particleExp: 20,
                colorSlow: '#0000ff',
                colorFast: '#ffea00',
                autoRotate: 1.35,
                walkerStr: walkerStrength.value,
                walkerRad: walkerRadius.value,
                walker1Speed: walkerSpeed1,
                walker2Speed: walkerSpeed2,
                reset,
                copyParams: () => {
                    const snap = {
                        fieldScale: fieldScale.value,
                        fieldStrength: fieldStrength.value,
                        timeSpeed: timeSpeedJS,
                        maxSpeed: maxSpeed.value,
                        damping: damping.value,
                        particleSize: particleScale.value,
                        boundRadius: boundRadiusUniform.value,
                        particleExp: Math.round(Math.log2(particleMesh.count)),
                        colorSlow: '#' + colorSlow.value.getHexString(THREE.SRGBColorSpace),
                        colorFast: '#' + colorFast.value.getHexString(THREE.SRGBColorSpace),
                        camRotateSpeed: controls.autoRotateSpeed,
                        walkerStrength: walkerStrength.value,
                        walkerRadius: walkerRadius.value,
                        walker1Speed: walkerSpeed1,
                        walker2Speed: walkerSpeed2,
                    };
                    navigator.clipboard.writeText(JSON.stringify(snap, null, 2))
                        .then(() => console.log('params copied:', snap))
                        .catch(() => console.log('params:', JSON.stringify(snap, null, 2)));
                }
            };
            const ctrls = {};
            ctrls.fieldScale    = gui.add(p, 'fieldScale', 0.02, 1.5, 0.01).name('field scale').onChange(v => fieldScale.value = v);
            ctrls.fieldStrength = gui.add(p, 'fieldStrength', 0, 3, 0.02).name('field strength').onChange(v => fieldStrength.value = v);
            ctrls.timeSpeed     = gui.add(p, 'timeSpeed', 0, 0.1, 0.001).name('time speed').onChange(v => timeSpeedJS = v);
            ctrls.maxSpeed      = gui.add(p, 'maxSpeed', 1, 20, 0.1).name('max speed').onChange(v => maxSpeed.value = v);
            ctrls.damping       = gui.add(p, 'damping', 0, 0.1, 0.001).name('damping').onChange(v => damping.value = v);
            ctrls.particleSize  = gui.add(p, 'particleSize', 0, 0.05, 0.001).name('particle size').onChange(v => particleScale.value = v);
            ctrls.boundRadius   = gui.add(p, 'boundRadius', 1, 15, 0.1).name('bound radius').onChange(v => boundRadiusUniform.value = v);
            ctrls.particleExp   = gui.add(p, 'particleExp', 12, 20, 1).name('particles  2ⁿ').onChange(v => particleMesh.count = Math.pow(2, v));
            ctrls.colorSlow     = gui.addColor(p, 'colorSlow').name('color slow').onChange(v => colorSlow.value.set(v));
            ctrls.colorFast     = gui.addColor(p, 'colorFast').name('color fast').onChange(v => colorFast.value.set(v));
            ctrls.autoRotate    = gui.add(p, 'autoRotate', -3, 3, 0.05).name('cam rotate speed').onChange(v => controls.autoRotateSpeed = v);

            const wf = gui.addFolder('Walkers');
            ctrls.walkerStr    = wf.add(p, 'walkerStr', 0, 40, 0.5).name('field pull').onChange(v => walkerStrength.value = v);
            ctrls.walkerRad    = wf.add(p, 'walkerRad', 0.2, 8, 0.05).name('radius').onChange(v => walkerRadius.value = v);
            ctrls.walker1Speed = wf.add(p, 'walker1Speed', 0.1, 6, 0.05).name('speed 1').onChange(v => walkerSpeed1 = v);
            ctrls.walker2Speed = wf.add(p, 'walker2Speed', 0.1, 6, 0.05).name('speed 2').onChange(v => walkerSpeed2 = v);

            gui.add(p, 'reset');
            gui.add(p, 'copyParams').name('copy params  {}');

            // ── DEFAULT SNAPSHOT (Q key) ──────────────────────────────────
            const DEFAULTS = {
                fieldScale: 0.79, fieldStrength: 0, timeSpeed: 0.05,
                maxSpeed: 6.8, damping: 0.008, particleSize: 0.009,
                boundRadius: 5, particleExp: 20,
                colorSlow: '#0000ff', colorFast: '#ffea00',
                autoRotate: 1.35, walkerStr: 7.5, walkerRad: 2.0,
                walker1Speed: 5.85, walker2Speed: 5.25
            };

            const applyParams = (vals) => {
                fieldScale.value         = p.fieldScale      = vals.fieldScale;
                fieldStrength.value      = p.fieldStrength   = vals.fieldStrength;
                timeSpeedJS              = p.timeSpeed        = vals.timeSpeed;
                maxSpeed.value           = p.maxSpeed         = vals.maxSpeed;
                damping.value            = p.damping          = vals.damping;
                particleScale.value      = p.particleSize     = vals.particleSize;
                boundRadiusUniform.value = p.boundRadius      = vals.boundRadius;
                particleMesh.count       = Math.pow(2, vals.particleExp);
                p.particleExp            = vals.particleExp;
                colorSlow.value.set(vals.colorSlow); p.colorSlow = vals.colorSlow;
                colorFast.value.set(vals.colorFast); p.colorFast = vals.colorFast;
                controls.autoRotateSpeed = p.autoRotate       = vals.autoRotate;
                walkerStrength.value     = p.walkerStr        = vals.walkerStr;
                walkerRadius.value       = p.walkerRad        = vals.walkerRad;
                walkerSpeed1             = p.walker1Speed     = vals.walker1Speed;
                walkerSpeed2             = p.walker2Speed     = vals.walker2Speed;
                Object.values(ctrls).forEach(c => c.updateDisplay());
            };

            const rnd = (lo, hi) => lo + Math.random() * (hi - lo);
            const randomHex = () => '#' + Math.floor(Math.random() * 0xffffff).toString(16).padStart(6, '0');

            // ── KEYBOARD SHORTCUTS ────────────────────────────────────────
            window.addEventListener('keydown', ev => {
                if (ev.repeat) return;
                switch (ev.key.toLowerCase()) {
                    case 'r': reset(); break;
                    case 'e': isScattering = true; break;
                    case 'w': applyParams({
                        fieldScale:    rnd(0.05, 1.5),
                        fieldStrength: rnd(0, 2.0),
                        timeSpeed:     rnd(0, 0.1),
                        maxSpeed:      rnd(2, 20),
                        damping:       rnd(0, 0.05),
                        particleSize:  rnd(0.003, 0.03),
                        boundRadius:   rnd(2, 12),
                        particleExp:   20,
                        colorSlow:     randomHex(),
                        colorFast:     randomHex(),
                        autoRotate:    rnd(-3, 3),
                        walkerStr:     rnd(0, 40),
                        walkerRad:     rnd(0.5, 8),
                        walker1Speed:  rnd(0.5, 6),
                        walker2Speed:  rnd(0.5, 6),
                    }); break;
                    case 'q': applyParams(DEFAULTS); break;
                }
            });
            window.addEventListener('keyup', ev => {
                if (ev.key.toLowerCase() === 'e') isScattering = false;
            });
        }

        // ── GLOW TEXTURE ──────────────────────────────────────────────────
        function buildGlowTexture() {
            const S = 256, cvs = document.createElement('canvas');
            cvs.width = cvs.height = S;
            const ctx = cvs.getContext('2d'), cx = S / 2;
            const g = ctx.createRadialGradient(cx, cx, 0, cx, cx, cx);
            g.addColorStop(0, 'rgba(255,255,255,1.00)');
            g.addColorStop(0.04, 'rgba(255,255,255,1.00)');
            g.addColorStop(0.12, 'rgba(210,230,255,0.90)');
            g.addColorStop(0.28, 'rgba(160,200,255,0.45)');
            g.addColorStop(0.55, 'rgba(120,160,255,0.10)');
            g.addColorStop(1.0, 'rgba(0,0,0,0)');
            ctx.fillStyle = g;
            ctx.fillRect(0, 0, S, S);
            return new THREE.CanvasTexture(cvs);
        }

        function makeSprite(tex, scale) {
            const s = new THREE.Sprite(new THREE.SpriteMaterial({
                map: tex, blending: THREE.AdditiveBlending,
                depthWrite: false, transparent: true
            }));
            s.scale.setScalar(scale);
            return s;
        }

        // ── WALKER HELPERS ────────────────────────────────────────────────

        // Bounce a walker off the sphere: reflects velocity, clamps position
        function bounceOnSphere(pos, vel, radius) {
            const dist = pos.length();
            if (dist > radius) {
                const nx = pos.x / dist, ny = pos.y / dist, nz = pos.z / dist;
                const vDotN = vel.x * nx + vel.y * ny + vel.z * nz;
                if (vDotN > 0) {
                    vel.x -= 2 * vDotN * nx;
                    vel.y -= 2 * vDotN * ny;
                    vel.z -= 2 * vDotN * nz;
                    vel.multiplyScalar(0.85); // slight energy loss
                }
                pos.set(nx * radius * 0.99, ny * radius * 0.99, nz * radius * 0.99);
            }
        }

        // Advance one walker's position, steer randomly, sample trail
        function stepWalker(
            pos, vel, target,
            steerTimerRef, steerIntRef, speed,
            trailData, trailCountRef, trailTimerRef, trailPositions, trailActiveCount,
            halo, core, dt
        ) {
            // Steer
            steerTimerRef.v += dt;
            if (steerTimerRef.v >= steerIntRef.v) {
                target.set(Math.random() - 0.5, Math.random() - 0.5, Math.random() - 0.5).normalize();
                steerTimerRef.v = 0;
                steerIntRef.v = 0.5 + Math.random() * 2.0;
            }
            vel.lerp(target.clone().multiplyScalar(speed), Math.min(1, dt * 2.5));
            const s = vel.length();
            if (s > 0.001) vel.multiplyScalar(speed / s);

            pos.addScaledVector(vel, dt);
            bounceOnSphere(pos, vel, boundRadiusUniform.value);

            // Sample trail
            trailTimerRef.v += dt;
            if (trailTimerRef.v >= TRAIL_DT) {
                const used = Math.min(trailCountRef.v, TRAIL_LENGTH - 1);
                for (let i = used; i > 0; i--) trailData[i].copy(trailData[i - 1]);
                trailData[0].copy(pos);
                if (trailCountRef.v < TRAIL_LENGTH) trailCountRef.v++;
                trailActiveCount.value = trailCountRef.v;
                trailTimerRef.v = 0;
            }

            // Sprite pulse
            const pulse = 0.80 + 0.20 * Math.sin(totalTime * 9.0);
            halo.position.copy(pos); halo.scale.setScalar(0.38 * pulse);
            core.position.copy(pos); core.scale.setScalar(0.06 * (2.0 - pulse));
        }

        // ── RESIZE ────────────────────────────────────────────────────────
        function onWindowResize() {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        }

        // ── ANIMATE ───────────────────────────────────────────────────────

        // Mutable refs for stepWalker's timer args (plain objects as pass-by-ref)
        const st1 = { v: 0 }, si1 = { v: 1.2 }, tc1 = { v: 0 }, tt1 = { v: 0 };
        const st2 = { v: 0 }, si2 = { v: 0.9 }, tc2 = { v: 0 }, tt2 = { v: 0 };

        async function animate() {
            const dt = Math.min(clock.getDelta(), 0.05);
            totalTime += dt;

            controls.update();
            fieldTimeUniform.value += dt * timeSpeedJS;

            stepWalker(
                wPos1, wVel1, wTarget1, st1, si1, walkerSpeed1,
                trail1Data, tc1, tt1, trailPositions1, trailActiveCount1,
                halo1, core1, dt
            );
            stepWalker(
                wPos2, wVel2, wTarget2, st2, si2, walkerSpeed2,
                trail2Data, tc2, tt2, trailPositions2, trailActiveCount2,
                halo2, core2, dt
            );

            if (isScattering) {
                scatterSeedUniform.value = Math.floor(Math.random() * 0xffffff);
                renderer.compute(scatterCompute);
            }
            renderer.compute(updateCompute);
            renderer.render(scene, camera);
        }

    </script>
</body>

</html>
```
