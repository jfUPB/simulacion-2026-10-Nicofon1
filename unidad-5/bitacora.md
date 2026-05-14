# Unidad 5

## Bitácora de proceso de aprendizaje

### Actividad 01: Anatomía de una partícula

+ ¿Qué propiedades tiene cada partícula? Clasifícalas: ¿Cuáles definen su estado físico? ¿Cuáles su estado vital?

R/ Físico: pos, vel, acc. Vital: lifespan (tiempo de vida).

+ ¿Qué condición determina que una partícula "muere"? ¿Es una muerte instantánea o gradual?

R/ muere cuando lifespan llega a 0. Es gradual pq el valor baja en cada frame.

+ ¿Cómo se actualiza la partícula en cada frame? Identifica el patrón motion 101 dentro de la partícula.

R/ se suma acc a vel, vel a pos, y se baja el lifespan. El motion 101 es cambiar la posición basada en velocidad y aceleración.

+ ¿Quién crea las partículas? ¿En qué momento?

R/ el sketch principal (draw) las crea en cada frame agregándolas al array.

+ ¿Quién decide cuándo eliminar una partícula del array?

R/ una función (isDead) dentro de la clase Particle avisa, y el loop de draw las saca del array.

+ ¿Por qué se recorre el array en orden inverso para eliminar? ¿Qué pasaría si no se hiciera así?

R/ para q no se salte elementos al borrar, pq si borras el 2, el 3 pasa a ser el 2 y el loop se descuadra.

+ Si no eliminaras nunca las partículas, ¿Qué pasaría con la memoria y el rendimiento?

R/ la compu se pondría lenta y el kernel podría colapsar pq el array crece infinito hasta q no haya ram.

+ ¿Qué elementos visuales usa para representar una partícula?

R/ un círculo con borde y relleno q se va poniendo transparente.

+ ¿Cómo se conecta el "tiempo de vida" con la apariencia visual?

R/ se usa para el alpha del color, entre más vieja más invisible.

+ Si quisieras cambiar la representación visual (por ejemplo, usar líneas en vez de círculos), ¿Qué cambiarías y qué NO cambiarías?

R/ cambiaría solo la función show() o display(). No cambiaría nada de la lógica de movimiento ni el lifespan.

### Actividad 02: Del array al sistema: la abstracción del emisor

+ ¿Qué responsabilidades que antes estaban en draw() ahora están dentro de la clase Emitter?

R/ agregar partículas, recorrer el array para actualizarlas y borrarlas cuando mueren.

+ ¿Cuál es la ventaja de encapsular la lógica de emisión en una clase separada?

R/ q el código queda más ordenado y puedes tener muchos emisores en diferentes sitios sin repetir lógica.

+ En este ejemplo hay un array de emitters. ¿Quién crea los emitters? ¿Quién crea las partículas dentro de cada emitter?

R/ el sketch (mousePressed) crea los emitters. Cada emitter crea sus propias partículas adentro.

+ Dibuja un diagrama que muestre la jerarquía: sketch → [emitters] → [partículas]. ¿Cuántos niveles de "colección" hay?

R/ sketch -> array de emitters -> array de partículas. Hay 2 niveles de colección.

+ Describe este ejemplo usando palabras que NO mencionen p5.js...

R/ un grupo de centros (emisores) q gestionan el ciclo de vida de muchas entidades q nacen, se mueven y desaparecen solas.

### Actividad 03: Heterogeneidad: herencia y polimorfismo

+ ¿Qué tienen en común las subclases de partículas? ¿Qué tienen de diferente?

R/ común: física y vida. diferente: cómo se ven (una es un cuadro y gira).

+ ¿Por qué es importante que el Emitter no necesite saber qué tipo específico de partícula está gestiónando?

R/ pq así puede manejar cualquier bicho q herede de Particle sin cambiar el código del emisor.

+ Si mañana quisieras agregar un tercer tipo de partícula, ¿Qué tendrías que crear y qué NO tendrías que modificar?

