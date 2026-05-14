# Unidad 2

## Bitácora de proceso de aprendizaje
### Actividad 01

+ qué trabajo te gustó más y por qué.

R/ 

## Bitácora de aplicación 

### Actividad 02

+ ¿Cómo funciona la suma dos vectores en p5.js?
  
R/ la clase vector tiene el metodo .add que recive otro vector y suma sus componentes.

+ ¿Por qué esta línea position = position + velocity; no funciona?

R/ pq el + no tiene la sobrecarga que reciva un vector.

### Actividad 03

+ ¿Qué tuviste que hacer para hacer la conversión propuesta?

R/ eliminar las variables x , y y remplasarla por componentes de position.

+ Escribe el código que utilizaste para resolver el ejercicio.

R/ 

```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(860, 860);
  walker = new Walker();
  background(200);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.position = createVector(width / 2, height / 2)

  }

  show() {
    noStroke();
    fill(color(random(255), random(255), random(255)));
    circle(this.position.x, this.position.y,7);
  }
  
  

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.position.x=this.position.x+5;
    } else if (choice == 1) {
      this.position.x=this.position.x-5;
    } else if (choice == 2) {
      this.position.y=this.position.y+5;
    } else {
      this.position.y=this.position.y-5;
    }
    
    if(floor(random(20))==2)
      if (choice == 0) {
        this.position.x=this.position.x+25;
      } else if (choice == 1) {
        this.position.x=this.position.x-25;
      } else if (choice == 2) {
        this.position.y=this.position.y+25;
      } else {
        this.position.y=this.position.y-25;
      }
  }
}

```

### Actividad 04

+ ¿Qué resultado esperas obtener en el programa anterior?

R/ver en consola los dos valores q tuvo el vetor y por ultimo un Only once 

+ ¿Qué resultado obtuviste?

R/  p5.Vector Object : [6, 9, 0] 
    p5.Vector Object : [20, 30, 0] 
    Only once 

+ ¿Qué tipo de paso se está realizando en el código?

R/ paso por referencia

+ ¿Qué aprendiste?

R/ el uso de la funcion copy().

### Actividad 05

+ ¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?

R/ mag() devuelve la magnitud del vector, con magSq() se ahorra la raiz lo cual es comveniente para el computo


+ ¿Para qué sirve el método normalize()?

R/ permite normalizar la magnitud del vector a 1, lo que nos permite usar la direccion.


+ Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?

R/ sirve para saber qué tan alineados están dos vectores.


+ El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?

R/ la de instancia se llama desde un vector, la estática recibe dos vectores como parámetros.


+ ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.

R/ el resultado es un vector perpendicular a los dos originales, su magnitud depende del ángulo entre ellos y la orientación sigue la regla de la mano derecha.


+ ¿Para que te puede servir el método dist()?

R/ para calcular la distancia entre dos puntos o vectores.


+ ¿Para qué sirven los métodos normalize() y limit()?

R/ normalize() fija la magnitud en 1 y limit() restringe la magnitud máxima del vector.

### Actividad 06

+ El código que genera el resultado.

R/
```js
let t =0;
let d =0.01;
function setup() {
    createCanvas(500, 500);
}

function draw() {
    background(200);
    if(t>1)
    d=-0.01;
    if(t<0)
    d=0.01;
    
    t+=d;
  
    let v0 = createVector(50, 50);
    let v1 = createVector(350, 0);
    let v2 = createVector(0, 350);
    let v4 = createVector(400, 50);
    let v5 = createVector(-350, 350);
    let c1 = color(0, 0, 255);
    let c2 = color(255, 0, 0);
  
  
    let v3 = p5.Vector.lerp(v1, v2, t);
    let v6 = lerpColor(c2, c1, t);
  
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, v6);
    drawArrow(v4, v5, 'green');
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(7);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```

+ ¿Cómo funciona lerp() y lerpColor().

R/

lerp() calcula un valor intermedio entre dos extremos usando una interpolación lineal proporcional.

lerpColor() aplica esa misma interpolación pero sobre los componentes del color.

+ ¿Cómo se dibuja una flecha usando drawArrow()?

R/ Se dibuja una línea con la dirección del vector y se rota un triángulo al final para simular la punta de la flecha.

### Actividad 07

+ Cuál es el concepto del marco motion 101 y cómo se interpreta geométricamente.

R/ 
Motion 101 describe el movimiento como la acumulación de vectores a lo largo del tiempo.

