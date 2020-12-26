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

![colorstripes1](colorstripes1(16).jpg)

```javascript
function setup() {

  // Format
  createCanvas(800, 400);  
  
  // Distance between the lines
  const s = 8;
  
  // Scales the thickness 
  const f = 0.85;
  
  // Increment for the noise 
  const i = 0.001;
  
  // Current noise 
  let n = 0;
  
  // Hack: Loops larger than the view to avoid empty spots
  for (let x = -width; x < width + width; x += s) {

    // A point on a 'virtual line' from top to bottom 
    const mid = createVector(x, height * noise(n));
    
    // Another noisy offset vector to shift left and right
    const off = createVector(width * noise(n), 0);
    
    // Add the offset
    mid.add(off);
    
    // Make each shape in a random color from the list
    stroke(random(colors));
    
    // Prevent default white fill
    noFill();
    
    // A random value, smaller than the distance betweeen curves
    strokeWeight(random(f * s));
    
    // Draw the shape
    beginShape();
    curveVertex(x, 0);          // Control start
    curveVertex(x, 0);          // Anchor start
    curveVertex(mid.x, mid.y);  // Curvy midpoint
    curveVertex(x, height);     // Anchor end
    curveVertex(x, height);     // Control end
    endShape();
    
    // Travel along the noise wave
    n += i;
  }
  
  // Done, save out
  save("colorstripes1.jpg");
}
```

# colorstripes 2
![colorstripes1](colorstripes2(7).jpg)

```javascript
function setup() {
  
  const s = 8
  const f = 0.55;
  const i = 0.001;
  const j = 0.01;
  let n = 0;
  let m = 0;
  createCanvas(800, 400);
  stroke(random(colors));
  for (let x = -width; x < width + width; x += s) {
    const a = createVector(x - noise(n) * width, 400 * noise(m));
    const b = createVector(x - noise(m) * width, 800 * noise(n));
    stroke(random(colors));
    noFill();
    strokeWeight(random(f * s));
    beginShape();
    curveVertex(x, 0);
    curveVertex(x, -10);
    curveVertex(a.x, a.y);
    curveVertex(b.x, b.y);
    curveVertex(x, height);
    curveVertex(x, height);
    endShape();
    n += i;
    m += j;
  }
  
  save("colorstripes2.jpg");
}
```

# colorstripes 3

![colorstripes1](colorstripes3(13).jpg)


```javascript
function setup() {

  // Format
  createCanvas(800, 400);
  
  // Black background
  background(0);
  
  // Prevent default fill
  noFill();
  
  // Points on a 'line' on top, from left to right
  const shape = [];
  
  // Construct the points 
  for (let i = -10; i < 20; i++) {
    
    // Very hacky
    let x = i * (width / 10);
    
    // Something for x and 0 for y
    shape.push(createVector(x, 0));
  }
  
  // Loops from top to bottom 
  for (let i = 0; i < height; i++) {
    // Random color from the list
    stroke(random(colors));
    
    // Random thickness
    strokeWeight(random(2));
    
    // Draw the shape
    beginShape();
    for (let vector of shape) {
      
      // Add the vertex to the shape
      curveVertex(vector.x, vector.y);
      
      // Then modify the vertext in the list
      // These numbers greatly affect the outcome...
      const shift_x = random(-5, 5);
      const drops_y = random(0, 8);
      
      // Add the modifictation 
      vector.add(createVector(shift_x, drops_y));
    }
    endShape();
    
  }
  
  // Done, save out
  save("colorstripes3.jpg");
}
```
# colorstripes 4

![colorstripes1](colorstripes4(13).jpg)


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
