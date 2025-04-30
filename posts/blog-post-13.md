---
title: Shaders
published_at: 2025-04-14
snippet:
disable_html_sanitization: true
allow_math: true
---

# Importing Shaders in p5.js

This was just my attempt at making sure it actually showed up on the canvas using the teachers example!

<canvas id="p5_canvas1"></canvas>

# Implementing My Own Simple Shader

<canvas id="p5_canvas2"></canvas>

<script type="module">
  import p5 from 'https://cdn.jsdelivr.net/npm/p5@1.11.3/+esm'

  // --- First Sketch: Teacher's Shader ---
  const cnv1 = document.getElementById('p5_canvas1')

  const sketch1 = p => {
    let theShader

    p.preload = () => {
      const vertexShader = `
        attribute vec3 aPosition;
        attribute vec2 aTexCoord;
        varying vec2 vTexCoord;

        void main() {
          vTexCoord = aTexCoord;
          vec4 positionVec4 = vec4(aPosition, 1.0);
          positionVec4.xy = positionVec4.xy * 2.0 - 1.0;
          gl_Position = positionVec4;
        }
      `

      const fragmentShader = `
        precision mediump float;
        varying vec2 vTexCoord;
        uniform vec2 u_resolution;
        uniform float u_time;
        uniform vec2 u_mouse;

        float circle(vec2 st, float radius, vec2 center) {
          vec2 dist = st - center;
          return 1.0 - smoothstep(
            radius - 0.01,
            radius + 0.01,
            dot(dist, dist) * 4.0
          );
        }

        void main() {
          vec2 st = vTexCoord;
          
          vec3 bg = vec3(st.x, st.y, 0.5);
          
          float mouseBall = circle(st, 0.1, u_mouse);
          vec3 mouseBallColor = vec3(1.0, 0.2, 0.6);
          
          float t = u_time * 0.5;
          float pulse = sin(t) * 0.5 + 0.5;
          float circle1 = circle(st, 0.2 * pulse, vec2(0.3, 0.3));
          float circle2 = circle(st, 0.1 * (1.0 - pulse), vec2(0.7, 0.7));
          
          vec3 color = bg;
          color = mix(color, vec3(0.0, 0.8, 0.8), circle1);
          color = mix(color, vec3(1.0, 0.8, 0.0), circle2);
          color = mix(color, mouseBallColor, mouseBall);
          
          gl_FragColor = vec4(color, 1.0);
        }
      `
      
      theShader = p.createShader(vertexShader, fragmentShader)
    }

    p.setup = () => {
      const w = cnv1.parentNode.scrollWidth
      const h = w * 9 / 16
      p.createCanvas(w, h, p.WEBGL, cnv1)
      p.noStroke()
    }

    p.draw = () => {
      theShader.setUniform('u_resolution', [p.width, p.height])
      theShader.setUniform('u_time', p.millis() * 0.001)
      theShader.setUniform('u_mouse', [
        p.mouseX / p.width,
        1.0 - p.mouseY / p.height
      ])
      p.shader(theShader)
      p.rect(0, 0, p.width, p.height)
    }
  }

  new p5(sketch1)

  // --- Second Sketch: Your Own Simple Shader ---
  const cnv2 = document.getElementById('p5_canvas2')

  const sketch2 = p => {
    let theShader

    p.preload = () => {
      const vertexShader = `
        attribute vec3 aPosition;
        attribute vec2 aTexCoord;
        varying vec2 vTexCoord;

        void main() {
          vTexCoord = aTexCoord;
          vec4 positionVec4 = vec4(aPosition, 1.0);
          positionVec4.xy = positionVec4.xy * 2.0 - 1.0;
          gl_Position = positionVec4;
        }
      `

      const fragmentShader = `
        precision mediump float;
        varying vec2 vTexCoord;

        void main() {
          vec2 st = vTexCoord;
          vec3 color = mix(vec3(1.0, 0.0, 0.0), vec3(1.0, 1.0, 1.0), st.x);
          gl_FragColor = vec4(color, 1.0);
        }
      `
      
      theShader = p.createShader(vertexShader, fragmentShader)
    }

    p.setup = () => {
      const w = cnv2.parentNode.scrollWidth
      const h = w * 9 / 16
      p.createCanvas(w, h, p.WEBGL, cnv2)
      p.noStroke()
    }

    p.draw = () => {
      p.shader(theShader)
      p.rect(0, 0, p.width, p.height)
    }
  }

  new p5(sketch2)