R/ crearía una clase nueva q extienda a Particle. No tocaría nada del Emitter ni de las otras clases.

+ Compara con Example 4.2: ¿Cambió la lógica del Emitter? ¿Cambió la lógica de muerte? ¿Qué capa del sistema se modificó y cuáles permanecieron intactas?

R/ el emitter y la muerte siguen igual. Solo cambió la visualización y un poquito el comportamiento de rotación.

### Actividad 04: Fuerzas y partículas

+ En Example 4.6, ¿Dónde se define la gravedad? ¿Quién la aplica a las partículas? ¿Es una fuerza global o local?

R/ se define en draw() y se le pasa al sistema. Es global pq afecta a todas por igual.

+ En Example 4.7, ¿Qué diferencia hay entre la gravedad y la fuerza del repeller? ¿Dónde "vive" cada una?

R/ la gravedad es constante y vive en draw. El repeller es un objeto aparte q repele según posición.

+ La fuerza del repeller depende de la distancia entre la partícula y el repeller. ¿Qué principio físico se está modelando?

R/ la ley de gravitación universal (pero inversa) o fuerzas electrostáticas.

+ ¿Cambió la clase Particle entre Example 4.6 y 4.7? ¿Qué implica esto sobre la separación entre comportamiento de la partícula y fuerzas externas?

R/ no cambió nada, lo q implica q las partículas pueden recibir cualquier fuerza de afuera sin q ellas tengan q saber qué es.

+ Tabla comparativa:

R/ 

| Aspecto | 4.2 | 4.4 | 4.5 | 4.6 | 4.7 |
|---|---|---|---|---|---|
| ¿Quién crea partículas? | sketch | emitter | emitter | emitter | emitter |
| ¿Hay clase Emitter? | no | si | si | si | si |
| ¿Hay herencia? | no | no | si | no | no |
| ¿Hay fuerzas externas? | no | no | no | si | si |
| ¿Hay interacción entre elementos? | no | no | no | no | si (repeller) |
| ¿Cómo mueren las partículas? | lifespan 0 | lifespan 0 | lifespan 0 | lifespan 0 | lifespan 0 |



+ Modificación quirúrgica:

R/ Elegí (a) Cambiar la visualización sin cambiar fuerzas ni estructura.
- ¿Qué líneas de código toqué? la función show() o display() de Particle.
- ¿Qué clases/funciones modifiqué? Particle.display()
- ¿Qué partes del programa NO necesité modificar? draw, Emitter y Repeller.
- ¿Por qué fue posible hacer este cambio sin afectar las demás capas? pq la lógica de cómo se ve está separada de cómo se mueven (física).



### Actividad 05: Ejercicio de diseño "Ciclos de vida"

+ Concepto: 

R/ El ciclo de vida de la luz (fotones). Represento el nacimiento en una fuente, el viaje por el espacio (como onda o partícula) y la muerte al ser absorbidos por la materia (un muro arcoíris).

+ Mapa de decisiones:

R/
1. **Emisión**: a la izquierda salen fotones blancos "puros" de forma esporádica.
2. **Transformación (Prisma)**: el mouse controla un prisma q difracta la luz blanca en colores del arcoíris, cambiando su velocidad y tipo.
3. **Muerte**: los fotones mueren al tocar el muro de la derecha, causando un glow (reacción) q se apaga lento.
4. **Herencia/Polimorfismo**: uso clases para diferenciar fotones q se ven como puntos (partículas) y otros q vibran (ondas).

+ Implementación:

  https://editor.p5js.org/Nicofon1/sketches/3_LN_Qe8L
  <img width="698" height="485" alt="image" src="https://github.com/user-attachments/assets/f9be3295-6a91-47c2-b298-cf7645e74678" />

  <img width="946" height="797" alt="image" src="https://github.com/user-attachments/assets/18c7c97a-9a10-4878-a58b-3c04a8c7e30d" />


<img width="308" height="765" alt="image" src="https://github.com/user-attachments/assets/5767ad1b-8406-4383-be66-cbe5649aa1b4" />


