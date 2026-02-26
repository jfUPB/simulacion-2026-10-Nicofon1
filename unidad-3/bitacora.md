# Unidad 3

## Bitácora de proceso de aprendizaje

### Actividad 01

+ Luego ver el video con la charla de Robert Hodgin, te dejo la bitácora para que desahogues tus pensamientos, emociones, reflexiones, preguntas, etc, sobre lo que viste y escuchaste.

R/ siento que no somos conciendes de que naturalmente vamos a estar dirigidos a hacer las cosas de la manera que nos consume menos energia, lo cual esta directamente relacionado con la ia, y hasta que no tengamos presente esa relacion en cada producto que desarrollamos vamos a perder y remplazar lo que nos hace humanos, vamos a perder el valor por el esfuezao, la capasidad de asombro y la misma voluntad de crear entre muchas otras cosas

### Actividad 02

+ ¿Por qué es necesario multiplicar la aceleración por cero en cada frame?
  
R/ para que en cada frame se apliquen las fuerzas de ese mismo instante y no se vayan sumando con las de los frames anteriores

+ ¿Por qué se multiplica por cero justo al final de update()?
  
R/ porque de esta manera la manera en que implica la aceleracion en los otros vectores ya fue aplicado y se deja listo para resivir las fuerzas del prox frame.


### Actividad 02

+ Friccion
  
```js
let movers = [];
let mu = 0.05;        // coeficiente de fricción
let groundHeight = 80;

function setup() {
  createCanvas(900, 500);

  for (let i = 0; i < 12; i++) {
    movers.push(new Mover());
  }
}

function draw() {
  background(245,0);

  drawGround();

  for (let mover of movers) {

    // Aplicar fricción solo si está tocando el suelo
    if (mover.onGround()) {
      let friction = mover.velocity.copy();
      friction.mult(-1);
      friction.normalize();
      friction.mult(mu * mover.mass); 
      mover.applyForce(friction);
    }

    mover.update();
    mover.checkEdges();
    mover.show();
  }
}

function drawGround() {
  fill(200, 180, 140);
  noStroke();
  rect(0, height - groundHeight, width, groundHeight);
}

class Mover {
  constructor() {
    this.mass = random(0.5, 4);
    this.radius = this.mass * 12;

    this.position = createVector(random(50, 200), height - groundHeight - this.radius);
    this.velocity = createVector(random(3, 8), 0);
    this.acceleration = createVector(0, 0);

    this.color = color(random(50,255), random(50,255), random(50,255));
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  onGround() {
    return this.position.y >= height - groundHeight - this.radius;
  }

  checkEdges() {
    if (this.position.x > width - this.radius) {
      this.position.x = width - this.radius;
      this.velocity.x *= -1;
    }
    if (this.position.x < this.radius) {
      this.position.x = this.radius;
      this.velocity.x *= -1;
    }
  }

  show() {
    fill(this.color);
    noStroke();
    circle(this.position.x, this.position.y, this.radius * 2);
  }
}

```

<img width="943" height="615" alt="image" src="https://github.com/user-attachments/assets/a331919c-0096-4c26-a69f-89bd29f338de" />

+ Friccion
  
```js
let balls = [];

let angle;
let speed;

let gravity;
let airDrag = 0.01;
let waterDrag = 0.2;

let waterLevel;

function setup() {
  createCanvas(900, 500);

  angle = -Math.PI / 4;
  gravity = createVector(0, 0.2);
  waterLevel = height * 0.65;
}

function draw() {
  background(220,0);

  drawEnvironment();

  for (let i = balls.length - 1; i >= 0; i--) {

    let b = balls[i];

    b.applyForce(gravity);

    let dragCoefficient =
      b.position.y > waterLevel ? waterDrag : airDrag;

    let speedMag = b.velocity.mag();

    if (speedMag > 0) {
      let drag = b.velocity.copy();
      drag.mult(-1);
      drag.normalize();
      drag.mult(dragCoefficient * speedMag * speedMag);
      b.applyForce(drag);
    }

    b.update();
    b.show();

    if (b.offScreen()) {
      balls.splice(i, 1);
    }
  }
}

function mousePressed() {

  speed = random(10, 30);
  angle += 0.25;

  let newBall = new Ball(140, waterLevel - 70);
  newBall.launch(angle, speed);

  balls.push(newBall);
}

function drawEnvironment() {

  // Agua
  noStroke();
  fill(100, 160, 255,5);
  rect(0, waterLevel, width, height - waterLevel);

  // Bloque
  fill(120);
  rect(80, waterLevel - 60, 120, 60);
}

class Ball {
  constructor(x, y) {

    this.mass = random(0.5, 3);
    this.radius = this.mass * 10;

    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);

    this.color = color(random(255), random(255), random(255));
  }

  launch(angle, speed) {
    this.velocity = p5.Vector.fromAngle(angle);
    this.velocity.mult(speed);
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    fill(this.color);
    noStroke();
    circle(this.position.x, this.position.y, this.radius * 2);
  }

  offScreen() {
    return (
      this.position.x > width ||
      this.position.y > height ||
      this.position.x < 0
    );
  }
}

```

