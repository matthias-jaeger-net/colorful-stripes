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
*An example that worked for me*

![colorstripes1](colorstripes1(4).jpg)
*An example that didn't work for me*

## Code with comments
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
```

# colorstripes 2
