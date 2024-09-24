# ziwu0874_9103_tut5

Week8 Quiz

# Imaging Technique Inspiration

These images are interstellar footage from the Guardians of the Galaxy movies and are a rich source of inspiration for random animation.

![An image of Guardians of the Galaxy](https://cdn2.parksmedia.wdprapps.disney.com/media/youth/blog/the-science-behind-the-magic--guardians-of/BlogImage2.png)

![An image of Guardians of the Galaxy](https://cdnb.artstation.com/p/assets/images/images/045/581/069/large/martin-sabran-msabran-eidos-gog-concept-early-arrivingquarantinezone-fp-v02-0.jpg?1643064789)

## Incorporating Aspects of the Example Code into the Next Project

I wish I can incorporate the **noise-based particle movement** from the example code into the next phase of my project. This feature allows particles to move in a natural, fluid manner, which could be useful for visualizing data flows, user movement patterns, or dynamic interactions within a sci-fi or futuristic interface. 

## Why This is a Beneficial Technique

- Organic, Realistic Movement
The `noise()` function introduces randomness that simulates more natural, fluid motion, making it ideal for representing real-time environmental changes, crowd flows, or energy streams in a visualized system. This aligns well with sci-fi themes, which often feature fluid, dynamic movements.

- Continuous Visual Experience
The `checkEdges()` function ensures particles continually move on the screen, creating a seamless visual experience. This could be applied in projects that require continuous real-time data visualizations, such as a hybrid event app where data constantly flows across the screen.


# Coding Technique Exploration

```

var num = 2222;
var noiseScale=100, noiseStrength=1;
var particles = [num];

function setup() {
	describe('purple sand particles mimicking water flow')
  createCanvas(windowWidth, windowHeight);
  noStroke();
  for (let i=0; i<num; i++) {
    var loc = createVector(random(width*1.2), random(height), 2);
    var angle = 0; //any value to initialize
    var dir = createVector(cos(angle), sin(angle));
    // var speed = random(0.5,2);
    var speed = random(5,map(mouseX,0,width,5,20));   // faster
    particles[i]= new Particle(loc, dir, speed);
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
function draw() {
  // background(0);
  fill(0, 10);
  rect(0, 0, width, height);
  for (let i=0; i<particles.length; i++) {
    particles[i].run();
  }
}

class Particle{
  constructor(_loc,_dir,_speed){
    this.loc = _loc;
    this.dir = _dir;
    this.speed = _speed;
  	// var col;
  }
  run() {
    this.move();
    this.checkEdges();
    this.update();
  }
  move(){
    let angle=noise(this.loc.x/noiseScale, this.loc.y/noiseScale, frameCount/noiseScale)*TWO_PI*noiseStrength; //0-2PI
    this.dir.x = sin(angle);
    this.dir.y = tan(angle);
    var vel = this.dir.copy();
    var d = 22;  //direction change 
    vel.mult(this.speed*d); //vel = vel * (speed*d)
    this.loc.add(vel); //loc = loc + vel
  }
  checkEdges(){

    if (this.loc.x<0 || this.loc.x>width || this.loc.y<0 || this.loc.y>height) {    
      this.loc.x = random(width*10);
      this.loc.y = random(height);
    }
  }
  update(){
    fill(255,200,255);
    ellipse(this.loc.x, this.loc.y, this.loc.z);
  }
}
```

[Existing Code Online](https://p5js.org/sketches/2211359/)

## Discuss How This Coding Technique Might Help Achieve or Contribute to the Desired Effect

- Flow
The noise() function generates random, smooth movement in particles that mimic natural, organic flows. The noise-based direction changes give each particle a unique movement, helping to simulate a living system.

- Continuous Movement and Boundaries
The checkEdges() function ensures that particles reset when they move out of bounds, creating a continuous, seamless particle flow. This mirrors the unbroken movement in space scenes, where particles and energy seem to drift endlessly.

- Visual Consistency
The rendering of particles as ellipses using ellipse() combined with color and opacity adjustments (fill(255, 200, 255)) allows for smooth transitions and a glowing, ethereal effect. This matches the glowing particle and light effects seen in the inspiration images.


