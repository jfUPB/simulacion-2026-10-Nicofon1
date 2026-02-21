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



## Bitácora de reflexión
