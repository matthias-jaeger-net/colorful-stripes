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
Along the the X-axis a number of curve shapes in random colors are created. Each time a 'virtual' midpoint is calculated and modified with perlin noise to render a 'fluid' looking piece. 

![colorstripes1](colorstripes1(16).jpg)
*An example that worked for me*

![colorstripes1](colorstripes1(4).jpg)
*An example that didn't work for me*

## Code with comments
```javascript
// No draw loop, single image out
function setup() {
  // Format: The original was a square image
  createCanvas(800, 400);  
  
  // Variables to play with:
  // - Initial distance between the lines
  const s = 8;
  // - Scales the thickness 
  const f = 0.85;
  // - Increment for the noise 
  const i = 0.001;
  
  // Currenet noise 
  let n = 0;
  
  // Hack: Loops larger than the view to avoid empty spots
  for (let x = -width; x < width + width; x += s) {
    // A midpoint with a noisy offset in x,y is calculated and added
    const mid = createVector(x, height * noise(n));
    const off = createVector(height * noise(n), 0);
    mid.add(off);
    
    // Make each shape in a random color from the list
    stroke(random(colors));
    // Prevent default white fill
    noFill();
    strokeWeight(random(f * s));
    
    // Draw the shape
    beginShape();
    // Control start
    curveVertex(x, 0);
    // Anchor start
    curveVertex(x, 0);
    // Curvy midpoint
    curveVertex(mid.x, mid.y);
    // Anchor end
    curveVertex(x, height);
    // Control end
    curveVertex(x, height);
    endShape();
    
    // Travel along the noise wave
    n += i;
  }
  
  // Done, save out
  save("colorstripes1.jpg");
}