```js
let system;
let wall;
let prism;

function setup() {
  createCanvas(800, 600);
  system = new Emitter(30, height / 2);
  wall = new RainbowWall();
  prism = new Prism();
}

function draw() {
  background(10, 15, 25);

  // El prisma sigue al mouse
  prism.update(mouseX, mouseY);
  prism.display();

  // El sistema de partículas corre
  system.run();

  // El muro arcoíris
  wall.display();
}

// --- CLASE EMISOR ---
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    // Esporádico: probabilidad de crear una blanca
    if (random(1) < 0.1) {
      this.particles.push(new WhitePhoton(this.origin.x, this.origin.y));
    }
  }

  run() {
    this.addParticle();
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.run();

      // Interacción con Prisma
      if (prism.contains(p.pos) && p instanceof WhitePhoton) {
        // Difracción: La blanca muere y nacen de colores
        this.diffract(p);
        this.particles.splice(i, 1);
        continue;
      }

      // Interacción con Muro
      if (wall.hits(p.pos)) {
        p.lifespan = 0; // Se absorbe
      }

      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }

  diffract(p) {
    let colors = [
      color(255, 50, 50),   // Rojo
      color(255, 150, 50),  // Naranja
      color(255, 255, 50),  // Amarillo
      color(50, 255, 50),   // Verde
      color(50, 150, 255),  // Azul
      color(150, 50, 255)   // Violeta
    ];
    for (let c of colors) {
      let angle = p.vel.heading() + random(-0.5, 0.5);
      let v = p5.Vector.fromAngle(angle);
      v.setMag(p.vel.mag() * random(0.8, 1.2));
      
      // Aleatoriamente tipo onda o partícula
      if (random(1) > 0.5) {
        this.particles.push(new WavePhoton(p.pos.x, p.pos.y, c, v));
      } else {
        this.particles.push(new ParticlePhoton(p.pos.x, p.pos.y, c, v));
      }
    }
  }
}

// --- CLASES DE PARTÍCULAS (HERENCIA Y POLIMORFISMO) ---
class Photon {
  constructor(x, y, col, vel) {
    this.pos = createVector(x, y);
    this.vel = vel || createVector(random(2, 5), random(-1, 1));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.col = col || color(255);
  }

  run() {
    this.update();
    this.display();
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    // vida infinita hasta q choque o salga
    if (this.pos.x > width || this.pos.x < 0 || this.pos.y > height || this.pos.y < 0) {
      this.lifespan = 0;
    }
  }

  display() {
    // Se define en las subclases
  }

  isDead() {
    return this.lifespan <= 0;
  }
}

class WhitePhoton extends Photon {
  constructor(x, y) {
    super(x, y, color(255, 200));
  }
  display() {
    push();
    drawingContext.shadowBlur = 15;
    drawingContext.shadowColor = color(255);
    noStroke();
    fill(255, 180);
    ellipse(this.pos.x, this.pos.y, 8, 8);
    pop();
  }
}

class ParticlePhoton extends Photon {
  constructor(x, y, col, vel) {
    super(x, y, col, vel);
  }
  display() {
    push();
    drawingContext.shadowBlur = 20;
    drawingContext.shadowColor = this.col;
    noStroke();
    // Varios niveles de brillo
    for (let i = 0; i < 2; i++) {
        let alpha = map(i, 0, 2, 200, 50);
        fill(red(this.col), green(this.col), blue(this.col), alpha);
        ellipse(this.pos.x, this.pos.y, 5 + i * 5, 5 + i * 5);
    }
    pop();
  }
}

class WavePhoton extends Photon {
  constructor(x, y, col, vel) {
    super(x, y, col, vel);
    this.angle = 0;
  }
  display() {
    this.angle += 0.2;
    push();
    drawingContext.shadowBlur = 10;
    drawingContext.shadowColor = this.col;
    stroke(this.col);
    strokeWeight(3);
    noFill();
    translate(this.pos.x, this.pos.y);
    rotate(this.vel.heading());
    beginShape();
    for (let i = -10; i < 10; i += 2) {
      let y = sin(this.angle + i * 0.5) * 5;
      vertex(i, y);
    }
    endShape();
    pop();
  }
}

// --- OBJETOS DE ESCENARIO ---
class RainbowWall {
  constructor() {
    this.segments = [];
    let colors = [
      color(255, 0, 0), color(255, 127, 0), color(255, 255, 0),
      color(0, 255, 0), color(0, 0, 255), color(75, 0, 130), color(148, 0, 211)
    ];
    for (let i = 0; i < 50; i++) {
      let y = map(i, 0, 50, 0, height);
      let x = width - 40 - sin(map(y, 0, height, 0, PI)) * 60;
      let c = colors[floor(map(y, 0, height, 0, colors.length))];
      this.segments.push({ x: x, y: y, col: c, glow: 0 });
    }
  }

  display() {
    for (let s of this.segments) {
      push();
      if (s.glow > 0) {
        drawingContext.shadowBlur = map(s.glow, 0, 255, 0, 40);
        drawingContext.shadowColor = s.col;
      }
      noStroke();
      let alpha = map(s.glow, 0, 255, 20, 230);
      fill(red(s.col), green(s.col), blue(s.col), alpha);
      rect(s.x, s.y, 40, height / 50 + 1);
      pop();
      
      if (s.glow > 0) s.glow -= 4; // Se apaga más lento
    }
  }

  hits(pPos) {
    for (let s of this.segments) {
      let d = dist(pPos.x, pPos.y, s.x, s.y);
      if (d < 25) {
        s.glow = 255;
        return true;
      }
    }
    return false;
  }
}

class Prism {
  constructor() {
    this.pos = createVector(0, 0);
    this.size = 80;
  }

  update(x, y) {
    this.pos.set(x, y);
  }

  display() {
    push();
    translate(this.pos.x, this.pos.y);
    drawingContext.shadowBlur = 25;
    drawingContext.shadowColor = color(100, 200, 255);
    stroke(150, 230, 255, 180);
    strokeWeight(3);
    fill(180, 240, 255, 30);
    triangle(0, -this.size/2, -this.size/2, this.size/2, this.size/2, this.size/2);
    pop();
  }

  contains(pPos) {
    return dist(pPos.x, pPos.y, this.pos.x, this.pos.y) < this.size/2;
  }
}

```




