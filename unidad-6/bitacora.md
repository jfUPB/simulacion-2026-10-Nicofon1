# Unidad 6

## Bitácora de proceso de aprendizaje

### Actividad 01: Un referente para pensar sistemas visuales

1.  **Selección de imágenes**: Analicé las obras de **Tyler Hobbs** tituladas **Elektroanima** (2020) y **Fresh Currents** (2018).

2.  **Decisiones visuales**:

    *   **Composición**: En **Elektroanima**, la composición es total, no hay espacios vacíos, todo está lleno de ese "ruido" de líneas q se cruzan. En **Fresh Currents**, hay una composición más direccional, como un río q va de una esquina a otra, tmbn llena el lienzo pero se siente con más movimiento hacia afuera.
    *   **Densidad**: **Elektroanima** tiene una densidad super alta pq las líneas son anchas y no dejan ver el fondo. **Fresh Currents** juega con la densidad para crear capas; donde hay más líneas se ve una sombra negra profunda y donde hay pocas se ve la luz del fondo.
    *   **Dirección del movimiento**: En **Elektroanima** el movimiento es circular y caótico, como si estuvieran atrapados en un laberinto. En **Fresh Currents** es un flujo fluido y orgánico, como si fuera una corriente de aire o agua. 
    *   **Color**: Ambas son monocromáticas (blanco/crema y negro). Esto me gusta pq hace q uno se fije solo en la textura y en el rastro q deja cada punto al moverse.
    *   **Ritmo**: **Elektroanima** tiene un ritmo lento y pesado, casi estático por lo apretadas q están las ondas. El de **Fresh Currents** es un ritmo super rápido, se siente la velocidad de los trazos.
    *   **Repetición y variación**: Se repite mucho el mismo tipo de trazo, pero la variación está en el ángulo con el q cada línea "decide" girar, lo q evita q se vea aburrido o mecánico.

3.  **¿Por qué son potentes?**
    R/ Me trama como algo q sale de código se puede ver tan "táctil". La potencia está en esa sensación de **orden dentro del caos**. Parece q hubiera una inteligencia o una regla invisible guiando cada línea, y eso le da una naturalidad q no se logra solo con random(). Ver como miles de agentes siguen una corriente invisible te hace sentir q estás viendo un proceso biológico real.

4.  **Hipótesis del sistema**:
    R/ Pa' mi q esto es puro **Flow Field** mezclado con **Autonomous Agents**. 
    *   En **Elektroanima**: el campo de flujo debe tener un ruido de muy alta frecuencia o un ángulo de giro muy cerrado para q las líneas se enreden así. Seguramente los agentes tienen un `maxForce` alto para poder dar esos giros tan bruscos sin salirse del camino.
    *   En **Fresh Currents**: es un Flow Field clásico con **Perlin Noise** de gran escala para q las curvas sean suaves. Lo q la hace ver así es q los agentes tienen una vida (lifespan) distinta y dejan un rastro muy fino. Tmbn puede q la aceleración dependa de la intensidad del ruido en ese punto, tons en unas partes van más rápido q en otras.

### Actividad 02: Agentes autónomos y steering forces

1. **Agente autónomo**: 
    R/ Es un ente q tiene "voluntad", o sea, no solo se mueve pq una fuerza lo empuja (como una pelota), sino q tiene su propio objetivo y decide como maniobrar para llegar allá.

2. **Steering force**: 
    R/ Es la fuerza de maniobra. Se calcula restando la velocidad actual de la "velocidad deseada" (`steering = desired - velocity`). Básicamente es lo q el agente hace para corregir su rumbo.

3. **Diferencia con fuerzas externas**: 
    R/ Las externas (gravedad, viento) te afectan quieras o no. La `steering force` nace de adentro del agente según lo q él perciba de su entorno.

4. **Utilidad en diseño**: 
    R/ Sirve para crear comportamientos q se sienten "vivos". Puedes diseñar agentes q tengan miedo, q sean curiosos o sociales, y eso da visuales mucho más orgánicas q la física simple.

### Actividad 03: Flow Fields

1. **Construcción**: 
    R/ Se hace una cuadrícula o rejilla invisible q cubre toda la pantalla.

2. **Celda/Vector**: 
    R/ Cada casilla de la rejilla guarda un vector q indica la dirección de la corriente en ese punto exacto.

3. **Consulta**: 
    R/ El agente mira en q posición `(x, y)` está y "lee" el vector q le corresponde a esa celda en la rejilla.