Un objeto tiene una posición, que cambia al sumarle un vector de velocidad, y esta a su vez puede cambiar al sumarle un vector de aceleración.

Geométricamente, el movimiento se interpreta como vectores encadenados:

cada frame la posición se desplaza en la dirección y magnitud de la velocidad, y la velocidad se modifica según la aceleración.

+ Cuál es el concepto del marco motion 101 y cómo se interpreta geométricamente.

R/ 
En el código, el objeto parte desde el centro con velocidad inicial cero.
Una aceleración constante hacia la izquierda y abajo se acumula en la velocidad en cada frame, aumentando su magnitud progresivamente.
La velocidad se limita con topSpeed, y luego se aplica a la posición, haciendo que el objeto caiga diagonalmente hasta alcanzar una velocidad máxima estable.

### Actividad 08

+ Cuál es el concepto del marco motion 101 y cómo se interpreta geométricamente.

R/ 

### Actividad 09

+ Describe el concepto de tu obra generativa. Explica el concepto de tu obra generativa, qué regla aplicaste para la aceleración y por qué, si fue una decisión de diseño, o qué te evoca, si fue una exploración artística.

R/ Es una obra generativa basada en muchas partículas que siguen a un punto en movimiento controlado por ruido Perlin. Ese punto nunca se mueve igual, así que el sistema está en cambio constante.

Cada partícula acelera hacia ese punto, pero también se aleja del mouse. La aceleración es la suma de ambas fuerzas más una pequeña variación aleatoria.

La intención fue explorar cómo reglas muy simples —seguir y evitar— pueden producir comportamientos colectivos interesantes. Me interesa observar cómo el sistema reacciona cuando el usuario interviene y altera el flujo.

```js
let followers = [];

function setup() {
  createCanvas(640, 640);
  mover = new Mover();

  for (let i = 0; i < 2000; i++) {
    followers.push(new Follower());
  }
}
  function keyPressed() {
  for (let i = 0; i < 200; i++) {
    let f = new Follower();
    
    
    followers.push(f);
  }
}
function draw() {
  background(0, 10);
  


  
  mover.update(frameCount * 0.05*noise(frameCount * 0.001));
  mover.show();

  for (let f of followers) {
    f.update(mover.position);
    f.checkEdges();
    f.show();
  }
}


// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    
  }

  update(t) {
  this.position.x = width * noise(t);
  this.position.y = height * noise(t + 100); // desplazamos para que no sea igual en x y y
}


  show() {
    noStroke();
    
    fill(0,255,0);
    circle(this.position.x, this.position.y, 48);
  }


}


class Follower {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector();
    this.acceleration = createVector();
    
    this.topSpeed = 10;
    this.maxForce = 0.3;
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  seek(target) {
    let desired = p5.Vector.sub(target, this.position);
    desired.normalize();
    desired.mult(this.topSpeed);

    let steer = p5.Vector.sub(desired, this.velocity);
    steer.limit(this.maxForce);

    return steer;
  }

  flee(target) {
    let desired = p5.Vector.sub(this.position, target);
    let d = desired.mag();

    if (d < 100) {
      desired.normalize();
      desired.mult(this.topSpeed);

      let steer = p5.Vector.sub(desired, this.velocity);
      steer.limit(this.maxForce * 2); 

      return steer;
    }

    return createVector(0, 0);
  }

  update(target) {

    // Reset aceleración cada frame
    this.acceleration.mult(0);

    let seekForce = this.seek(target);
    let fleeForce = this.flee(createVector(mouseX, mouseY));

    // Ponderación de fuerzas
    seekForce.mult(1);
    fleeForce.mult(2);

    this.applyForce(seekForce);
    this.applyForce(fleeForce);

    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
  }

  show() {
    noStroke();
    fill(255, 0, 0);
    circle(this.position.x, this.position.y, 2);
  }

  checkEdges() {
    if (this.position.x > width) this.position.x = 0;
    if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    if (this.position.y < 0) this.position.y = height;
  }
}

```
<img width="783" height="789" alt="image" src="https://github.com/user-attachments/assets/80ab66f0-673b-404c-8432-cb7a5c3cef58" />

https://editor.p5js.org/Nicofon1/sketches/b_EH8lPQa

## Bitácora de reflexión



### Actividad 10

+ Describe el concepto de tu obra generativa. Explica el concepto de tu obra generativa, qué regla aplicaste para la aceleración y por qué, si fue una decisión de diseño, o qué te evoca, si fue una exploración artística.

