# Unidad 4

## Bitácora de proceso de aprendizaje

### Actividad 01

+ Documenta en tu bitácora de aprendizaje los aspectos que más te llamaron la atención de la obra de Memo.

R/ Me gustó mucho como usa el movimiento armónico simple para crear patrones visuales que parecen complejos pero salen de reglas matemáticas super básicas, el ritmo se siente muy natural.

### Actividad 02

+ ¿Qué está pasando en esta simulación? ¿Cuál es la interacción?

R/ es un sistema rotando sobre su eje, la interaccion es q gira dependiendo de la posicion del mouse.

+ Nota que en cada frame se está trasladando el origen del sistema de coordenadas al centro de la pantalla. ¿Por qué crees que se hace esto?

R/ para q sea mas facil rotar los objetos desde el centro del lienzo y no desde la esquina superior izquierda.

+ Cuál es la relación entre el sistema de coordenadas y la función rotate().

R/ rotate() gira todo el sistema de coordenadas, tons los objetos se visualizan rotados respecto al origen (0,0).

+ ¿Por qué crees que se hace esto? y ¿Por qué aunque en cada frame se hace lo mismo, los elementos gráficos rotan?

R/ se dibuja en (0,0) pq el origen se movió ahí con translate, y rotan pq el angulo cambia en cada frame antes de dibujar.

+ ¿Qué hace la función heading()?

R/ devuelve el angulo de la direccion hacia donde apunta el vector.

+ ¿Qué hace la función push() y pop()?

R/ push() guarda el estado actual del lienzo (traslaciones, rotaciones, colores) y pop() lo restaura para no afectar lo q se dibuje despues.

+ ¿Qué hace rectMode(CENTER)?

R/ hace q el rectangulo se dibuje tomando las coordenadas x,y como su centro y no como la esquina.

+ ¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad?

R/ el angulo de rotacion debe ser igual al heading de la velocidad para q el objeto "mire" hacia donde se mueve.

### Actividad 03

+ Crea una simulación de un vehículo que puedas conducir...

R/
```js
let velocity;
let position;
let acceleration;
let topSpeed = 5;

function setup() {
  createCanvas(600, 400);
  position = createVector(width / 2, height / 2);
  velocity = createVector(0, 0);
  acceleration = createVector(0, 0);
}

function draw() {
  background(220);

  if (keyIsDown(LEFT_ARROW)) {
    acceleration.add(createVector(-0.1, 0));
  } else if (keyIsDown(RIGHT_ARROW)) {
    acceleration.add(createVector(0.1, 0));
  } else {
    acceleration.mult(0);
  }

  velocity.add(acceleration);
  velocity.limit(topSpeed);
  position.add(velocity);

  display();
}

function display() {
  let angle = velocity.heading();
  push();
  translate(position.x, position.y);
  rotate(angle);
  fill(127);
  stroke(0);
  triangle(-10, -5, 10, 0, -10, 5);
  pop();
}
```

### Actividad 04

+ ¿Qué modificación hay que hacer al motion 101 cuando se quiere agregar fuerzas acumulativas?

R/ hay q resetear la aceleracion multiplicandola por cero al final de cada frame pq sino las fuerzas se guardan para siempre.

+ ¿Cómo podrías modificar el código para que esto funcione?

R/ usando las funciones mousePressed() y mouseReleased() para activar un booleano de dragging y q el attractor siga el mouse si esta presionado y cerca.

### Actividad 05

+ ¿Cuál es la relación entre r y theta con las posiciones x y y?

R/ x es r * cos(theta) y y es r * sin(theta). basico de trigonometria.

+ ¿Qué ocurre? ¿Por qué? (con fromAngle(theta))

R/ el circulo se queda pegado al centro pq fromAngle crea un vector de magnitud 1 por defecto, tons casi no se mueve.

+ ¿Qué ocurre aquí? ¿Por qué? (con fromAngle(theta, r))

R/ vuelve a funcionar como antes pq ya le diste el radio r como magnitud del vector.

### Actividad 06

+ Realiza una simulación en la que puedas modificar estos parámetros y observar cómo se comporta la función sinusoide.

R/
```js
let angle = 0;
let angleVel = 0.05;
let amplitude = 100;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  translate(width/2, height/2);
  let y = amplitude * sin(angle);
  line(0, 0, 0, y);
  circle(0, y, 32);
  angle += angleVel;
}
```

### Actividad 07

+ La idea es que la modifiques incluyendo un concepto de la unidad 1 y la unidad 3.

R/
```js
class Oscillator {
  constructor() {
    this.angle = createVector();
    this.angleVelocity = createVector(random(-0.05, 0.05), random(-0.05, 0.05));
    // Unidad 1: aleatoriedad gaussiana para la amplitud
    this.amplitude = createVector(randomGaussian(width/4, 20), randomGaussian(height/4, 20));
  }

  update() {
    // Unidad 3: una "fuerza" de friccion angular constante
    this.angleVelocity.mult(0.999);
    this.angle.add(this.angleVelocity);
  }

  show() {
    let x = sin(this.angle.x) * this.amplitude.x;
    let y = sin(this.angle.y) * this.amplitude.y;
    push();
    translate(width / 2, height / 2);
    // Mas estilo
    stroke(0, 50);
    line(0, 0, x, y);
    fill(127, 100);
    circle(x, y, 16);
    pop();
  }
}

let oscillators = [];
function setup() {
  createCanvas(640, 400);
  for (let i = 0; i < 20; i++) oscillators.push(new Oscillator());
}
function draw() {
  background(255);
  for (let o of oscillators) {
    o.update();
    o.show();
  }
}
```

### Actividad 08