<img width="952" height="633" alt="image" src="https://github.com/user-attachments/assets/99d33143-c9d3-4bca-bf91-aafc1b05e150" />


+ Gravedad
  
```js
let attractor;
let movers = [];
let G = 1;

function setup() {
  createCanvas(900, 600);
  attractor = new Attractor(width / 2, height / 2, 40);
}

function draw() {
  background(10,5);

  attractor.show();

  for (let mover of movers) {
    let force = attractor.attract(mover);
    mover.applyForce(force);

    mover.update();
    mover.show();
  }
}

function mousePressed() {
  for (let i = 0; i < 50; i++) {
    movers.push(new Mover());
  }
}

class Attractor {
  constructor(x, y, mass) {
    this.position = createVector(x, y);
    this.mass = mass;
  }

  attract(mover) {
    let force = p5.Vector.sub(this.position, mover.position);

    let distance = force.mag();
    distance = constrain(distance, 10, 100);

    force.normalize();

    let strength = (G * this.mass * mover.mass) / (distance * distance);
    force.mult(strength);

    return force;
  }

  show() {
    noStroke();
    fill(255, 200, 0);
    circle(this.position.x, this.position.y, this.mass * 2);
  }
}

class Mover {
  constructor() {
    this.mass = random(0.5, 3);
    this.radius = this.mass * 5;

    this.position = createVector(random(width), random(height));

    this.velocity = p5.Vector.random2D();
    this.velocity.mult(random(1, 3));

    this.acceleration = createVector(0, 0);

    this.color = color(
      random(100, 255),
      random(100, 255),
      random(100, 255)
    );
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    noStroke();
    fill(this.color);
    circle(this.position.x, this.position.y, this.radius * 2);
  }
}

```


<img width="939" height="736" alt="image" src="https://github.com/user-attachments/assets/1032cc5a-bfcf-4649-b89a-6ef11feba368" />


## Bitácora de aplicación 

### Actividad 02

+ Describe el concepto de tu obra generativa.


R/ de pequeño recuerdo mucho q cuando estaba estresado me iba a como una especie de fuente de agua grande en mi colegio y me ponia a lanzar pidras y q rebotaran, al hacer la actividad del drag me di cuenta q al tirar algo muy rapido al "agua" me rebotaba, y me hizo recordar todo esto, tons quise hacer algo que transmitiera esa calma y relajacion que me daba hacer rebotar piedras

<img width="942" height="617" alt="image" src="https://github.com/user-attachments/assets/f58b96be-8181-4720-94e5-390954ef516e" />

https://editor.p5js.org/Nicofon1/sketches/Umx-Sl1Am
  
