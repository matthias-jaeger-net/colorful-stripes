# colorful-stripes
An ongoing collection of my attempts to create a colorful minimalistic visual in p5 js. All examples create a striped pattern of various kinds. See the sketches and output images below for inspiration. I kept it short and simple, but some things might be complicated to understand. I try to clarify in the comments of each sketch when I think this is complicated or wired. 

### Dependencies
#### p5 
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.1.9/p5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.1.9/addons/p5.sound.min.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />

  </head>
  <body>
    <script src="colors.js"></script>
    <script src="sketch.js"></script>
  </body>
</html>
```

```javascript
// colors.js
// Used in all attempts - for readability excluded.
const colors = [ '#E55A2E', '#E5BC4B', '#FEED61', '#DAEC5E', '#3F864D', '#58B2B0', '#5B8FEB', '#3260B2', '#000000'];
```

# colorstripes 1

![colorstripes1](colorstripes1(16).jpg)

```javascript
// The curving 'midpoint' is modulated with noise
function setup() {
  createCanvas(800, 400);  
  
  const spacing = 8;
  const leftEdge = -width;
  const rightEdge = width + width;
  const reduction = 0.85;
  const noiseInc = 0.001;
  let currentNoise = 0;
  
  for (let x = leftEdge; x < rightEdge; x += spacing) {
    const curving = createVector(x, height * noise(currentNoise));
    const offsetx = createVector(width * noise(currentNoise), 0);
    curving.add(offsetx);
    
    noFill();
    stroke(random(colors));
    strokeWeight(random(spacing * reduction));
    
    beginShape();
    curveVertex(x, 0);
    curveVertex(x, 0);
    curveVertex(curving.x, curving.y);
    curveVertex(x, height);
    curveVertex(x, height);
    endShape();
    
    currentNoise += noiseInc;
  }
}
```

# colorstripes 2
![colorstripes1](colorstripes2(7).jpg)

```javascript
// Two curving 'midpoints' modulated with noise 
function setup() {
  createCanvas(800, 400);
  
  const spacing = 8;
  const leftEdge = -width;
  const rightEdge = width + width;
  const reduction = 0.55;
  const nInc = 0.001;
  const mInc = 0.01;
  let n = 0;
  let m = 0;

  for (let x = leftEdge; x < rightEdge; x += spacing) {
    const noiseA = createVector(x - noise(n) * width, 400 * noise(m));
    const noiseB = createVector(x - noise(m) * width, 800 * noise(n));
    
    stroke(random(colors));
    noFill();
    strokeWeight(random(spacing * reduction));
    
    beginShape();
    curveVertex(x, 0);
    curveVertex(x, -10);
    curveVertex(noiseA.x, noiseA.y);
    curveVertex(noiseB.x, noiseB.y);
    curveVertex(x, height);
    curveVertex(x, height);
    endShape();
    
    n += nInc;
    m += mInc;
  }

  save("colorstripes2.jpg");
}
```

# colorstripes 3

![colorstripes1](colorstripes3(13).jpg)


```javascript
// Curved shapes are modulated with random vectors 
function setup() {
 createCanvas(800, 400);
  background(0);
  noFill();

  const shape = [];
  for (let i = -10; i < 20; i++) {
    let x = i * (width / 10);
    shape.push(createVector(x, 0));
  }

  for (let i = 0; i < height; i++) {
    stroke(random(colors));
    strokeWeight(random(2));
    
    beginShape();
    for (let vector of shape) {
      curveVertex(vector.x, vector.y);
      const shift_x = random(-5, 5);
      const drops_y = random(0, 8);
      vector.add(createVector(shift_x, drops_y));
    }
    endShape();
  }
  save("colorstripes3.jpg");
}
```

# colorstripes 4

![colorstripes1](colorstripes4(106).jpg)


```javascript
// Curved shapes are modulated by a wave
function setup() {
  createCanvas(800, 800);
  noFill();
  background(0);
  const s = 5;
  const i = 0.01224439131597621;
  let d = 0;
  let n = 0;  
  let skew = 0.1;
  let blow = 10;
  for (let x = -width; x < width + width; x += s) {
    stroke(random(colors));
    strokeWeight(random(4))
    beginShape();
    for (let y = -s; y < height + s * 2; y += s) {
      const o = sin(n * d * cos(n*skew)) * s * blow;
      curveVertex(x - o, y);
      n += i;
    }
    n = 0;
    d += i;
    endShape();
  }
  save("colorstripes4.jpg");
}
```

# colorstripes 5

![colorstripes5](colorstripes5(1).png)

```javascript
// Curved lines respecting the distance to an attractor point
function setup() {
  createCanvas(800, 400);
  background(0);
  noFill();
  const points = [];
  const s = 8;
  let index = 0;
  for (let x = 0; x < width; x += s) {
    const col = random(colors);
    for (let y = 0; y < height; y++) {
      points.push({
        col: col,
        pos: createVector(x, y),
        index: index,
      });
      index++;
    }
  }
  
  const stregth = random(height * 0.5);
  const attractor = createVector(402, height*0.5-1);
  for (let v of points) {
    const a = v.pos.copy();
    const b = attractor;
    const d = a.sub(b).normalize().mult(stregth);
    v.pos.add(d);
  }

  for (let r = 0; r < stregth+s-0.3; r += s) {
    const a = attractor.copy();
    const b = p5.Vector.random2D().mult(random(3));
    a.add(b);    
    strokeWeight(random(2));
    stroke(random(colors));
    circle(a.x, a.y, r*2);  
  }
  
  index = 0;
  for (let x = 0; x < width; x += s) {
    strokeWeight(random(3));
    beginShape();
    for (let y = 0; y < height; y++) {
      const v = points[index];
      stroke(v.col)
      curveVertex(v.pos.x, v.pos.y);
      index++;
    }
    endShape();
  }
  save('colorstripes5');
}
```