4. **Decisión**: 
    R/ Ese vector se vuelve su meta, y el agente calcula su `steering force` para girar y alinearse con esa corriente.

5. **Parámetros**: 
    R/ 
    - **Resolución**: tamaño de los cuadros (si es pequeño el flujo es mas detallado).
    - **maxspeed**: velocidad máxima.
    - **maxforce**: q tan fuerte puede girar (limita la maniobra).
    - **cantidad de agentes**: define la densidad de la textura.

6. **Modificación**: 
    R/ Si bajo mucho el `maxforce`, los agentes fluyen lento y con curvas suaves pq les cuesta girar. Si lo subo, se vuelven super nerviosos y siguen el campo casi en ángulos rectos.

7. **Reflexión**: 
    R/ Produce un movimiento tipo corriente de río o viento. Sugiere orden masivo y fluidez. Me lo imagino funcionando super bien con un tema de techno hipnótico o algo ambiental profundo.

### Actividad 04: Flocking

1. **Reglas básicas**: 
    R/ 
    - **Separación**: no te amontones con los vecinos.
    - **Alineación**: ve hacia donde va el promedio del grupo.
    - **Cohesión**: busca el centro de masa de tus vecinos para no quedarte solo.

2. **Parámetros**: 
    R/ Se controlan con "pesos" (weights), q definen q tan importante es cada una de las 3 reglas para el agente.

3. **Modificación**: 
    R/ Si le meto mucho peso a la **cohesión**, se vuelven una mancha densa q casi no se mueve. Si le subo a la **separación**, el grupo se rompe y parecen hormigas asustadas.

4. **Comportamiento observado**: 
    R/ Se ve fluido y orgánico. Los grupos se arman y desarman solos, se siente muy natural.

5. **Reflexión**: 
    R/ La atmósfera es de "comunidad" o sistema vivo. Funcionaría bien con música q tenga capas q se suman o coros complejos.

### Actividad 05: Comparar algoritmos como herramientas de diseño

R/ Aquí la comparativa rápida:

| Aspecto | Flow Fields | Flocking |
|---|---|---|
| **Movimiento** | Trayectorias fijas (corrientes) | Interacción grupal dinámica |
| **Control** | Alto (tú diseñas el campo) | Bajo (es emergente) |
| **Emergencia** | Baja | Muy Alta |
| **Atmósfera** | Orden, flujo, constancia | Vida, nerviosismo, colectividad |
| **Relación Musical** | Ritmos constantes, texturas | Cambios de energía, clímax |
| **Ventajas** | Ligero, fácil de predecir | Espectacular, muy orgánico |
| **Limitaciones** | Puede verse rígido | Come mucho CPU (O(n²)) |

**¿Qué usaría según la música?**

- **Contemplativa**: **Flow Field** con curvas muy suaves (Perlin noise lento). Da paz.
- **Agresiva**: **Flocking** con mucha separación y `maxspeed` alto. Se ve errático y violento.
- **Melancólica**: **Flow Field** lento con agentes q dejen rastro y mueran rápido (lifespan).
- **Eufórica**: **Flocking** con cohesión alta y un attractor q se mueva rápido. Se siente como una explosión de vida.

## Bitácora de aplicación 

### Actividad 06: Bitácora del Proyecto "Perspective - Klsr"

**1. Concepto visual**
R/ La obra Perspective - Klsr tiene algo muy peculiar porque en medio de su forma abstracta te transmite una sensacion que se siente demasiado pero es muy dificil de describir, pq a mi parecer es como un revueltijo de vacio con descubrimiento, con perdida y podria tirar mil adjetivos ocn los que no estaria 100% de acuerdo que lo describen, ent no encuentro mejor manera que expresar esa sensacion que a travez de las visuales

**2. Relación entre la visual y la canción**
R/La relación entre el audio y la pieza busca materializar visualmente ese algo indescriptible que se siente al escuchar la obra. En lugar de forzar emociones concretas, la canción actúa como una fuerza física sobre el sistema: las frecuencias controlan la rotación de los fragmentos, y la amplitud dicta la luminosidad y el rastro. Así, los cambios en la pista rompen la estabilidad del flujo visual, traduciendo esa tensión sonora abstracta en un comportamiento errático.