R/ Sistema de partículas basado en vectores y aceleración asimétrica. Las entidades interactúan según una matriz de atracción y repulsión por especies, generando cúmulos y persecuciones orgánicas. El rastro acumulado crea una textura visual inspirada en sedimentos biológicos. La obra busca mostrar cómo la ruptura de la simetría física produce comportamientos que simulan vida.

```js
let particles = [];
let numParticles = 300; // Ajustado para que el CPU no sufra (O(n^2))
let numSpecies = 3; 
let interactionMatrix = [];

function setup() {
  createCanvas(800, 800);
  
  // 1. Matriz de Ventrella: Define la "Personalidad" de las especies
  // interactionMatrix[A][B] = cómo se siente la especie A respecto a la B
  for (let i = 0; i < numSpecies; i++) {
    interactionMatrix[i] = [];
    for (let j = 0; j < numSpecies; j++) {
      // Valor positivo: atracción | Valor negativo: repulsión
      interactionMatrix[i][j] = random(-1, 1);
    }
  }

  // 2. Crear las partículas
  for (let i = 0; i < numParticles; i++) {
    let species = floor(random(numSpecies));
    particles.push(new Particle(species));
  }
  
  background(10); // Fondo oscuro estilo Tarbell
}

function draw() {
  // Estética Tarbell: rastro muy suave
  background(10, 15); 

  for (let p of particles) {
    p.applyInteractions(particles);
    p.update();
    p.checkEdges();
    p.show();
  }
}

class Particle {
  constructor(species) {
    this.species = species;
    this.position = createVector(random(width), random(height));
    this.velocity = p5.Vector.random2D();
    this.acceleration = createVector();
    
    this.topSpeed = 3;
    this.maxForce = 0.15;
    this.friction = 0.95; // Para que no se descontrolen (física orgánica)
    
    // Colores tipo Jared Tarbell (paleta desaturada y elegante)
    let colors = [
      color(255, 100, 50, 80),  // Especie 0
      color(100, 200, 255, 80), // Especie 1
      color(240, 240, 240, 80)  // Especie 2
    ];
    this.col = colors[this.species];
  }

  // Aquí está el corazón de "Clusters" de Ventrella
  applyInteractions(others) {
    let steering = createVector(0, 0);
    let count = 0;
    let perceptionRadius = 100; // Radio de visión

    for (let other of others) {
      if (other !== this) {
        let d = dist(this.position.x, this.position.y, other.position.x, other.position.y);
        
        if (d > 0 && d < perceptionRadius) {
          // 1. Calcular vector dirección (Ejemplo 1.10 Nature of Code)
          let force = p5.Vector.sub(other.position, this.position);
          force.normalize();
          
          // 2. Aplicar la ASIMETRÍA de Ventrella
          // Obtenemos el deseo (atracción/repulsión) de mi especie hacia la suya
          let strength = interactionMatrix[this.species][other.species];
          
          // Si d es muy pequeño, siempre hay una repulsión física para que no colapsen
          if (d < 20) {
            force.mult(-1.5); // Repulsión de contacto
          } else {
            force.mult(strength); // Atracción/repulsión social
          }
          
          steering.add(force);
          count++;
        }
      }
    }

    if (count > 0) {
      steering.div(count);
      steering.setMag(this.maxForce);
      this.acceleration.add(steering);
    }
  }

  update() {
    // Motion 101
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
    
    // Aplicar un poco de fricción para que el movimiento sea más "líquido"
    this.velocity.mult(this.friction);
    
    // Limpiar aceleración
    this.acceleration.mult(0);
  }

  show() {
    // Estética Jared Tarbell: 
    // En lugar de círculos, dibujamos una pequeña línea que indica dirección
    stroke(this.col);
    strokeWeight(1.2);
    let prevPos = p5.Vector.sub(this.position, p5.Vector.mult(this.velocity, 2));
    line(this.position.x, this.position.y, prevPos.x, prevPos.y);
  }

  checkEdges() {
    // Bordes infinitos (Toroidal)
    if (this.position.x > width) this.position.x = 0;
    if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    if (this.position.y < 0) this.position.y = height;
  }
}
```
<img width="813" height="762" alt="image" src="https://github.com/user-attachments/assets/94d3d6a3-e133-43bf-8492-29bb3ea245d2" />


[https://editor.p5js.org/Nicofon1/sketches/b_EH8lPQa](https://editor.p5js.org/Nicofon1/sketches/0tcdI2GHd)


