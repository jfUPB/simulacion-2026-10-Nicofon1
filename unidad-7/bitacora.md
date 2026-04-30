# Unidad 7

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

### Actividad 05

**Palabra elegida:**
BLACK HOLE (Visualizada como BLACK H   LE).

**Justificación conceptual:**
Representar la fuerza destructiva e ineludible de un agujero negro. La obra ilustra cómo la gravedad extrema no solo afecta el entorno (asteroides, estrellas), sino que termina devorando y desintegrando su propio significado y estructura.

**Análisis de su significado visual y comportamental:**
*   **Visual:** La palabra no es sólida; está compuesta por un enjambre de partículas (polvo estelar) en equilibrio. La letra "O" se omite tipográficamente y es reemplazada por la representación del fenómeno astronómico (horizonte de sucesos y disco de acreción con brillo intenso).
*   **Comportamental:** El sistema existe en gravedad cero. Al activarse la fuerza, los resortes que mantienen la forma de las letras ceden ante la tracción del agujero negro. La materia circundante es arrastrada en espiral, pierde velocidad al acercarse al centro, se comprime (reduce su escala) y es absorbida por el vacío.

**Moodboard o referencias:**
*[Inserta aquí tus imágenes]* 
Sugerencia: Incluye capturas de la película *Interstellar* (Gargantúa), la fotografía real del Event Horizon Telescope (agujero negro M87*), y referencias de redes de nodos o polvo estelar.


**Mapa de decisiones:**
*   **Forma:** Letras generadas con `textToPoints` convirtiendo la tipografía en partículas físicas independientes.
*   **Física (Matter.js):** Gravedad del mundo en 0. Uso de `Constraint` con tensión baja (`stiffness: 0.01`) para anclar las partículas de la letra, permitiendo que se deformen y rompan bajo presión o por colisiones.
*   **Cuerpos externos:** Polígonos irregulares (basura espacial) con restitución alta (0.9) y fricción casi nula para generar colisiones violentas y aleatorias contra la palabra.
*   **Visualización:** Uso intensivo de `drawingContext.shadowBlur` (Glow) para diferenciar térmicamente los objetos (azul para estrellas lejanas, naranja para texto y chatarra caliente).
*   **Interacción:** Control manual de la fuerza del vórtice usando la posición `mouseY`.

**Mapa de interpretación:**
1.  **Estado de reposo (Ratón arriba):** El agujero negro es un punto diminuto. Fuerza en 0. La palabra es legible. Sonido silenciado y ahogado.
2.  **Transición (Ratón bajando):** El horizonte de sucesos se expande. Comienza la fuerza de atracción tangencial. Asteroides chocan contra la palabra. El audio sube su volumen progresivamente.
3.  **Estado crítico (Ratón abajo):** Fuerza máxima. Las letras se desfiguran. Los objetos que entran en un radio de 150px sufren freno gravitacional, caen en espiral, se encogen al llegar a 60px y desaparecen en el centro. El audio alcanza su pico de volumen y el filtro paso bajo se abre para emitir frecuencias agudas y perturbadoras.
4.  **Clic en pantalla:** Activa pantalla completa y arranca el motor de audio en loop.

**Explicación de la relación entre audio y comportamiento:**
El comportamiento del audio está mapeado directamente a la variable de fuerza del agujero negro (controlada por el usuario). Al aumentar la fuerza de succión visual, ocurren dos cosas en el audio:
1. El volumen sube del 0% al 100%.
2. Un filtro `LowPass` aumenta su frecuencia de corte (de 150Hz a 3000Hz). Esto significa que cuando el agujero está "lejos" o inactivo, el sonido es un retumbo sordo; al abrirse, el sonido se vuelve nítido, agresivo y directo. El loop se mantiene constante mediante dos pistas desfasadas y un reverb de 4 segundos.

**Evidencia del uso de IA:**
Se utilizó IA como herramienta de apoyo técnico para:
*   Generar la sintaxis básica de integración entre p5.js y Matter.js.
*   Escribir las fórmulas matemáticas de los vectores de fuerza (atracción + tangencial) para simular el remolino gravitacional.
*   Calcular el encogimiento de escala (`scale`) y el freno de velocidad (`velocity * 0.92`) previos a la absorción.
*   Construir el motor de crossfade y filtros para evitar cortes en el loop del archivo de audio corto.
*   *(Las decisiones de interacción, posición, colores, ajuste de físicas, alteración del texto y el concepto central son de estricta autoría humana).*
https://editor.p5js.org/Nicofon1/sketches/vO0mckiHv


<img width="1914" height="1074" alt="image" src="https://github.com/user-attachments/assets/e180ff95-841b-43c7-806e-1a22cc3bdf13" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/2a9d69f5-35bb-4341-855c-914c7cf67621" />