**3. Moodboard o referencias**
R/ 
<img width="736" height="1309" alt="image" src="https://github.com/user-attachments/assets/be68ae1d-6ed6-4955-b7f2-7b5a707ba7a0" />
<img width="736" height="736" alt="image" src="https://github.com/user-attachments/assets/6f46f11b-5bd4-4e25-bb1b-4ab9e62c9086" />
<img width="1158" height="801" alt="image" src="https://github.com/user-attachments/assets/9a1201a9-14b5-4c2f-8c9c-dc2655e48459" />




**4. Bocetos**
R/
<img width="841" height="1280" alt="image" src="https://github.com/user-attachments/assets/b4db3c5b-9d25-4794-94da-2e674cb87314" />
<img width="841" height="1280" alt="image" src="https://github.com/user-attachments/assets/ee289a0d-9bd8-476f-905d-6e8cd3908852" />


**5. Mapa de decisiones**
R/ Todo en la visual tiene un por qué:
*   **El rastro (background condicionado al delta del volumen):** si la música fluye suave, el rastro es largo. Si hay un corte abrupto de volumen, borra el lienzo de golpe, dando esa sensación literal de "pérdida" o reinicio.
*   **Truco matemático de los vidrios (ilusión 3D con `cos`):** Da un efecto donde el vidrio te da una cara brillante y un respaldo opaco. Sirve pa' generar un contraste pesado entre la arena (fluida y plana) y los vidrios (fríos, afilados e intrusivos).
*   **El Glow (shadowBlur):** Pa' darle ese carácter inmersivo y de neón, pero apagándolo en la parte de atrás pa' no saturar la compu.

**6. Mapa de interpretación**
R/ La visual la "toco" yo en vivo como si fuera un instrumento, pa' acentuar los clímax de la canción:
*   **Mouse (clic sostenido + arrastrar):** Actúa como un repulsor masivo. Si lo paso por encima de la arena, rasga el flujo y los agentes huyen despavoridos. Lo uso pa' inyectar tensión manual.
*   **Barra espaciadora:** Invierte todos los vectores del Flow Field. Todo empieza a fluir pa' atrás. Es un efecto brutal pa' acentuar los *drops* o silencios raros de la pista.
*   **Clic central (Rueda):** Play/Pause para iniciar la obra.

**7. Justificación del algoritmo elegido**
R/ Hice una quimera entre **Flow Fields** y **Flocking (Separation)**. 
Elegí el Flow Field pa' tener esa corriente de tiempo armónica (el descubrimiento). Pero el Flocking no está prendido siempre, es condicional. La regla de *Separación* solo se prende cuando un agente pasa cerca de un vidrio que está rotando durísimo por un golpe de bajo. Ahí entran en pánico, se hace un espiral errático del que intentan huir, y cuando se alejan vuelven a su paz. Transmite perfecto esa "tensión sonora abstracta".

**8. Uso explícito de IA como materializador**
R/ El concepto, la dirección de arte, y la decisión de mezclar flow fields con flocking condicional son 100% míos. Usé a la IA (Gemini) como un partner técnico para un par de cosas pesadas: primero, armar "laboratorios" que me escupieran en JSON los datos exactos en milisegundos de la canción para afinar la detección de bajos; segundo, sacar la matemática para el falso 3D de los vidrios; y tercero, lograr el *Batched Rendering* (`beginShape(LINES)`) pa' que la compu aguantara miles de partículas sin que los fotogramas se fueran al piso.

