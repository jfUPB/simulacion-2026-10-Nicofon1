# Unidad 1

## Bitácora de proceso de aprendizaje

### Actividad 01

+ Piensa y describe en una sola frase y en tus propias palabras cómo la aleatoriedad influye en el arte generativo.
R/ La aleatoriedad en el arte generativo básicamente evita que todo sea rígido y repetitivo, metiendo variaciones inesperadas que hacen que cada resultado salga distinto sin que el sistema se vuelva caótico.


### Actividad 02

+ Modifica el código del ejemplo Example 0.1: A Traditional Random Walk.
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
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    noStroke();
    fill(color(random(255), random(255), random(255)));
    circle(this.x, this.y,7);
  }
  
  

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x=this.x+5;
    } else if (choice == 1) {
      this.x=this.x-5;
    } else if (choice == 2) {
      this.y=this.y+5;
    } else {
      this.y=this.y-5;
    }
  }
}

```

+ Antes de ejecutar el código, escribe en tu bitácora qué esperas que suceda.

R/ que depasos más grandes, de igual manera, puntos mas grandes y que los puntos sean de colores aleatoreos.

+ Ejecuta el código y escribe en tu bitácora qué sucedió realmente.

R/ dió depasos más grandes, de igual manera, puntos mas grandes y los puntos son de colores aleatoreos.

+ Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?

R/ si, porque pense en lo que queria que pasara antes de hacer el codigo.

### Actividad 03

+ En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.

R/ En una distribución uniforme todas las posibilodades tendran la misma probabilidad de salis, mientras que en una no unniforme habran posibilidades con mas probabilidad que otras

+ Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.

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
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    noStroke();
    fill(color(random(255), random(255), random(255)));
    circle(this.x, this.y,7);
  }
  
  

  step() {
    const choice = floor(random(5));
    if (choice == 0||choice == 4) {
      this.x=this.x+5;
    } else if (choice == 1) {
      this.x=this.x-5;
    } else if (choice == 2) {
      this.y=this.y+5;
    } else {
      this.y=this.y-5;
    }
  }
}

```

### Actividad 04

+ Crea un nuevo sketch en p5.js que represente una distribución normal.

R/ 
```js
let sizes = [];

function setup() {
  createCanvas(800, 600);
  background(220);

  for (let i = 0; i < 11; i++) {
    sizes[i] = 5;
  }

}

function draw() {
  background(220);
  noStroke();
  fill(0, 40);

  let y = height / 2;
  sizes[floor(randomGaussian(5, 2))]++;

  for (let i = 0; i < 11; i++) {

    let x = (i + 1) * 60;
    circle(x, y, sizes[i]);
  }
}

```

https://editor.p5js.org/Nicofon1/sketches/-eHHCTw5U

<img width="647" height="240" alt="image" src="https://github.com/user-attachments/assets/85eedd56-d5c4-41d1-8e88-9091fef09ee0" />


### Actividad 05

+ Crea un nuevo sketch en p5.js donde modifiques uno de los ejemplos anteriores y adiciones de Lévy flight.

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
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    noStroke();
    fill(color(random(255), random(255), random(255)));
    circle(this.x, this.y,7);
  }
  
  

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x=this.x+5;
    } else if (choice == 1) {
      this.x=this.x-5;
    } else if (choice == 2) {
      this.y=this.y+5;
    } else {
      this.y=this.y-5;
    }
    
    if(floor(random(20))==2)
      if (choice == 0) {
        this.x=this.x+25;
      } else if (choice == 1) {
        this.x=this.x-25;
      } else if (choice == 2) {
        this.y=this.y+25;
      } else {
        this.y=this.y-25;
      }
  }
}

```

+ Explica por qué usaste esta técnica y qué resultados esperabas obtener.

R/ puse que con una probabilidade de 1/20 el punto le adicionara 25px a su salto y esperava ver pequeños recorridos  con largos espacios en medio

<img width="587" height="405" alt="image" src="https://github.com/user-attachments/assets/526ca2bf-1552-422d-afc3-487ec66c08ee" />

https://editor.p5js.org/Nicofon1/sketches/BZio1KE1f

### Actividad 06

+ Crea un nuevo sketch en p5.js donde los visualices.

R/
```js
let t=0;
function setup() {
  createCanvas(400, 400);
  background(220);
  
}

function draw() {
  t+=0.01;
  noStroke();
  fill(color(random(255), random(255), random(255)));
  circle(noise(t)*400, noise(t+2)*400,7);
}
```

+ Explica el concepto qué resultados esberabas obtener.

R/ espero una esfera mulricolor dejando rastro por todo el camino que va recorriendo.

<img width="361" height="359" alt="image" src="https://github.com/user-attachments/assets/08019aef-6016-41da-800d-2c254919ea63" />

https://editor.p5js.org/Nicofon1/sketches/9miwcLNzu



## Bitácora de aplicación 

### Actividad 07

+ Un texto donde expliques el concepto de obra generativa.

R/ Esta obra es un experimento visual sobre la acumulación y el movimiento. La imagen se construye a partir de sus propios estados anteriores, que se reescalan y permanecen en pantalla, generando una sensación de profundidad y expansión continua. Un punto en rotación traza líneas hacia el centro, creando un ritmo constante, mientras pequeñas partículas aparecen de forma aleatoria, aportando variación y textura. El resultado es una composición en cambio permanente, donde el trazo, el color y el tiempo se superponen sin borrarse.

```js
t=0;
angle=0;
radio = 100;


function setup() {
  createCanvas(400, 400);
  background(220);
  
}

function draw() {
  let img = get();
  push();
  imageMode(CENTER);
  translate(width/2,height/2)
  scale(1.01);
  
  image(img,0,0);
  pop();
  t+=0.02;
  angle+=0.04;
  
    radio=abs(width/2-mouseX)
  let posC = rotatingPoint(angle,radio)
  
  stroke(color(floor(noise(t+2)*250), floor(noise(t)*250), floor(noise(t+6)*250)));
  strokeWeight(5);
  line(posC.x,posC.y,width/2,height/2);
  
  
  noStroke();
  fill(color(random(255), random(255), random(255)));
  circle(randomGaussian(200, 20),randomGaussian(200, 20),5);
  circle(randomGaussian(200, 40),randomGaussian(200, 40),3);
}
function rotatingPoint(a,r){
  return{
    x : width/2+cos(a)*r,
    y : height/2+sin(a)*r
    
}
}
```


<img width="357" height="363" alt="image" src="https://github.com/user-attachments/assets/bd4b5dea-2b68-460e-85ae-06e17813cb92" />

https://editor.p5js.org/Nicofon1/sketches/73jvq-DcX

## Bitácora de reflexión


