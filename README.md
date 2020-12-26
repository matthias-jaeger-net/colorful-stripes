# colorful-stripes
A collection of a few attempts to create a colorful minimalistic visual in p5 js

## Colors
```javascript
// Used in all examples
const colors = [
  '#E55A2E', 
  '#E5BC4B', 
  '#FEED61', 
  '#DAEC5E', 
  '#3F864D',
  '#58B2B0', 
  '#5B8FEB', 
  '#3260B2', 
  '#000000'
];
```

# colorstripes 1
![colorstripes1](colorstripes1.jpg)

```javascript
function setup() {
  const s = 8;
  const f = 0.85;
  const i = 0.001;
  let n = 0;
  createCanvas(800, 800);
  stroke(random(colors));
  for (let x = -width; x < width + width; x += s) {
    const mid = createVector(x, height * noise(n));
    const off = createVector(height * noise(n), 0);
    mid.add(off);
    stroke(random(colors));
    noFill();
    strokeWeight(random(f * s));
    beginShape();
    curveVertex(x, 0);
    curveVertex(x, 0);
    curveVertex(mid.x, mid.y);
    curveVertex(x, height);
    curveVertex(x, height);
    endShape();
    n += i;
  }
  save("colorstripes.jpg");
}