```js
let stones = [];
let particles = [];
let stars = [];

let gravity;
let waterLevel;
let baseWaterLevel;

function setup() {
  createCanvas(900, 500);
  colorMode(HSL, 360, 100, 100, 1);

  gravity = createVector(0, 0.22);
  baseWaterLevel = height * 0.7;

  // Crear estrellas
  for (let i = 0; i < 120; i++) {
    stars.push(new Star());
  }
}

function draw() {

  // Fondo oscuro con leve persistencia
  noStroke();
  fill(220, 30, 8, 0.25);
  rect(0, 0, width, height);

  drawStars();

  waterLevel = baseWaterLevel + sin(frameCount * 0.01) * 5;
  drawWater();

  gravity.y = 0.2 + noise(frameCount * 0.01) * 0.05;

  // STONES
  for (let i = stones.length - 1; i >= 0; i--) {
    let s = stones[i];
    s.applyForce(gravity);

    if (s.position.y + s.h/2 > waterLevel) {

      if (s.velocity.x > 2 && s.velocity.y > 0) {
        let liftStep = s.velocity.x * 0.35;
        s.applyForce(createVector(0, -liftStep));
        s.velocity.x *= 0.95;

        for (let j = 0; j < 3; j++) {
          particles.push(new Particle(s.position.x, waterLevel));
        }
      }

      let drag = s.velocity.copy();
      drag.mult(-0.08);
      s.applyForce(drag);

      s.applyForce(createVector(0, -0.08));
    }

    s.update();
    s.showGlow(); // <- dibujamos glow primero
    s.show();

    if (s.offScreen()) stones.splice(i, 1);
  }

  // PARTICLES
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].show();
    if (particles[i].life <= 0) particles.splice(i, 1);
  }
}

function mousePressed() {
  let vx = random(6, 18);
  let vy = random(1, 3);
  stones.push(new Stone(20, waterLevel - 20, vx, vy));
}

function drawWater() {
  noStroke();
  fill(210, 70, 25, 0.4);

  beginShape();
  vertex(0, height);

  for (let x = 0; x <= width; x += 12) {
    let wave = noise(x * 0.01, frameCount * 0.01) * 20;
    vertex(x, waterLevel + wave);
  }

  vertex(width, height);
  endShape(CLOSE);
}

function drawStars() {
  for (let star of stars) {
    star.update();
    star.show();
  }
}

class Stone {
  constructor(x, y, vx, vy) {
    this.position = createVector(x, y);
    this.velocity = createVector(vx, vy);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
    this.w = random(20, 40);
    this.h = random(8, 16);
    this.angle = random(TWO_PI);
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);

    if (this.velocity.x > 0.5) {
      this.angle += this.velocity.x * 0.03;
    }
  }

  showGlow() {
    push();
    translate(this.position.x, this.position.y);
    rotate(sin(this.angle) * 0.15);

    let speed = this.velocity.mag();
    let hue = map(speed, 0, 20, 190, 230);

    noStroke();
    fill(hue, 60, 60, 0.15);
    ellipse(0, 0, this.w * 2.5, this.h * 2.5);

    pop();
  }

  show() {
    push();
    translate(this.position.x, this.position.y);
    rotate(sin(this.angle) * 0.15);

    let speed = this.velocity.mag();
    let hue = map(speed, 0, 20, 190, 230);
    let light = map(this.position.y, 0, height, 50, 75);

    fill(hue, 50, light, 0.9);
    noStroke();
    ellipse(0, 0, this.w, this.h);

    pop();
  }

  offScreen() {
    return (this.position.x > width || this.position.y > height);
  }
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-2, -0.5));
    this.life = 80;
  }

  update() {
    this.position.add(this.velocity);
    this.velocity.mult(0.97);
    this.life -= 2;
  }

  show() {
    noStroke();
    fill(200, 70, 70, this.life / 100);
    ellipse(this.position.x, this.position.y, 4);
  }
}

class Star {
  constructor() {
    this.x = random(width);
    this.y = random(height * 0.6);
    this.size = random(1, 3);
    this.offset = random(1000);
  }

  update() {}

  show() {
    let twinkle = noise(this.offset + frameCount * 0.01);
    let brightness = map(twinkle, 0, 1, 60, 100);

    noStroke();
    fill(60, 20, brightness, 0.8);
    ellipse(this.x, this.y, this.size);
  }
}
```
## Bitácora de reflexión


### Actividad 05

+  ¿Qué es el marco de movimiento motion 101 y cómo se relacionan: fuerza, aceleración, velocidad y posición?