**9. Código fuente y Enlace al sketch**
R/ *https://editor.p5js.org/Nicofon1/sketches/FL4AWjJA3
```
let song;
let amp;
let fft;

// Arreglos
let agents = [];
let shards =[];

// Variables Flow Field
let prevVol = 0; 
let balance = 0.5; 
let zoff = 0;      

// Detección de bajo (sensibilidad ajustada)
let bassState = { peak: 0 };
let invertFlow = false; // Control de inversión de tiempo

function preload() {
  song = loadSound('Perspective.mp3'); 
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  amp = new p5.Amplitude();
  fft = new p5.FFT();
  
  // 500 Agentes de arena
  for (let i = 0; i < 700; i++) agents.push(new Agent());
  
  // 15 Fragmentos flotantes en posiciones aleatorias
  for (let i = 0; i < 12; i++) shards.push(new Shard(random(width), random(height)));
  
  background(10, 10, 15);
}


function draw() {
  let spectrum = fft.analyze();
  let currentVol = amp.getLevel();
  
  let bass = fft.getEnergy("bass");
  let lowMid = fft.getEnergy("lowMid");
  let mid = fft.getEnergy("mid");
  let treble = fft.getEnergy("treble");

  // =================================================================
  // 1. DETECCIÓN DEL GOLPE (BEAT)
  // =================================================================
  let isBeat = false;
  let empuje = bass - bassState.peak;
  
  if (bass > bassState.peak) {
    if (empuje > 3 && bass > 160) {
      isBeat = true; 
    }
    bassState.peak = bass; 
  } else {
    bassState.peak -= 0.5; 
  }
  if (bassState.peak < 0) bassState.peak = 0;

  // =================================================================
  // 2. BALANCE Y FLOW FIELD
  // =================================================================
  let energiaTotal = bass + lowMid + mid + treble;
  let balanceCrudo = 0.5;
  if (energiaTotal > 0) balanceCrudo = (mid + treble) / energiaTotal;
  balance = lerp(balance, balanceCrudo, 0.1);

  let noiseScale = map(balance, 0.39, 0.42, 0.001, 0.02, true);
  let zSpeed = map(balance, 0.39, 0.42, 0.001, 0.02, true);

  // Rastro (Fondo semi-transparente)
 // =================================================================
  // Rastro (Fondo semi-transparente)
  // =================================================================
  drawingContext.shadowBlur = 0; // APAGAMOS EL GLOW PARA EL FONDO
  
  let deltaVol = max(0, currentVol - prevVol);
  let alphaTrail = map(deltaVol, 0, 0.08, 4, 100, true);
  noStroke(); 
  fill(10, 10, 15, alphaTrail); 
  rect(0, 0, width, height);;
  
  if (song.isPlaying()) {
   // 3. DIBUJAR ARENA (OPTIMIZACIÓN: Renderizado en Lote)
    
    // Calculamos el brillo una sola vez para todos
    let brightness = map(currentVol, 0.08, 0.24, 20, 255, true);
    stroke(255, brightness);
    strokeWeight(1.5);
        // --- MAGIA DE POST-PROCESAMIENTO ---
    // El tamaño del glow pulsa con el volumen de la canción
    drawingContext.shadowBlur = map(currentVol, 0.08, 0.24, 2, 15, true); 
    drawingContext.shadowColor = color(200, 220, 255, brightness); // Azul/blanco fantasmal
    // -----------------------------------
    // Abrimos el lote de líneas
    beginShape(LINES); 
    
    for (let i = 0; i < agents.length; i++) {
      let n = noise(agents[i].pos.x * noiseScale, agents[i].pos.y * noiseScale, zoff);
      let angle = map(n, 0, 1, 0, TWO_PI * 4);
      let flowForce = p5.Vector.fromAngle(angle).mult(0.5); 
      
      if (invertFlow) flowForce.mult(-1);
      
      agents[i].applyForce(flowForce);
      agents[i].interact(shards, agents); 
      agents[i].update();
      agents[i].edges();
      
      // En lugar de llamar a display(), añadimos los dos puntos de la línea al lote
      vertex(agents[i].pos.x, agents[i].pos.y);
      vertex(agents[i].prevPos.x, agents[i].prevPos.y);
      
      agents[i].updatePrev(); // Actualizamos la memoria de la posición
    }
    
    // Mandamos a dibujar las miles de líneas de un solo golpe
    endShape();

    // 4. Dibujar Fragmentos 3D
    for (let i = 0; i < shards.length; i++) {
      shards[i].update(isBeat);
      shards[i].display(currentVol);
    }
  }
  
  zoff += zSpeed;
  prevVol = currentVol;
}

function mousePressed() {
  // Comprobamos si el botón presionado es el central (la rueda)
  if (mouseButton === CENTER) {
    if (getAudioContext().state !== 'running') {
      userStartAudio();
    }
    
    if (song.isPlaying()) {
      song.pause();
    } else {
      song.play();
    }
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  background(10, 10, 15);
}

// =================================================================
// CLASE FRAGMENTOS MEJORADA (Flotantes, 3 ejes y 2 caras)
// =================================================================
class Shard {
  constructor(x, y) {
    this.pos = createVector(x, y);
    // Velocidad de flotación libre
    this.vel = p5.Vector.random2D().mult(random(0.1, 0.5));
    // Tamaño más pequeño
    this.size = random(10, 25);
    
    // Tres ángulos para simular rotación en todos los ejes
    this.xAngle = random(TWO_PI);
    this.yAngle = random(TWO_PI);
    this.zAngle = random(TWO_PI);
    
    this.spinSpeed = 0.005; // Rotación lenta y natural por defecto
    this.flash = 0;
  }

  update(isBeat) {
    // Flotar y aparecer por los bordes
    this.pos.add(this.vel);
    if (this.pos.x > width + 50) this.pos.x = -50;
    if (this.pos.x < -50) this.pos.x = width + 50;
    if (this.pos.y > height + 50) this.pos.y = -50;
    if (this.pos.y < -50) this.pos.y = height + 50;

    // Reaccionar al golpe de la música
    if (isBeat) {
      this.spinSpeed = random(0.1, 0.25); // Más controlado, sin ser licuadora
      this.flash = 255;
    }
    
    // Inercia: frenado suave
    this.spinSpeed = lerp(this.spinSpeed, 0.005, 0.05);
    
    // Aplicar giro en los tres ejes
    this.xAngle += this.spinSpeed * 1.2;
    this.yAngle += this.spinSpeed * 0.8;
    this.zAngle += this.spinSpeed * 0.3;
    
    if (this.flash > 0) this.flash -= 10;
  }

  display(vol) {
    push();
    translate(this.pos.x, this.pos.y);
    
    // Rotación 2D base
    rotate(this.zAngle); 
    
    // Magia 3D: Coseno en X y Y
    let scaleX = cos(this.yAngle);
    let scaleY = cos(this.xAngle);
    scale(scaleX, scaleY); 

    let baseAlpha = map(vol, 0.08, 0.24, 50, 200, true);
    
    // EL TRUCO: ¿Nos está dando la cara o la espalda?
        let isFront = (scaleX * scaleY) > 0;

    if (isFront) {
      // CARA FRONTAL (Brilla y reacciona al beat)
      
      // --- GLOW DEL VIDRIO ---
      drawingContext.shadowBlur = 15 + this.flash; // Estalla con el beat
      drawingContext.shadowColor = color(255, 255, 255);
      // -----------------------
      
      fill(10, 10, 15, 180);
      stroke(255, baseAlpha + this.flash);
      strokeWeight(1.5);
    } else {
      // CARA TRASERA (Opaca y oscura)
      
      drawingContext.shadowBlur = 0; // La espalda no emite luz
      
      fill(20, 20, 25, 200); 
      stroke(100, baseAlpha); 
      strokeWeight(1);
    }
    // Dibujar cristal (rombo asimétrico)
    beginShape();
    vertex(0, -this.size);         
    vertex(this.size * 0.4, 0);    
    vertex(0, this.size * 1.5);    
    vertex(-this.size * 0.4, 0);   
    endShape(CLOSE);

    // Detalle de luz interior si es la cara frontal
    if (isFront) {
      stroke(255, (baseAlpha + this.flash) * 0.5);
      strokeWeight(0.5);
      line(0, -this.size, 0, this.size * 1.5);
    }

    pop();
  }
}
// Activar o desactivar la inversión del tiempo con la Barra Espaciadora
function keyPressed() {
  if (key === ' ') {
    invertFlow = !invertFlow;
  }
}
class Agent {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    
    // Controles de física
    this.maxSpeed = 2; 
    this.maxForce = 0.1; 
    
    this.prevPos = this.pos.copy(); 
  }

  update() {
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0); 
  }

  applyForce(force) {
    this.acc.add(force);
  }

  // =======================================================
  // NUEVA FUNCIÓN: Interacción con los Vidrios y Flocking
  // =======================================================
  interact(shards, allAgents) {
    let chaosLevel = 0; // Nivel de pánico del agente
    let spiralForce = createVector(0, 0);

    // 1. EVALUAR LOS VIDRIOS CERCANOS
    for (let shard of shards) {
      let vectorToShard = p5.Vector.sub(shard.pos, this.pos);
      let dSq = vectorToShard.magSq(); // magSq es más rápido que dist() para la compu
      
      // Si está a menos de 150 píxeles de un vidrio (150^2 = 22500)
      if (dSq < 22500) {
        let d = sqrt(dSq);
        
        // Mapeamos qué tanto brilla el vidrio (0 a 255) a la fuerza de repulsión
        let shardInfluence = map(shard.flash, 0, 255, 0, 1.5);
        
        if (shardInfluence > 0) {
          chaosLevel += shardInfluence; // El agente entra en pánico
          
          // Fuerza Tangencial (hace el espiral)
          let tangent = createVector(-vectorToShard.y, vectorToShard.x).normalize();
          
          // Fuerza de Escape (los empuja suavemente hacia afuera para que no se queden atrapados)
          let escape = vectorToShard.copy().mult(-1).normalize();
          
          // Combinamos espiral + escape
          let combinedForce = p5.Vector.add(tangent, escape).mult(shardInfluence);
          
          // Entre más cerca del centro, más fuerte el empuje
          let proximidad = map(d, 0, 150, 2, 0); 
          combinedForce.mult(proximidad);
          
          spiralForce.add(combinedForce);
        }
      }
    }

    // Aplicar la fuerza de los vidrios
    if (spiralForce.magSq() > 0) {
      spiralForce.limit(this.maxForce * 3); // Dejamos que rompa el límite normal un poco
      this.applyForce(spiralForce);
    }

    // 2. FLOCKING (Separación Errática) CONDICIONADO
    // Solo hacen flocking si el nivel de caos es alto (hay un vidrio girando cerca)
    if (chaosLevel > 0.1) {
      let steer = this.separate(allAgents);
      // Multiplicamos la fuerza de separación por el nivel de pánico
      steer.mult(chaosLevel); 
      this.applyForce(steer);
      
      // Aumentamos su velocidad máxima temporalmente para el efecto de "susto"
      this.maxSpeed = 4;
    } else {
      // Si no hay vidrios girando cerca, fluyen en paz
      this.maxSpeed = 2;
    }
    // 3. INTERACCIÓN MANUAL (El toque del artista)
    // Si el mouse está presionado, actúa como un repulsor violento
    if (mouseIsPressed) {
      let mousePos = createVector(mouseX, mouseY);
      let vectorToMouse = p5.Vector.sub(this.pos, mousePos);
      let dSq = vectorToMouse.magSq();

      // Si el agente está a menos de 200px del mouse (200^2 = 40000)
      if (dSq < 40000) { 
        let repulse = vectorToMouse.normalize();
        repulse.mult(this.maxForce * 10); // Fuerza masiva de repulsión
        this.applyForce(repulse);
        this.maxSpeed = 6; // Entran en pánico total
      }
    }
  }

  // La regla de "Separación" pura de Craig Reynolds (Naturaleza del Código)
  separate(agents) {
    let desiredSeparation = 15; 
    let sum = createVector();
    let count = 0;
    
    for (let other of agents) {
      let dSq = p5.Vector.sub(this.pos, other.pos).magSq();
      
      // Si está demasiado cerca de otro grano de arena
      if (dSq > 0 && dSq < desiredSeparation * desiredSeparation) {
        let diff = p5.Vector.sub(this.pos, other.pos);
        diff.normalize();
        let d = sqrt(dSq);
        diff.div(d); // Mientras más cerca, más fuerte es el deseo de huir
        sum.add(diff);
        count++;
      }
    }
    
    if (count > 0) {
      sum.div(count);
      sum.normalize();
      sum.mult(this.maxSpeed);
      let steer = p5.Vector.sub(sum, this.vel);
      steer.limit(this.maxForce * 2);
      return steer;
    }
    return createVector(0, 0);
  }

// ELIMINAMOS display(col) porque ahora el sketch dibujará todo de golpe
  
  updatePrev() {
    this.prevPos.x = this.pos.x;
    this.prevPos.y = this.pos.y;
  }

  updatePrev() {
    this.prevPos.x = this.pos.x;
    this.prevPos.y = this.pos.y;
  }

  edges() {
    if (this.pos.x > width) { this.pos.x = 0; this.updatePrev(); }
    if (this.pos.x < 0) { this.pos.x = width; this.updatePrev(); }
    if (this.pos.y > height) { this.pos.y = 0; this.updatePrev(); }
    if (this.pos.y < 0) { this.pos.y = height; this.updatePrev(); }
  }
}
```

**10. Capturas o registros de momentos importantes**
R/ 
<img width="1919" height="913" alt="image" src="https://github.com/user-attachments/assets/9f5fc90b-fdc6-48d8-9e63-bc2a7d4f7332" />

<img width="1919" height="918" alt="image" src="https://github.com/user-attachments/assets/8ad14611-5a95-4f7d-862e-f265e67c18f7" />

<img width="1919" height="891" alt="image" src="https://github.com/user-attachments/assets/f2aa928e-7e92-438a-b47f-3108770568b3" />


## Bitácora de reflexión