</script>

<style>
  #p5_canvas1, #p5_canvas2 {
    width: 100%;
    height: auto;
    display: block;
    margin-bottom: 2rem;
  }
</style>

# What Is it Like to Be A Fungus by Merlin Sheldrake

### Three Passages That Speak to Me

> The soil was a horizonless external gut—digestion and salvage everywhere—flocks of bacteria surfing on waves ofelectrical charge—chemical weather systems—subterranean highways—slimy infective embrace—seething intimate contact on all sides.

This passage describes the fungul world as something that is wild, chaotic, alive and interconnected in every possible way. It matches the idea of chaos that I want to explore visually and sonically, capturing the fluid, uncontrollable nature. It inspires me to create visuals that grow, glitch and overlap, where interactions are dense and unpredictable, similar to fungul networks in real life.

> They are eating rock, making soil, digesting pollutants, nourishing and killing plants, surviving in space inducing visions, producing food, making medicines, manipulating animal behavior, and influencing the composition of the Earth’s atmosphere.

This passage shows how fungi are not passive organisms, they actively reshape the world in powerful ways. It shows the scale and versatility and highlights how fungi are world builders as they create new systems and collapse old ones. It influences me to make my assignment something that actively alters its environment, not just something that grows.

> We are ecosystems that span boundaries and transgress categories. Our selves emerge from a complex tangle of relationships only now becoming known.

This challenges the idea of a fixed and self-contained identity. It describes life as something dynamic and collective, showing boundaries are constantly shifting and blending. It suggests that what we are is always somewhat unknown, and there is hidden complexity inside everything that we can never really fully see or control. This inspires me to create my assignment as something that constantly makes new identities or structures that appear based on things like interaction or recursion.

# Rough Draft for Assignment 2

This is the JavaScript for my first draft! It uses the p5.js library which I imported in the HTML section. I like where this is headed but also it feels too simple, and not chaotic enough. I inserted it in p5.js for the sake of being able to see the drafts in the blog, but I did make it on visual studio code!

<iframe id="A1.1" src="https://editor.p5js.org/yeahlia/sketches/GQXJC0yFU"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A1.1`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

```js
let growingBranches = []; // array of all growing branches
let mainPointX, mainPointY; // holds the coordinates of the centre where the branches will start growing

// SETUP ----------------------------------------------------------------------------------------------------
function setup() {
  createCanvas(windowWidth, windowHeight); // creates canvas the size on the window
  background("black"); // black background
  stroke("white"); // white lines
  strokeWeight(2); // thickness of the lines

  mainPointX = width / 2; // sets the main point middle of the total width
  mainPointY = height / 2; // sets the main point middle of the total height

  for (let i = 0; i < 5; i++) {
    // starts the loop with 5 branches
    let startAngle = random(TWO_PI); // chooses a random angle of an entire circle
    // creates new branch with a maximum of 8 generations and pushes it to the growingBranches array
    growingBranches.push(new Branch(mainPointX, mainPointY, startAngle, 8));
  }
}

// DRAW -----------------------------------------------------------------------------------------------------
function draw() {
  // if there is zero values in growingBranches array:
  if (growingBranches.length === 0) {
    // creates a new branch with a random angle and a depth of 6
    growingBranches.push(new Branch(mainPointX, mainPointY, random(TWO_PI), 6));
  }

  // loops through the growingBranches array
  for (let i = growingBranches.length - 1; i >= 0; i--) {
    growingBranches[i].update(); // runs the update function
    growingBranches[i].show(); // runs the show function

    // if branch is finished growing:
    if (growingBranches[i].finished) {
      let finishedBranch = growingBranches[i]; // saves the finished branch into a temporary variable
      growingBranches.splice(i, 1); // removes it after saving (otherwise will keep growing forever)

      const numChildren = int(random(2, 3)); // spawns either 2 or 3 children branches

      // loops depending on the the number of children branches
      for (let j = 0; j < numChildren; j++) {
        // picks a new angle for the child branches within 45 degrees of the parent branch direction
        const newAngle = finishedBranch.angle + random(-PI / 4, PI / 4);
        const newDepth = max(0, finishedBranch.depth - 1); // decreases depth

        // only creates child if depth is above 0 + a random 10% chance of continuation
        if (newDepth > 0 || random() < 0.1) {
          // push to growingBranches array
          growingBranches.push(
            new Branch( // starts building branch
              // x coordinate for new branch
              finishedBranch.x + // starts from parent branch's x coordinate
                // calculates the x direction and makes it the full length
                cos(finishedBranch.angle) * finishedBranch.targetLen,
              finishedBranch.y + // starts from parent branch's y coordinate
                // calculates the y direction and makes it the full length
                sin(finishedBranch.angle) * finishedBranch.targetLen,
              newAngle, // direction the new branch will grow
              newDepth //depth value (which slowly shrinks over generations)
            )
          );
        }
      }
    }
  }
}

