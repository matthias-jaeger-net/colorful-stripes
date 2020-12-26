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
Along the the X-axis a number of curve shapes in random colors are created. Each time a 'virtual' midpoint is calculated and modified with perlin noise to render a 'fluid' looking piece. The original was a square image in these sketches I used a landscape format.

![colorstripes1](colorstripes1(16).jpg)
*An example that worked for me*

![colorstripes1](colorstripes1(4).jpg)
*An example that didn't work for me*

## Code
```javascript
function setup() {
  createCanvas(800, 400);  

  // Initial distance between the lines
  const s = 8;
  // Scales the thickness 
  const f = 0.85;
  // Increment for the noise 
  const i = 0.001;
  // Currenet noise 
  let n = 0;

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
  save("colorstripes1.jpg");
}