```
const { Engine, World, Bodies, Body, Composite, Constraint } = Matter;

let engine;
let world;
let particles =[];
let floatingStars =[];
let debris =[]; 
let font;

// NUEVAS VARIABLES DE AUDIO
let drone1;
let drone2;
let reverb;
let filtro;
let audioIniciado = false;

let holeX = 0;
let holeY = 0;
let fontSize;

function preload() {
  font = loadFont('https://cdnjs.cloudflare.com/ajax/libs/ink/3.1.10/fonts/Roboto/roboto-black-webfont.ttf'); 
  
  // Cargamos el mismo audio en dos variables distintas
  drone1 = loadSound('agujero.mp3'); 
  drone2 = loadSound('agujero.mp3'); 
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  engine = Engine.create();
  world = engine.world;
  engine.world.gravity.y = 0; 

  // CONFIGURACIÓN DE AUDIO AVANZADA
  reverb = new p5.Reverb();
  filtro = new p5.LowPass();

  // Desconectamos la salida directa para pasarlos por los efectos
  drone1.disconnect();
  drone2.disconnect();
  
  // Conectamos ambos audios al Filtro
  drone1.connect(filtro);
  drone2.connect(filtro);
  
  // Conectamos el filtro al Reverb (4 segundos de eco para disimular los cortes)
  reverb.process(filtro, 4, 2);

  fontSize = width / 6;
  
  let textX = -fontSize * 3.8; 
  let textY = fontSize * 0.35;

  holeX = fontSize * 0.7; 
  holeY = -fontSize * 0.05; 

  let points = font.textToPoints('BLACK H    LE', textX, textY, fontSize, {
    sampleFactor: 0.2
  });

  for (let pt of points) {
    let pBody = Bodies.circle(pt.x, pt.y, 2, { frictionAir: 0.05 });
    let anchor = Constraint.create({
      pointA: { x: pt.x, y: pt.y },
      bodyB: pBody,
      stiffness: 0.01, 
      damping: 0.1
    });
    particles.push(pBody);
    Composite.add(world,[pBody, anchor]);
  }

  for(let i = 0; i < 80; i++) {
    let fs = Bodies.circle(random(-width/2, width/2), random(-height/2, height/2), random(1, 3), { 
      frictionAir: 0.01 
    });
    Body.setVelocity(fs, { x: random(-1, 1), y: random(-1, 1) });
    floatingStars.push(fs);
    Composite.add(world, fs);
  }

  for(let i = 0; i < 15; i++) {
    let lados = floor(random(3, 7));
    let radio = random(10, 25);
    let rock = Bodies.polygon(random(-width/2, width/2), random(-height/2, height/2), lados, radio, {
      frictionAir: 0.001, 
      restitution: 0.9,   
      density: 0.01       
    });
    Body.setVelocity(rock, { x: random(-4, 4), y: random(-4, 4) });
    Body.setAngularVelocity(rock, random(-0.1, 0.1));
    debris.push(rock);
    Composite.add(world, rock);
  }
}

function draw() {
  background(10, 10, 15);
  Engine.update(engine);

  translate(width / 2, height / 2);

  let vortexStrength = map(mouseY, height * 0.5, height, 0, 0.0006, true);
  let halfW = width / 2;
  let halfH = height / 2;

  // -------------------------------------------------------------
  // CONTROL DINÁMICO DE AUDIO Y VOLUMEN
  // -------------------------------------------------------------
  if (audioIniciado) {
    let volumen = map(vortexStrength, 0, 0.0006, 0.0, 1.0, true);
    
    // Cambiamos el volumen de las DOS pistas con una transición suave (0.1 seg)
    drone1.setVolume(volumen, 0.1); 
    drone2.setVolume(volumen, 0.1); 

    // El filtro hace que el audio suene sordo y lejano al principio, 
    // y se vuelva nítido y aterrador cuando el agujero se abre a máxima fuerza.
    let frecuenciaFiltro = map(vortexStrength, 0, 0.0006, 150, 3000, true);
    filtro.freq(frecuenciaFiltro);
  }

  // --- ESTRELLAS FLOTANTES ---
  drawingContext.shadowBlur = 20; 
  drawingContext.shadowColor = color(100, 200, 255);
  fill(200, 230, 255);
  noStroke();

  for (let fs of floatingStars) {
    aplicarRemolino(fs, vortexStrength, width); 
    
    let distAlCentro = dist(fs.position.x, fs.position.y, holeX, holeY);
    let escala = 1;

    if (vortexStrength > 0) {
      if (distAlCentro < 150) Body.setVelocity(fs, { x: fs.velocity.x * 0.92, y: fs.velocity.y * 0.92 });
      if (distAlCentro < 60) escala = map(distAlCentro, 10, 60, 0, 1, true);
      if (distAlCentro < 15) {
        Body.setPosition(fs, { x: random(-halfW, halfW), y: -halfH - 50 });
        Body.setVelocity(fs, { x: random(-1, 1), y: random(1, 3) });
      }
    }

    push();
    translate(fs.position.x, fs.position.y);
    scale(escala);
    ellipse(0, 0, fs.circleRadius * 2);
    pop();
    
    envolverPantalla(fs, halfW, halfH);
  }

  // --- BASURA ESPACIAL ---
  drawingContext.shadowBlur = 15;
  drawingContext.shadowColor = color(255, 100, 50); 
  stroke(150, 80, 50);
  strokeWeight(2);
  fill(40, 20, 20); 

  for (let d of debris) {
    aplicarRemolino(d, vortexStrength, width);

    let distAlCentro = dist(d.position.x, d.position.y, holeX, holeY);
    let escala = 1;

    if (vortexStrength > 0) {
      if (distAlCentro < 150) Body.setVelocity(d, { x: d.velocity.x * 0.92, y: d.velocity.y * 0.92 });
      if (distAlCentro < 60) escala = map(distAlCentro, 10, 60, 0, 1, true);
      if (distAlCentro < 15) {
        Body.setPosition(d, { x: random(-halfW, halfW), y: -halfH - 50 });
        Body.setVelocity(d, { x: random(-5, 5), y: random(2, 6) });
      }
    }

    push();
    translate(d.position.x, d.position.y);
    scale(escala); 
    beginShape();
    for (let vert of d.vertices) {
      vertex(vert.x - d.position.x, vert.y - d.position.y);
    }
    endShape(CLOSE);
    pop();

    envolverPantalla(d, halfW, halfH);
  }

  // --- TEXTO ---
  drawingContext.shadowBlur = 15;
  drawingContext.shadowColor = color(255, 150, 50);
  fill(255);
  noStroke();

  for (let p of particles) {
    aplicarRemolino(p, vortexStrength, fontSize * 5); 
    ellipse(p.position.x, p.position.y, 3);
  }

  // --- AGUJERO NEGRO ---
  dibujarAgujeroNegro(holeX, holeY, vortexStrength);

  drawingContext.shadowBlur = 0; 
}

function aplicarRemolino(cuerpo, fuerza, alcance) {
  if (fuerza <= 0) return; 

  let pos = cuerpo.position;
  let dir = createVector(holeX - pos.x, holeY - pos.y);
  let dist = dir.mag();

  if (dist < alcance) {
    dir.normalize();
    let attraction = p5.Vector.mult(dir, fuerza);
    let tangent = createVector(-dir.y, dir.x);
    tangent.mult(fuerza * 1.5);

    Body.applyForce(cuerpo, pos, { 
      x: attraction.x + tangent.x, 
      y: attraction.y + tangent.y 
    });
  }
}

function dibujarAgujeroNegro(x, y, fuerza) {
  push();
  translate(x, y);
  
  let glowDinamico = map(fuerza, 0, 0.0006, 2, 80);
  let haloBase = map(fuerza, 0, 0.0006, 10, 120); 
  let centroNegro = map(fuerza, 0, 0.0006, 3, 50); 
  let grosorBorde = map(fuerza, 0, 0.0006, 0.5, 3);

  drawingContext.shadowBlur = glowDinamico;
  drawingContext.shadowColor = color(255, 50, 0);

  fill(200, 50, 20, 80);
  noStroke();
  ellipse(0, 0, haloBase);
  
  fill(255, 100, 50, 150);
  ellipse(0, 0, haloBase * 0.7);

  drawingContext.shadowBlur = 0; 
  fill(0);
  stroke(255, 80, 0);
  strokeWeight(grosorBorde);
  ellipse(0, 0, centroNegro); 
  
  pop();
}

function envolverPantalla(cuerpo, halfW, halfH) {
  let pos = cuerpo.position;
  if(pos.x < -halfW - 50) Body.setPosition(cuerpo, {x: halfW + 50, y: pos.y});
  if(pos.x > halfW + 50) Body.setPosition(cuerpo, {x: -halfW - 50, y: pos.y});
  if(pos.y < -halfH - 50) Body.setPosition(cuerpo, {x: pos.x, y: halfH + 50});
  if(pos.y > halfH + 50) Body.setPosition(cuerpo, {x: pos.x, y: -halfH - 50});
}

// -------------------------------------------------------------
// EVENTO: Iniciar audio cruzado (Crossfade manual)
// -------------------------------------------------------------
function mousePressed() {
  if (!audioIniciado) {
    userStartAudio(); 
    
    // Arrancamos la pista 1 inmediatamente
    drone1.loop();
    
    // Obtenemos cuánto dura tu audio en milisegundos
    let duracion = drone1.duration() * 1000;
    
    // Programamos la pista 2 para que empiece exactamente por la MITAD de la pista 1.
    // Esto crea un solapamiento continuo infinito.
    setTimeout(() => {
      drone2.loop();
    }, duracion / 2);

    audioIniciado = true;
  }
  
  let fs = fullscreen();
  fullscreen(!fs);
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```


## Bitácora de reflexión