+ El reto es que hagas que esta onda se mueva como una ola.

R/ solo hay q sumarle un offset al angulo inicial en cada frame para q se desplace.

```js
let startAngle = 0;
let angleVel = 0.1;

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);
  let angle = startAngle;
  for (let x = 0; x <= width; x += 24) {
    let y = map(sin(angle), -1, 1, 50, 150);
    circle(x, y, 24);
    angle += angleVel;
  }
  startAngle += 0.02; // esto hace q se mueva
}
```

### Actividad 09

+ Modifica esta simulación para crear un sistema de dos resortes conectados en serie.

R/ se conecta el primer resorte al primer bob, y el segundo resorte usa la posicion del primer bob como ancla para el segundo.

```js
let bob1, bob2;
let spring1, spring2;

function setup() {
  createCanvas(600, 400);
  spring1 = new Spring(width/2, 10, 100);
  spring2 = new Spring(width/2, 110, 100);
  bob1 = new Bob(width/2, 100);
  bob2 = new Bob(width/2, 200);
}

function draw() {
  background(255);
  let gravity = createVector(0, 1);
  
  bob1.applyForce(gravity);
  bob2.applyForce(gravity);
  
  spring1.connect(bob1);
  spring2.anchor = bob1.position; // ancla al primero
  spring2.connect(bob2);
  
  bob1.update();
  bob2.update();
  
  spring1.showLine(bob1);
  spring2.showLine(bob2);
  bob1.show();
  bob2.show();
}
```

### Actividad 10

+ Modifica esta simulación para crear un sistema de dos péndulos conectados en serie.

R/ igual q los resortes, el segundo pendulo tiene como pivot la posicion del bob del primero.

```js
let p1, p2;

function setup() {
  createCanvas(600, 400);
  p1 = new Pendulum(width/2, 0, 150);
  p2 = new Pendulum(0, 0, 100); // el origin se actualiza en draw
}

function draw() {
  background(255);
  p1.update();
  p1.show();
  
  p2.pivot = p1.bob; // se cuelga del primero
  p2.update();
  p2.show();
}
```

### Actividad 10

+ Modifica esta simulación para crear un sistema de dos péndulos conectados en serie.

R/ Mi obra se basa en la narrativa de una "Marea Reactiva". La idea es simular un ecosistema de plankton bioluminiscente en el que la regla principal es la perturbación: los organismos mantienen un estado de calma azul y movimiento armónico (ondas) hasta que detectan movimiento externo (el mouse).

https://editor.p5js.org/Nicofon1/sketches/HjfIkBxHH

<img width="941" height="788" alt="image" src="https://github.com/user-attachments/assets/965488ca-4211-4af1-b969-6e80fccad03b" />

```
let strands = [];

function setup() {
  createCanvas(800, 600);
  for (let i = 0; i < 6; i++) {
    strands.push(new Colony(random(100, height - 100)));
  }
}

function draw() {
  background(5, 10, 20, 70); 
  
  for (let s of strands) {
    s.update();
    s.show();
  }
}

function keyPressed() {
  if (key === 'a' || key === 'A') {
    strands.push(new Colony(random(height)));
  }
}

class Colony {
  constructor(baseY) {
    this.baseY = baseY;
    this.points = [];
    this.t = random(1000); 
    
    for (let x = 0; x <= width; x += 30) {
      this.points.push({
        x: x,
        y: 0,
        angle: map(x, 0, width, 0, TWO_PI * 1.5),
        offset: random(1000) 
      });
    }
  }

  update() {
    this.t += 0.01;
    let mouse = createVector(mouseX, mouseY);

    for (let p of this.points) {
      let waveY = sin(p.angle + frameCount * 0.04) * 50;
      let currentShift = noise(p.x * 0.01, this.t) * 30;
      
      let targetPos = createVector(p.x, this.baseY + waveY + currentShift);
      
      let d = p5.Vector.dist(mouse, targetPos);
      p.distToMouse = d;
      
      if (d < 120) {
        let fear = p5.Vector.sub(targetPos, mouse);
        fear.setMag(map(d, 0, 120, 60, 0));
        targetPos.add(fear); 
      }
      
      p.currentPos = targetPos;

      p.dynamicSize = map(noise(p.x * 0.05, this.t), 0, 1, 2, 20);
    }
  }

  show() {
    for (let p of this.points) {
      let glow = map(sin(p.angle + frameCount * 0.1), -1, 1, 80, 255);
      
      let blueCol = color(0, 100, 255);
      let greenCol = color(0, 255, 150);
      
      let amt = map(p.distToMouse, 0, 150, 1, 0);
      amt = constrain(amt, 0, 1);
      let finalCol = lerpColor(blueCol, greenCol, amt);
      
      noStroke();
      fill(red(finalCol), green(finalCol), blue(finalCol), glow - 50);
      circle(p.currentPos.x, p.currentPos.y, p.dynamicSize * 2.5); 
      
      fill(255, glow);
      circle(p.currentPos.x, p.currentPos.y, p.dynamicSize * 0.6); 
    }
  }
}

function mousePressed() {
  for (let s of strands) {
    s.baseY = constrain(s.baseY + random(-100, 100), 50, height-50);
  }
}

```

<img width="1276" height="4826" alt="d2" src="https://github.com/user-attachments/assets/e199f0e8-62ae-4905-b849-63facb280bf2" />
 Veo oportunidades en hacer webs q no sean tan rígidas, usando física para q los botones o menús se sientan más naturales. Tmbn para mostrar datos de forma más movida y no solo con tablas aburridas, o para crear landing pages q llamen mas la atención con cosas q reaccionen al mouse. Básicamente ayuda a q lo q programe no se vea tan mecánico.