R/ el motion 101 es uan forma de simular propiedades fisicas en codigo con el cual te puedes manejar vectorialmente propiedades de fuerza aceleracion velocidade y fuerza, la relacion entre estas es q la fuerza junto con la masa se relacionan para darte una aceleracion, frame a frame la magnitud de la aceleracion se le adiciona a la velocidad, en sus ambas componentes, la velocidad a la posicion y de esta manera se logra simular y se consigue toda la simulacion

+ Vas a analizar este video sobre el artista Alexander Calder. Selecciona una de sus obras y luego crea una obra generativa inspirada en la obra de Calder que seleccionaste y el marco de movimiento motion 101 con fuerzas que trabajamos en esta unidad.

https://editor.p5js.org/Nicofon1/sketches/7K153zcqu

<img width="913" height="758" alt="image" src="https://github.com/user-attachments/assets/5e3efffb-89f4-4aa3-ad8f-177ec41380f1" />

```js
let system;

function setup() {
  createCanvas(900, 800);
  angleMode(RADIANS);
  system = new MobileSystem(width / 2, 120);
  
}

function draw() {
  background(0,5);

  system.update();
  system.display();
}


/* =========================
   MOBILE SYSTEM
========================= */

class MobileSystem {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.root = this.createBranch(this.origin, 7);
  }

  createBranch(origin, depth) {
    if (depth <= 0) return null;

    let length = random(70, 150);
    let angle = random(-1, 1);
    let massSize = random(10, 26);

    let arm = new Arm(origin, length, angle, massSize);

    arm.child = this.createBranch(null, depth - 1);

    if (random() < 0.65) {
      arm.secondary = this.createBranch(null, depth - 2);
    }

    return arm;
  }

  update() {
    this.root.update(this.origin);
  }

  display() {
    this.root.display();
  }
}


/* =========================
   ARM
========================= */

class Arm {
  constructor(origin, length, angle, massSize) {
    this.origin = origin;
    this.length = length;
    this.angle = angle;

    this.aVel = random(-0.01, 0.01);
    this.aAcc = 0;

    this.damping = 0.995;
    this.massSize = massSize;

    this.child = null;
    this.secondary = null;

    this.color = color(
      random(100, 220),
      random(100, 220),
      random(100, 220),
      190
    );
  }

  update(parentOrigin) {
    if (parentOrigin) {
      this.origin = parentOrigin;
    }

    let gravity = 0.35;
    this.aAcc = (-gravity / this.length) * sin(this.angle);

    // VIENTO DEL MOUSE (atracción suave)
    let end = this.getEnd();
    let mouse = createVector(mouseX, mouseY);
    let dir = p5.Vector.sub(mouse, end);
    let dist = dir.mag();

    if (dist < 250) {
      dir.normalize();
      let strength = map(dist, 0, 250, 0.02, 0);
      this.aAcc += dir.x * strength * 0.5;
    }

    // Variación orgánica
    let organic = noise(frameCount * 0.01 + this.length) - 0.5;
    this.aAcc += organic * 0.002;

    this.aVel += this.aAcc;
    this.aVel *= this.damping;
    this.angle += this.aVel;

    if (this.child) this.child.update(end);
    if (this.secondary) this.secondary.update(end);
  }

  getEnd() {
    let x = this.origin.x + this.length * sin(this.angle);
    let y = this.origin.y + this.length * cos(this.angle);
    return createVector(x, y);
  }

  display() {
    let end = this.getEnd();

    // brazo

    
    stroke(255);
    
    strokeWeight(2);
    line(this.origin.x, this.origin.y, end.x, end.y);

    // masa orgánica
    push();
    translate(end.x, end.y);
    noStroke();
    fill(this.color);

    beginShape();
    for (let i = 0; i < 30; i++) {
      let ang = map(i, 0, 30, 0, TWO_PI);
      let r =
        this.massSize +
        noise(i * 0.4, frameCount * 0.02) * this.massSize * 0.4;
      vertex(r * cos(ang), r * sin(ang));
    }
    endShape(CLOSE);
    pop();

    if (this.child) this.child.display();
    if (this.secondary) this.secondary.display();
  }
}


/* =========================
   CLICK = IMPULSO
========================= */

function mousePressed() {
  system.root.aVel += random(-0.2, 0.2);
}
```