// --- BRANCH CLASS -----------------------------------------------------------------------------------------
// defines the Branch class
class Branch {
  // the necesssary information
  constructor(x, y, angle, depth) {
    this.x = x; // starting property of x position
    this.y = y; // starting property of y position
    this.angle = angle; // starting property of angle
    this.depth = depth; // starting property of depth
    this.len = 0; // starts the branch with 0 length
    this.targetLen = depth * 10 + 10; // sets length so the depth lowers every generation
    this.finished = false; // makes sure it doesn't finish when it is first created
    this.speed = 0.5; // speed of growth

    this.lifetime = 300; // each branch lives fofr 300 frames
  }

  // update logic
  update() {
    // if branch hasn't fully grown:
    if (this.len < this.targetLen) {
      this.len += this.speed; // keeps growing
      this.lifetime--; // reduces lifetime by 1 each frame

      // if lifetime hits 0
      if (this.lifetime <= 0) {
        this.finished = true; // branch dies
        return;
      }
    } else {
      this.finished = true; // branch dies
    }
  }

  // show logic
  show() {
    push(); // saves current canvas settings?
    translate(this.x, this.y); // move origin to branch starting point
    rotate(this.angle); // rotates canvas by branch angle
    line(0, 0, this.len, 0); // draws line
    pop(); // restores previous canvas settings
  }
}
```

## How Well Does My Rough Draft:

### Responds to 'What is it Like to be a Fungus' by Merlin Sheldrake

Sheldrake describes fungi as nonlinear, branching and constantly decaying, growing and adapting. My code simulates something similar, with branches starting from a point and branching out, grows randomly and dies.

### As an Example of Post Digital (Why/Why Not)

This draft embraces an imperfect mess and unpredictablility. It engages with ideas of growth and decay, blending technical techniques with fungi, something with natural biological systems. It questions control and questions the idea of digital systems needing to be orderly.

### Functioning in a Chaotic Aesthetic Register

This functions inside a chaotic aesthetic register as it is inbetween randomness and structure, which is a key component of effective complexity. In my work, the growth patterns are random, branches are always growing outwards and the angle is chosen randomly. But, it has structure as it has a lifetime so it doesn't get too chaotic that it becomes a mess.

### How Will This Inform the Next Stage of Assignment 2

I want the to continue with this idea, but I definitely think that its current state isn't chaotic enough. I want to have a deeper simulation of fungul behaviors, maybe branches influencing each other's growth or decay, but I'm not 100% sure on how to do it. Maybe that when a branch dies randomly, it glitches the parent branch and causes the rest to slowly stop growing? Maybe has pixel drag/glitch effect? Maybe also add spontaneous deaths!

I also want to use shaders for the background to make a cool background, but also use shaders maybe to like visualize the branch growing. Like the color slowing fading as it gets further from the middle node.

I also want to avoid using the lifetime thing to kill branches as it seems random and disruptive. I want to deal with it maybe either by making the children branches to get smaller at a random pace (so not everything is the same) or code something that scans if theres about to be an overlap, and goes a different direction, and if its surrounded, it dies. This will prevent things looking too 'muddy'. For when it dies, I was thinking of adding a glitch effect somehow, maybe through color or jittering, and the branch retracts 3 generations before trying to continue to grow again

To add interactivity, my idea is to add a function where the user can click on the canvas, which will set a node, and then branches will form from that point. It will be a different color and will completely ignore the branches for the other nodes, so it kind of looks like layers of different systems.
