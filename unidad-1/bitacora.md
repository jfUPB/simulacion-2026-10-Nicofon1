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

## Bitácora de aplicación 



## Bitácora de reflexión
