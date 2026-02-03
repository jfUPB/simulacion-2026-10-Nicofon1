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

R/


+ El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?

R/


+ ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.

R/


+ ¿Para que te puede servir el método dist()?

R/


+ ¿Para qué sirven los métodos normalize() y limit()?

R/



## Bitácora de reflexión
