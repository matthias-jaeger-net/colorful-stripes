# colorful-stripes
A collection of a few attempts to create a colorful minimalistic visual in p5 js


```javascript
// Used in all attempts
const colors = [
  '#E55A2E', '#E5BC4B', '#FEED61', '#DAEC5E', '#3F864D',
  '#58B2B0', '#5B8FEB', '#3260B2', '#000000'
];
```

# colorstripes 1

![colorstripes1](colorstripes1(16).jpg)

```javascript
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