### Actividad 06

**Parte 1 — Principios fundamentales**

1. **Estado**: cada partícula guarda su propia información física como posición y velocidad.
2. **Ciclo de vida**: tienen un inicio, una transformación y un final; no duran para siempre.
3. **Colecciones**: el sistema organiza grupos de elementos que aparecen o desaparecen dinámicamente.
4. **Memoria**: saber cuándo crear y cuándo eliminar es fundamental para el rendimiento del programa.
5. **Responsabilidad**: hay que separar lo que hace cada partícula de la lógica que las controla a todas.
6. **Emisor**: es la clase o abstracción que simplifica la gestión de miles de objetos individuales.
7. **Jerarquía**: se pueden crear sistemas complejos donde un emisor maneja otros sub-emisores.
8. **Diversidad**: se pueden mezclar comportamientos distintos en un mismo grupo usando herencia.
9. **Fuerzas**: el sistema puede aplicar fuerzas globales (como gravedad) o locales (como repellers).
10. **Apariencia**: la lógica de cómo se mueven es independiente de cómo se dibujan visualmente.

**Parte 2 — Transferencia**

R/ me gustaria hacerlo en touch designer, en cuanto a logica creo que se mantrendia igual, desconosco touch designer ent no estoy seguro se se podria manejar una especie de clases y polimorfismo con herencia, solamente desde los nodos, si no ps tmbn se podria hacer con python, pero de base la logiac se mantendria igual lo diferente son el medio, acostubrarme a los nodos y depronto aprender a usar los pops para manejar las particulas desde la grafica
