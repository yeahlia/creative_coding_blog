---
title: Creating Assignment 2
published_at: 2025-04-30
snippet:
disable_html_sanitization: true
allow_math: true
---

# Assignment 2 Draft 1

This is the creation of my assignment over time! Just in more detail I guess...

So you already saw my first draft a few posts ago but here it is again:

 <iframe id="A2.1" src="https://editor.p5js.org/yeahlia/sketches/GQXJC0yFU"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A2.1`)
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

I intended to make it very slow at first, just so I can see what was happening and once I was happy with it, I could speed things up or make things more dramatic and more 'chaotic'. I defintely wasn't happy with this though, it felt like everything was just spawning in a circle because all the branches had the same generation, and there was no variation, it's just messy. It felt very structured because everything was growing at the same space so I wanted some variation. I also wasn't a big fan that when it finished growing, it just started a new branch, it isn't what happens in real life, as everything is constantly changing and adapting, especially in the explanation in the essay.

I had some ideas which I implemented in the next draft.

# Assignment 2 Draft 2

This was my second variation! I still wasn't able to make it feel as alive as I wanted, but I was able to add some variation in terms of stroke, chance to spawn new branches, the length, etc.

 <iframe id="A2.2" src="https://editor.p5js.org/yeahlia/sketches/KQwlyV52g"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A2.2`)
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

  // starts the loop with 10 branches
  for (let i = 0; i < 10; i++) {
    let startAngle = random(TWO_PI); // chooses a random angle of an entire circle
    // creates new branch with a maximum of 8 generations and pushes it to the growingBranches array
    growingBranches.push(new Branch(mainPointX, mainPointY, startAngle, 8));
  }
}

// DRAW -----------------------------------------------------------------------------------------------------
function draw() {
  // if there is zero values in growingBranches array:
  // if (growingBranches.length === 0) {
  //   // creates a new branch with a random angle and a depth of 6
  //   growingBranches.push(new Branch(mainPointX, mainPointY, random(TWO_PI), 6));
  // }

  // background(black);

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
        // picks a new angle for the child branches
        const newAngle = finishedBranch.angle + random(-PI / 4, PI / 4);
        const newDepth = max(0, finishedBranch.depth - 1); // decreases depth

        const spawnChance = map(finishedBranch.depth, 1, 8, 0.2, 1.0); // less likely for deeper generations

        // only creates child if depth is above 0 + random chance
        if (newDepth > 0 && random() < spawnChance) {
          // push to growingBranches array
          growingBranches.push(
            new Branch( // starts building branch
              // x coordinate for new branch
              finishedBranch.x + // starts from parent branch's x coordinate
                // calculates the x direction and makes it the actual final point
                cos(finishedBranch.angle) * finishedBranch.len,
              finishedBranch.y + // starts from parent branch's y coordinate
                // calculates the y direction and makes it the actual final point
                sin(finishedBranch.angle) * finishedBranch.len,
              newAngle, // direction the new branch will grow
              newDepth // depth value (which slowly shrinks over generations)
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

    let minLen = max(10, depth * 5 + 10); // makes sure branches aren't short
    let maxLen = depth * 20 + 20; // max length it can grow
    this.targetLen = random(minLen, maxLen); // sets the length within that range

    this.finished = false; // makes sure it doesn't finish when it is first created
    this.speed = random(0.3, 0.7); // random speed of growth between 0.3 and 0.7

    this.lifetime = 200 + depth * 20; // each branch lives longer based on its depth
  }

  // update logic
  update() {
    // skip this branch completely if it's too short
    if (this.targetLen < 15) {
      this.finished = true;
      return;
    }

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
    if (this.targetLen < 15) return; // skip drawing if branch is too short

    // stroke transparency fades with depth; thickness thins with depth
    stroke(255, map(this.depth, 0, 8, 30, 255)); // lighter in later generations
    strokeWeight(map(this.depth, 0, 8, 0.5, 2)); // thinner in later generations

    push(); // saves current canvas settings?
    translate(this.x, this.y); // move origin to branch starting point
    rotate(this.angle); // rotates canvas by branch angle
    line(0, 0, this.len, 0); // draws line
    pop(); // restores previous canvas settings
  }
}
```

Though I still had some issues because it was just static. I had this idea to make branches like "glitch" backwards, like they are decaying, and then it can regrow back so it simulates an actual system, with parts moving forever. I really liked that idea but I had no idea what to do so I asked for the teachers help which was huge in rethinking everything.

I had to redo the entire code basically and make sure that each branch stores the end point, which then has the value of the child branch which starts at the end point of its parent. Kind of hard to explain but it makes sense in my head and I did get it to work after countless hours crazyness and crying to my mother (not really but I was really close) and begging ChatGPT to explain why my code didn't work even though it made sense to me!

# Assignment 2 Draft 3

 <iframe id="A2.3" src="https://editor.p5js.org/yeahlia/sketches/AXox0GF0X"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A2.3`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

```js
let rootBranches = []; // stores the 10 original branches

// SETUP ----------------------------------------------------------------------------------------------------

function setup() {
  createCanvas(windowWidth, windowHeight); // makes the canvas fit the browser window
  stroke("white"); // sets stroke color to white
  strokeWeight(2); // base stroke weight

  let centreX = width / 2; // centre horizontal
  let centreY = height / 2; // centre vertical

  // loop to make 10 starting branches
  for (let i = 0; i < 10; i++) {
    let startAngle = random(TWO_PI); // picks a random angle
    let startLength = random(40, 80); // picks a random length
    // creates a new branch and adds it to rootBranches array
    rootBranches.push(
      // creates new branch starting from centre, random angle and length and the generation
      new Branch({ x: centreX, y: centreY }, startAngle, startLength, 8, null)
    );
  }
}

// DRAW -----------------------------------------------------------------------------------------------------

function draw() {
  background(0); // draws background and refreshes frames

  // loop through all root branches and update and draw them
  for (let b of rootBranches) {
    b.update(); // update growth or glitch
    b.show(); // draw the branch
  }
}

// BRANCH CLASS ---------------------------------------------------------------------------------------------

class Branch {
  // constructor for making a new branch
  constructor(start, angle, targetLen, generation, parent) {
    this.start = { x: start.x, y: start.y }; // sets the start position of the branch
    this.end = { x: start.x, y: start.y }; // end starts at same point, will grow over time
    this.angle = angle; // direction
    this.targetLen = targetLen; // max length this branch will grow to
    this.generation = generation; // generation number

    this.len = 0; // how much it has currently grown
    this.speed = random(0.3, 0.7); // how fast it grows
    this.shrinkSpeed = random(0.5, 1.2); // how fast it shrinks if glitching

    this.finished = false; // true when branch stops growing or glitching
    this.childrenBranch = false; // tracks if children have been created already
    this.branches = []; // array to store child branches

    this.glitching = false; // true when branch is shrinking
  }

  // update logic
  update() {
    // if length is too short
    if (this.targetLen < 15) {
      this.finished = true; // mark as done
      return; //exot
    }

    // glitching logic
    if (this.glitching) {
      this.len -= this.shrinkSpeed; // shrink backwards towards start point

      // if fully shrunk
      if (this.len <= 0) {
        this.len = 0;
        this.finished = true; // marks done
        this.end = { x: this.start.x, y: this.start.y }; // move end to start
      } else {
        // update the end point
        this.end.x = this.start.x + cos(this.angle) * this.len;
        this.end.y = this.start.y + sin(this.angle) * this.len;
      }
    }

    // growing logic
    else if (!this.finished) {
      // if growing
      if (this.len < this.targetLen) {
        // if not done growing
        this.len += this.speed; // keeps growing

        // update the end point as it grows
        this.end.x = this.start.x + cos(this.angle) * this.len;
        this.end.y = this.start.y + sin(this.angle) * this.len;
      } else {
        this.finished = true; // finished growing
      }

      // if finished growing, spawn children or glitch
      if (this.finished && !this.childrenBranch) {
        // if not the last generation:
        if (this.generation > 0) {
          this.makeBranch(); // makes branch
        } else {
          // 50% chance to glitch if last generation
          if (random() < 0.5) {
            this.startGlitch(); // glitc instead of grow
          }
        }

        this.childrenBranch = true; // prevents repeating
      }
    }

    // loop through children branches
    for (let i = this.branches.length - 1; i >= 0; i--) {
      let child = this.branches[i]; // gets each child branch

      // check if glitching child will hit 0 next
      if (child.glitching && child.len - child.shrinkSpeed <= 0) {
        this.branches.splice(i, 1); // remove from array
      } else {
        child.update(); // keeps updating if not
      }
    }
  }

  // add new child branches
  makeBranch() {
    const numChildren = int(random(2, 3)); // choose 2 or 3 children
    let created = false; // tracks if at least one child was made

    // loop for each child
    for (let i = 0; i < numChildren; i++) {
      const newAngle = this.angle + random(-PI / 4, PI / 4); // random angle
      const newGeneration = this.generation - 1; // one generation lower
      const spawnChance = map(this.generation, 1, 8, 0.2, 1.0); // less chance to spawn as generation lowers

      // checks if generation is valid, and a random chance on creation
      if (newGeneration > 0 && random() < spawnChance) {
        //creates a random length based on min and max
        const newLen = random(
          max(10, newGeneration * 5 + 10), // makes sure it isn't too short
          newGeneration * 20 + 20 // max value
        );

        // creates new branch (yay recursion!)
        const child = new Branch(
          { x: this.end.x, y: this.end.y }, // new branch starts where this one ends
          newAngle,
          newLen,
          newGeneration,
          this //makes this branch the parent of new branches
        );
        this.branches.push(child); // add to branch's children
        created = true; // mark we created something
      }
    }

    // if no children got made, possibility of glitch instead
    if (!created && random() < 0.5) {
      // 50% chance
      this.startGlitch();
    }
  }

  // starts glitching
  startGlitch() {
    this.glitching = true; //activates shrinking
    this.finished = false; // keeps it shrinking
  }

  // draw function for branch and its children
  show() {
    if (this.targetLen < 15) return; // skip if branch is too short

    stroke(255, map(this.generation, 0, 8, 100, 255)); // transparency lowers by generation
    strokeWeight(map(this.generation, 0, 8, 1, 3)); // stroke gets thinner by generation

    line(this.start.x, this.start.y, this.end.x, this.end.y); // draws the line

    //loops through child branches
    for (let child of this.branches) {
      child.show(); // draws them
    }
  }
}
```

Okay this may not look any different BUT IT MAKES ALL THE DIFFERENCE! I promise. I orginally asked for help because I wanted to create the glitch effect, but I just realized that none of the branches was being stored, so each branch didn't know what was their parent branch and so forth, so it couldn't really glitch backwards because the information of where it should go basically was impossible to find. But if you replay the draft, you can see that there are glitches happening! That means it is working as intended and I have never been happier in my life

I added some chance of it glitching so not everything is glitching, which adds the randomness.

# Assignment 2 Draft 4

Then I wanted to keep it going by letting these glitched branches regrow, but at a different angle, so basically calling itself again to regrow. I also had it get more transparent the deeper the generations go, and the stroke gets smaller (I'm not sure if I already mentioned that in my previous drafts).

I had an idea that when it glitches, I move "back" a generation so the code thinks it's not yet done growing. I tried to code this but it didn't work so I was ablel to figure out that instead of splicing the branches from the array which erase it completely, I just reset its values so it is able to be regrown again!

 <iframe id="A2.4" src="https://editor.p5js.org/yeahlia/sketches/r45kMr0U6"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A2.4`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

```js
let rootBranches = []; // stores the 10 original branches

// SETUP ----------------------------------------------------------------------------------------------------

function setup() {
  createCanvas(windowWidth, windowHeight); // makes the canvas fit the browser window
  stroke("white"); // sets stroke color to white
  strokeWeight(2); // base stroke weight

  let centreX = width / 2; // centre horizontal
  let centreY = height / 2; // centre vertical

  // loop to make 10 starting branches
  for (let i = 0; i < 10; i++) {
    let startAngle = random(TWO_PI); // picks a random angle
    let startLength = random(40, 80); // picks a random length
    // creates a new branch and adds it to rootBranches array
    rootBranches.push(
      // creates new branch starting from centre, random angle and length and the generation
      new Branch({ x: centreX, y: centreY }, startAngle, startLength, 8, null)
    );
  }
}

// DRAW -----------------------------------------------------------------------------------------------------

function draw() {
  background(0); // draws background and refreshes frames

  // loop through all root branches and update and draw them
  for (let b of rootBranches) {
    b.update(); // update growth or glitch
    b.show(); // draw the branch
  }
}

// BRANCH CLASS ---------------------------------------------------------------------------------------------

class Branch {
  // constructor for making a new branch
  constructor(start, angle, targetLen, generation, parent) {
    this.start = { x: start.x, y: start.y }; // sets the start position of the branch
    this.end = { x: start.x, y: start.y }; // end starts at same point, will grow over time
    this.angle = angle; // direction
    this.targetLen = targetLen; // max length this branch will grow to
    this.generation = generation; // generation number

    this.len = 0; // how much it has currently grown
    this.speed = random(0.3, 0.7); // how fast it grows
    this.shrinkSpeed = random(0.5, 1.2); // how fast it shrinks if glitching

    this.finished = false; // true when branch stops growing or glitching
    this.childrenBranch = false; // tracks if children have been created already
    this.branches = []; // array to store child branches

    this.glitching = false; // true when branch is shrinking
  }

  // update logic
  update() {
    // if length is too short
    if (this.targetLen < 15) {
      this.finished = true; // mark as done
      return; //exot
    }

    // glitching logic
    if (this.glitching) {
      this.len -= this.shrinkSpeed; // shrink backwards towards start point

      // if fully shrunk
      if (this.len <= 0) {
        this.len = 0;

        // instead of deleting the branch, reset it to regrow
        this.finished = false; // starts growing again
        this.glitching = false; // stop glitching mode
        this.childrenBranch = false; // allow new children later

        // optional: tweak direction and growth length
        this.angle += random(-PI / 6, PI / 6);
        this.speed = random(0.3, 0.7);
        this.targetLen = random(40, 80);

        // reset end position to start again
        this.end = { x: this.start.x, y: this.start.y };
      } else {
        // update the end point
        this.end.x = this.start.x + cos(this.angle) * this.len;
        this.end.y = this.start.y + sin(this.angle) * this.len;
      }
    }

    // growing logic
    else if (!this.finished) {
      // if growing
      if (this.len < this.targetLen) {
        // if not done growing
        this.len += this.speed; // keeps growing

        // update the end point as it grows
        this.end.x = this.start.x + cos(this.angle) * this.len;
        this.end.y = this.start.y + sin(this.angle) * this.len;
      } else {
        this.finished = true; // finished growing
      }

      // if finished growing, spawn children or glitch
      if (this.finished && !this.childrenBranch) {
        // if not the last generation:
        if (this.generation > 0) {
          this.makeBranch(); // makes branch
        } else {
          // 50% chance to glitch if last generation
          if (random() < 0.5) {
            this.startGlitch(); // glitc instead of grow
          }
        }

        this.childrenBranch = true; // prevents repeating
      }
    }

    // loop through children branches
    for (let i = this.branches.length - 1; i >= 0; i--) {
      let child = this.branches[i]; // gets each child branch

      child.update(); // update normally (no splice anymore)
    }
  }

  // add new child branches
  makeBranch() {
    const numChildren = int(random(2, 3)); // choose 2 or 3 children
    let created = false; // tracks if at least one child was made

    // loop for each child
    for (let i = 0; i < numChildren; i++) {
      const newAngle = this.angle + random(-PI / 4, PI / 4); // random angle
      const newGeneration = this.generation - 1; // one generation lower
      const spawnChance = map(this.generation, 1, 8, 0.2, 1.0); // less chance to spawn as generation lowers

      // checks if generation is valid, and a random chance on creation
      if (newGeneration > 0 && random() < spawnChance) {
        //creates a random length based on min and max
        const newLen = random(
          max(10, newGeneration * 5 + 10), // makes sure it isn't too short
          newGeneration * 20 + 20 // max value
        );

        // creates new branch (yay recursion!)
        const child = new Branch(
          { x: this.end.x, y: this.end.y }, // new branch starts where this one ends
          newAngle,
          newLen,
          newGeneration,
          this //makes this branch the parent of new branches
        );
        this.branches.push(child); // add to branch's children
        created = true; // mark we created something
      }
    }

    // if no children got made, possibility of glitch instead
    if (!created && random() < 0.5) {
      // 50% chance
      this.startGlitch();
    }
  }

  // starts glitching
  startGlitch() {
    this.glitching = true; //activates shrinking
    this.finished = false; // keeps it shrinking
  }

  // draw function for branch and its children
  show() {
    if (this.targetLen < 15) return; // skip if branch is too short

    stroke(255, map(this.generation, 0, 8, 100, 255)); // transparency lowers by generation
    strokeWeight(map(this.generation, 0, 8, 1, 3)); // stroke gets thinner by generation

    line(this.start.x, this.start.y, this.end.x, this.end.y); // draws the line

    //loops through child branches
    for (let child of this.branches) {
      child.show(); // draws them
    }
  }
}
```

I changed the angle of the regrowing angles to be a bit more dramatic. I think it makes everything more lively and shows that ecosystems are always constantly in a state of movement and inbetween growth and decay. Currently, since there is a lot of chance and randomness evolves, over time it eventually stops moving because no branches hit the "glitch" percentage, and there is no system for any movement after it is marked finished. I want to change this in my next iteration!

# Assignment 2 Draft 5

My goal for this was to make it keep on moving, without the need to reset!

 <iframe id="A2.5" src="https://editor.p5js.org/yeahlia/sketches/WIcrRPu7U"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A2.5`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

```js
let rootBranches = []; // stores the 10 original branches

// SETUP ----------------------------------------------------------------------------------------------------

function setup() {
  // initializes canvas
  createCanvas(windowWidth, windowHeight); // makes the canvas fit the browser window
  stroke("white"); // sets stroke color to white
  strokeWeight(2); // base stroke weight

  let centreX = width / 2; // centre horizontal
  let centreY = height / 2; // centre vertical

  // loop to make 10 starting branches
  for (let i = 0; i < 10; i++) {
    let startAngle = random(TWO_PI); // TWEAK picks a random angle
    let startLength = random(40, 80); // TWEAK picks a random length
    // creates a new branch and adds it to rootBranches array
    rootBranches.push(
      // creates new branch starting from centre, random angle and length and the generation
      new Branch({ x: centreX, y: centreY }, startAngle, startLength, 8, null) // TWEAK initial generation count
    );
  }
}

// DRAW -----------------------------------------------------------------------------------------------------

// runs every frame
function draw() {
  background(0); // draws background and refreshes frames

  let activeBranch = 0; // tracks how many branches are moving

  // loops through all root branches
  for (let b of rootBranches) {
    b.update(); // update growth or glitch
    b.show(); // draw the branch
    activeBranch += b.countMoving(); // counts active branches
  }

  let idleLastBranch = []; // array for last generation branches that aren't moving
  // loops through each root branch
  for (let b of rootBranches) {
    // search the deepest branches and checks if they are not moving, and adds to array
    b.collectIdleLastBranch(idleLastBranch);
  }

  // TWEAK - if fewer than 30 branches:
  if (activeBranch < 30) {
    shuffle(idleLastBranch, true); // randomly shuffles through the array
    // TWEAK activates up to 200 idle branches
    for (let i = 0; i < min(200, idleLastBranch.length); i++) {
      idleLastBranch[i].regrow(); // reactivates by growing or glitching
    }
  }
}

// BRANCH CLASS ---------------------------------------------------------------------------------------------

class Branch {
  // constructor for making a new branch
  constructor(start, angle, targetLength, generation, parent) {
    this.start = { x: start.x, y: start.y }; // sets the start position of the branch
    this.end = { x: start.x, y: start.y }; // end starts at same point, will grow over time
    this.angle = angle; // direction
    this.targetLength = targetLength; // max length this branch will grow to
    this.generation = generation; // generation number

    this.len = 0; // how much it has currently grown
    this.speed = random(0.3, 0.7); // TWEAK how fast it grows
    this.shrinkSpeed = random(0.5, 1.2); // TWEAK how fast it shrinks if glitching

    this.finished = false; // true when branch stops growing or glitching
    this.childrenBranch = false; // tracks if children have been created already
    this.branches = []; // array to store child branches

    this.glitching = false; // true when branch is shrinking
  }

  // update logic
  update() {
    // checks if length is too short
    if (this.targetLength < 15) {
      this.finished = true; // mark as done
      return; // exit
    }

    // glitching logic
    if (this.glitching) {
      this.len -= this.shrinkSpeed; // shrink backwards towards start point

      // if fully shrunk
      if (this.len <= 0) {
        this.len = 0;

        // reset to allow regrowth
        this.finished = false; // starts growing again
        this.glitching = false; // stop glitching
        this.childrenBranch = false; // allow new children later

        this.angle += random(-PI / 4, PI / 4); // TWEAK angle
        this.speed = random(0.3, 0.7); // TWEAK growth speed
        this.targetLength = random(40, 80); // TWEAK random length

        this.end = { x: this.start.x, y: this.start.y }; // resets end position
        // if not fully shrunk:
      } else {
        // update end point while its shrinking
        this.end.x = this.start.x + cos(this.angle) * this.len;
        this.end.y = this.start.y + sin(this.angle) * this.len;
      }
    }

    // growing logic
    // if not glitching and not finished, then it means branch is growing:
    else if (!this.finished) {
      // keep growing until it hits target length
      if (this.len < this.targetLength) {
        this.len += this.speed; // increase length each frame
        this.end.x = this.start.x + cos(this.angle) * this.len; //updates end x
        this.end.y = this.start.y + sin(this.angle) * this.len; // updates end y
        // if done growing:
      } else {
        this.finished = true; // mark done
      }

      // once done growing, decide whether to make children or glitch
      if (this.finished && !this.childrenBranch) {
        // if not the last generation:
        if (this.generation > 0) {
          this.makeBranch(); // makes children
          // if last generation:
        } else {
          if (random() < 0.5) {
            // TWEAK 50% chance to glitch
            this.startGlitch(); // start glitch
          }
        }
        this.childrenBranch = true; // prevent repeating
      }
    }

    // loops through child branches
    for (let i = this.branches.length - 1; i >= 0; i--) {
      let child = this.branches[i]; // stores branch based on index in variable
      child.update(); // recursive update!! yay!!!
    }
  }

  // add new child branches
  makeBranch() {
    const newChild = int(random(2, 3)); // TWEAK choose 2 or 3 children
    let created = false; // checks if successfuly created

    // loops through children
    for (let i = 0; i < newChild; i++) {
      const newAngle = this.angle + random(-PI / 4, PI / 4); // TWEAK angle spread
      const newGeneration = this.generation - 1; // lowers generation
      const spawnChance = map(this.generation, 1, 8, 0.2, 1.0); // TWEAK lower gens lowers the spawn chance

      // checks if child should be created based on spawnChance variable
      if (random() < spawnChance) {
        const newLen = random(
          max(10, newGeneration * 5 + 10), // TWEAK minimum length
          newGeneration * 20 + 20 // TWEAK maximum length
        );

        // yay recursion! new branch
        const child = new Branch(
          { x: this.end.x, y: this.end.y }, // child starts at the end of the parent
          newAngle, // random angle
          newLen, // randome length
          newGeneration, // new generation
          this // makes it self the parent
        );
        this.branches.push(child); // adds new child
        created = true; // marks branch created
      }
    }

    // TWEAK if no childre, 50% chance it will glitch instead
    if (!created && random() < 0.5) {
      this.startGlitch(); // starts glitch
    }
  }

  // glitching function
  startGlitch() {
    this.glitching = true;
    this.finished = false; // allows glitching to run
  }

  // draw function for branch and its children
  show() {
    if (this.targetLength < 15) return; // doesnt draw too smal branches

    stroke(255, map(this.generation, 0, 8, 100, 255)); // TWEAK more transparent by generation
    strokeWeight(map(this.generation, 0, 8, 1, 3)); // TWEAK smaller by generation

    line(this.start.x, this.start.y, this.end.x, this.end.y); // draws branch

    // loops and draws all the children
    for (let child of this.branches) {
      child.show(); // draw children
    }
  }

  // counts all moving branches (growing or glitching)
  countMoving() {
    // counts 1 if the branch is growing or glitching
    let count =
      this.glitching || (!this.finished && this.len < this.targetLength)
        ? 1
        : 0;
    // loops through each child branch
    for (let child of this.branches) {
      count += child.countMoving(); // counts all the moving ones
    }
    return count; // returns all the moving branches
  }

  // gets the last child of branch
  lastGen() {
    if (this.branches.length === 0) return this; // if no childre, return itself
    return this.branches[this.branches.length - 1].lastGen(); // otherwise, get last child
  }

  // collects all finished and non-glitching branches and adds to list
  collectIdleLastBranch(done) {
    // checks if not moving
    if (this.branches.length === 0 && this.finished && !this.glitching) {
      done.push(this); // if not, push to list
    }
    // loops through each child branch
    for (let b of this.branches) {
      b.collectIdleLastBranch(done); // collect from each child
    }
  }

  // tries to regrow branch
  regrow() {
    // if branch is not moving:
    if (this.finished && !this.glitching) {
      // TWEAK 70% chance to regrow
      if (this.len === 0 && random() < 0.7) {
        this.finished = false; // unmark finished
        this.childrenBranch = false; //reset so can make children
        this.targetLength = random(40, 80); // TWEAK new target length
        this.speed = random(0.3, 0.7); // TWEAK new speed
        this.angle += random(-PI / 4, PI / 4); // TWEAK nee angle
        this.end = { x: this.start.x, y: this.start.y }; // reset end point
      }

      // TWEAK 50% chance of glitch
      else if (this.len >= this.targetLength && random() < 0.5) {
        this.startGlitch(); // starts glitching
      }
    }
  }
}
```

I was successful! did this by making some code that counts all currently growing or glitching branches, and if it is less than a certain number, it regrows a certain number of last generation child branches that AREN'T moving. These numbers are tweakable and I've been playing around with them to see what works best.

I had some issues though because even though I said I wanted to wake up 20 more child branches, 20 didn't start moving. It took a while for me to figure out why, but I asked ChatGPT and it said it was because when I marked a branch as finished, it didn't allow for any more regrowth. To fix this I adjusted soemthing in the regrow function to reset the state so it was able to grow or glitch again if called for.

Anyways because of this it is able to move infinitely yay! Now I had this idea to make things sway and the branches swaying towards the mouse? And also I need to add sound and make it more chaotic. Maybe by adding a click function that adds another node so the entire thing looks like layers of an ecosystem? Then I need to choose the colors too...

Coding is hard, how do coders sleep.

# Assignment 2 Draft 6

Anyways in THE SAME NIGHT (mind you everything from draft 3 to now has been in the same day. I'm going crazy) I added the swaying function. It wasn't too hard because the teacher's recursion example basically had it, but I just decided to use math and radians and PI for it because I wasn't sure what the p5 equivalent to some of the methods were, but to be honest it wasn't too hard.

 <iframe id="A2.6" src="https://editor.p5js.org/yeahlia/sketches/mMnvgufQ2"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A2.6`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

```js
let rootBranches = []; // stores the 10 original branches

// SETUP ----------------------------------------------------------------------------------------------------

// initializes canvas
function setup() {
  createCanvas(windowWidth, windowHeight); // makes the canvas fit the browser window
  stroke("white"); // sets stroke color to white
  strokeWeight(2); // base stroke weight

  let centreX = width / 2; // centre horizontal
  let centreY = height / 2; // centre vertical

  // loop to make 10 starting branches
  for (let i = 0; i < 10; i++) {
    let startAngle = random(TWO_PI); // TWEAK picks a random angle
    startAngle += sin(i) * 0.2; // TWEAK3 adds slight nudge to spread outward
    let startLength = random(100, 200); // TWEAK3 makes the root branches longer

    let swayAmount = random(0.01, 0.05); // TWEAK2 how far the branches sways
    let swayRate = random(0.01, 0.03); // TWEAK2 how fast the branches sways

    // creates a new branch and adds it to rootBranches array
    rootBranches.push(
      // creates new branch:
      new Branch(
        { x: centreX, y: centreY }, // starts from centre
        startAngle, // angle
        startLength, // length
        8, // generation
        null, // parent (but null because it is the base branch)
        swayAmount, // how far it sways
        swayRate // how fast it sways
      )
    );
  }
}

// DRAW -----------------------------------------------------------------------------------------------------

// runs every frame
function draw() {
  background(0); // draws background and refreshes frames

  let activeBranch = 0; // tracks how many branches are moving

  // loops through all root branches
  for (let b of rootBranches) {
    b.update(); // update growth or glitch
    b.show(); // draw the branch
    activeBranch += b.countMoving(); // counts active branches
  }

  let idleLastBranch = []; // array for last generation branches that aren't moving
  // loops through each root branch
  for (let b of rootBranches) {
    // search the deepest branches and checks if they are not moving, and adds to array
    b.collectIdleLastBranch(idleLastBranch);
  }

  // TWEAK - if fewer than 30 branches:
  if (activeBranch < 30) {
    shuffle(idleLastBranch, true); // randomly shuffles through the array
    // TWEAK activates up to 200 idle branches
    for (let i = 0; i < min(200, idleLastBranch.length); i++) {
      idleLastBranch[i].regrow(); // reactivates by growing or glitching
    }
  }
}

// BRANCH CLASS ---------------------------------------------------------------------------------------------

class Branch {
  // constructor for making a new branch
  constructor(
    start,
    angle,
    targetLength,
    generation,
    parent,
    swayAmount,
    swayRate
  ) {
    this.start = { x: start.x, y: start.y }; // sets the start position of the branch
    this.end = { x: start.x, y: start.y }; // end starts at same point, will grow over time
    this.angle = angle; // direction
    this.targetLength = targetLength; // max length this branch will grow to
    this.generation = generation; // generation number

    this.len = 0; // how much it has currently grown
    this.speed = random(0.3, 0.7); // TWEAK how fast it grows
    this.shrinkSpeed = random(0.5, 1.2); // TWEAK how fast it shrinks if glitching

    this.finished = false; // true when branch stops growing or glitching
    this.childrenBranch = false; // tracks if children have been created already
    this.branches = []; // array to store child branches

    this.glitching = false; // true when branch is shrinking

    this.swayAmount = swayAmount * random(0.9, 1.1); // TWEAK2 sway amount with randomness
    this.swayRate = swayRate * random(0.9, 1.1); // TWEAK2 sway rate with randomness
  }

  // update logic
  update() {
    // checks if length is too short
    if (this.targetLength < 15) {
      this.finished = true; // mark as done
      return; // exit
    }

    // glitching logic
    if (this.glitching) {
      this.len -= this.shrinkSpeed; // shrink backwards towards start point

      // if fully shrunk
      if (this.len <= 0) {
        this.len = 0; // prevents going to negatives

        // reset to allow regrowth
        this.finished = false; // starts growing again
        this.glitching = false; // stop glitching
        this.childrenBranch = false; // allow new children later

        this.angle += random(-PI / 4, PI / 4); // TWEAK angle
        this.speed = random(0.3, 0.7); // TWEAK growth speed
        this.targetLength = random(40, 80); // TWEAK random length

        this.end = { x: this.start.x, y: this.start.y }; // resets end position
      } else {
        let sway = sin(frameCount * this.swayRate) * this.swayAmount; // TWEAK2 sway angle
        let swayedAngle = this.angle + sway; // calculates angle by sway amount
        this.end.x = this.start.x + cos(swayedAngle) * this.len; // update end x with sway
        this.end.y = this.start.y + sin(swayedAngle) * this.len; // update end y with sway
      }
      //ends glitching logic, begins growth
    } else {
      let sway = sin(frameCount * this.swayRate) * this.swayAmount; // TWEAK2 sway angle
      let swayedAngle = this.angle + sway; // calculates the current angle with sway

      // if not finished growing, continue
      if (!this.finished && this.len < this.targetLength) {
        this.len += this.speed; // increase length each frame
      }

      this.end.x = this.start.x + cos(swayedAngle) * this.len; // update end x with sway
      this.end.y = this.start.y + sin(swayedAngle) * this.len; // update end y with sway

      // if finished growing:
      if (!this.finished && this.len >= this.targetLength) {
        this.finished = true; // mark done
      }

      // if branch has finished growing nad hasn't made children:
      if (this.finished && !this.childrenBranch) {
        // if not the final generation:
        if (this.generation > 0) {
          this.makeBranch(); // makes children
          // if generation is 0, can't make children
        } else {
          if (random() < 0.5) {
            this.startGlitch(); // TWEAK 50% chance to glitch
          }
        }
        this.childrenBranch = true; // prevent repeating
      }
    }

    // loops through child branches
    for (let i = this.branches.length - 1; i >= 0; i--) {
      let child = this.branches[i]; // stores branch based on index in variable
      child.start = { x: this.end.x, y: this.end.y }; // TWEAK3 connect child to parent
      child.update(); // recursive update!! yay!!!
    }
  }

  // add new child branches
  makeBranch() {
    const newChild = int(random(2, 3)); // TWEAK choose 2 or 3 children
    let created = false; // checks if successfuly created

    // loops through children
    for (let i = 0; i < newChild; i++) {
      const newAngle = this.angle + random(-PI / 4, PI / 4); // TWEAK angle spread
      const newGeneration = this.generation - 1; // lowers generation
      const spawnChance = map(this.generation, 1, 8, 0.2, 1.0); // TWEAK lower gens lowers the spawn chance

      // checks if child should be created based on spawnChance variable
      if (random() < spawnChance) {
        const newLen = random(
          newGeneration * 10 + 20, // TWEAK3 longer children
          newGeneration * 30 + 40 // TWEAK3 longer maximum length
        );

        // yay recursion! new branch
        const child = new Branch(
          { x: this.end.x, y: this.end.y }, // child starts at the end of the parent
          newAngle, // random angle
          newLen, // random length
          newGeneration, // new generation
          this, // makes it self the parent
          this.swayAmount, // pass sway amount
          this.swayRate // pass sway rate
        );
        this.branches.push(child); // adds new child
        created = true; // marks branch created
      }
    }

    // TWEAK if no children, 50% chance it will glitch instead
    if (!created && random() < 0.5) {
      this.startGlitch(); // starts glitch
    }
  }

  // glitching function
  startGlitch() {
    this.glitching = true; // starts glitching
    this.finished = false; // marks active so glitching has chance to occur again
  }

  // draw function for branch and its children
  show() {
    if (this.targetLength < 15) return; // doesnt draw too smal branches

    stroke(255, map(this.generation, 0, 8, 100, 255)); // TWEAK more transparent by generation
    strokeWeight(map(this.generation, 0, 8, 1, 3)); // TWEAK smaller by generation

    line(this.start.x, this.start.y, this.end.x, this.end.y); // draws branch

    // loops and draws all the children
    for (let child of this.branches) {
      child.show(); // draw children
    }
  }

  countMoving() {
    let count =
      this.glitching || (!this.finished && this.len < this.targetLength) // counts all moving branches (growing or glitching)
        ? 1 // if branch is active add 1
        : 0; // otherwise, add 0
    for (let child of this.branches) {
      count += child.countMoving(); // counts all the moving ones
    }
    return count; // returns all the moving branches
  }

  // gets the last child of branch
  lastGen() {
    if (this.branches.length === 0) return this; // if no childre, return itself
    return this.branches[this.branches.length - 1].lastGen(); // otherwise, get last child
  }

  collectIdleLastBranch(done) {
    // collects all finished and non-glitching branches and adds to list
    if (this.branches.length === 0 && this.finished && !this.glitching) {
      done.push(this); // if not, push to list
    }
    for (let b of this.branches) {
      //loops through child branches
      b.collectIdleLastBranch(done); // collect last, not moving branches
    }
  }

  // tries to regrow branch (or can start glitching)
  regrow() {
    if (this.finished && !this.glitching) {
      if (this.len === 0 && random() < 0.7) {
        this.finished = false; // unmark finished
        this.childrenBranch = false; //reset so can make children
        this.targetLength = random(40, 80); // TWEAK new target length
        this.speed = random(0.3, 0.7); // TWEAK new speed
        this.angle += random(-PI / 4, PI / 4); // TWEAK new angle
        this.end = { x: this.start.x, y: this.start.y }; // reset end point
      } else if (this.len >= this.targetLength && random() < 0.5) {
        this.startGlitch(); // starts glitching
      }
    }
  }
}
```

So before I got to this I had a few issues acutally. First I just decided to add like the sway amount and sway rate to the individual branches but when I pressed play, it basically just made each branch wobble on its own and everything disconnected from each other and didn't look like an interconnected system.

To fix this, I tried to make the original 10 root branches pass down its sway rate to its child branches, which recursively passed it down to the smaller ones. This helped it, but there was still some disconnect and after a bit of being very confused and wanting to throw my laptop across the room, it was because the start points weren't moving, they were fixed.

So to fix this I had to add something in the update loop that kept track of the swaying end point of every branch, so the start point of the child branch would dynamically adjust to it. So basically it just links all the points together instead of just copying the end point of the parent branch and using it as the start point of the child branch.

I've seen the word branch too many times it doesn't look real anymore..

ANYWAYS that was enough for one night, I think tomorrow I want to add the function where it follows the mouse (it can't be that hard right... just make it sway towards the x and y points of my mouse? right?) and then maybe the sound. I definitely still want to add the click function where it makes a new node, but I think it's a better idea to get everything functioning with the main one before I add that since it would basically just be doing what the main one is doing.

After that I probably would want to change the colors so it looks less plain, and tweak all the rates and percentages to a chaotic enough level... hopefully...

# Assignment Draft 7

Next day... I wrote some code that moves biased towards the mouse, but it kinda removed the swaying that I like, I want it to not have so much strength. I showed the teacher and basically using physics and velocity will help it look more alive which I did here:

 <iframe id="A2.7" src="https://editor.p5js.org/yeahlia/sketches/OfqDJHehO"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A2.7`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

```js
let colonies = []; // array for each colony
let maxColonies = 5; // how many colonies stay on screen
const colorPalette = ["#e7bc91", "#bc8a5f", "#8b5e34", "#6f4518", "#583101"]; // color palette

// SETUP ----------------------------------------------------------------------------------------------------

// initializes canvas
function setup() {
  createCanvas(windowWidth, windowHeight); // makes the canvas fit the browser window
  strokeWeight(2); // sets base stroke weight
  spawnColony(width / 2, height / 2); // spawns first colony at center
}

// DRAW -----------------------------------------------------------------------------------------------------

// runs every frame
function draw() {
  background("#ffedd8"); // draws background and refreshes frames

  // loops through each colony
  for (let colony of colonies) {
    for (let branch of colony.branches) {
      branch.update(); // update growth or glitch
      branch.show(colony.color, colony.alpha); // draw branch with color and transparency
    }
  }

  // if the lenggth of colonies is over the max colonies:
  if (colonies.length > maxColonies) {
    colonies[0].alpha -= 1; // fades the oldest colony
    if (colonies[0].alpha <= 0) {
      // when transparecny reaches 0,
      colonies.shift(); //
    }
  }
}

// MOUSE CLICK ----------------------------------------------------------------------------------------------

// runs when mouse is clicked
function mousePressed() {
  spawnColony(mouseX, mouseY); // spawns new colony at mouse location
}

// SPAWN COLONY ------------------------------------------------------------------------------------

// function to spawn a new colony
function spawnColony(x, y) {
  let colony = { branches: [], color: random(colorPalette), alpha: 255 }; // creates new colony with the values

  // loop to make 10 starting branches
  for (let i = 0; i < 10; i++) {
    let startAngle = random(TWO_PI); // TWEAK1 picks a random angle
    startAngle += sin(i) * 0.2; // TWEAK3 adds slight nudge to spread outward
    let startLength = random(100, 200); // TWEAK3 makes the root branches longer

    let swayAmount = random(0.01, 0.05); // TWEAK2 how far the branch sways
    let swayRate = random(0.01, 0.03); // TWEAK2 how fast the branch sways

    let b = new Branch( // creates a new branch
      { x: x, y: y }, // position
      startAngle,
      startLength,
      8, // generation
      null, // parent (null for root)
      swayAmount,
      swayRate
    );
    colony.branches.push(b); // add branch to colony
  }

  colonies.push(colony); // adds colony to colonies array
}

// BRANCH CLASS ---------------------------------------------------------------------------------------------

class Branch {
  constructor(
    start,
    angle,
    targetLength,
    generation,
    parent,
    swayAmount,
    swayRate
  ) {
    this.start = { x: start.x, y: start.y }; // sets the start position of the branch
    this.end = { x: start.x, y: start.y }; // end starts at same point, will grow over time
    this.angle = angle; // direction
    this.targetLength = targetLength; // max length this branch will grow to
    this.generation = generation; // generation number

    this.len = 0; // how much it has currently grown
    this.speed = random(0.1, 1.5); // TWEAK1 how fast it grows
    this.shrinkSpeed = random(0.5, 1.2); // TWEAK1 how fast it shrinks if glitching

    this.finished = false; // true when branch stops growing or glitching
    this.childrenBranch = false; // tracks if children have been created already
    this.branches = []; // array to store child branches

    this.glitching = false; // true when branch is shrinking

    this.swayAmount = swayAmount * random(0.9, 1.1); // TWEAK2 sway amount with randomness
    this.swayRate = swayRate * random(0.9, 1.1); // TWEAK2 sway rate with randomness

    // physics variables
    this.velX = 0; // TWEAK4 x velocity for soft movement
    this.velY = 0; // TWEAK4 y velocity for soft movement
    this.accX = 0; // TWEAK4 x acceleration based on mouse bias
    this.accY = 0; // TWEAK4 y acceleration based on mouse bias
  }

  // update logic
  update() {
    // if larget length istoo short
    if (this.targetLength < 15) {
      this.finished = true; // mark as done
      return;
    }

    // if it is glitching
    if (this.glitching) {
      this.len -= this.shrinkSpeed; // shrink backwards towards start point
      // if done shrinking
      if (this.len <= 0) {
        this.len = 0; // prevents going to negatives
        this.finished = false; // starts growing again
        this.glitching = false; // stop glitching
        this.childrenBranch = false; // allow new children later

        this.angle += random(-PI / 4, PI / 4); // TWEAK1 random new angle
        this.speed = random(0.3, 0.7); // TWEAK1 new speed
        this.targetLength = random(40, 70); // TWEAK1 new target length
        this.end = { x: this.start.x, y: this.start.y }; // reset end position
      } else {
        this.physicsUpdate(); // update physics when glitching
      }
    } else {
      if (!this.finished && this.len < this.targetLength) {
        this.len += this.speed; // continue growing
      }

      this.physicsUpdate(); // update physics while growing

      // if reached target length
      if (!this.finished && this.len >= this.targetLength) {
        this.finished = true; // mark as finished growing
      }

      // if finished and no children
      if (this.finished && !this.childrenBranch) {
        if (this.generation > 0) {
          this.makeBranch(); // make children if not last generation
        } else {
          if (random() < 0.5) {
            this.startGlitch(); // 50 % chance to start glitching
          }
        }
        this.childrenBranch = true; // prevent double creating
      }
    }

    // updates children
    for (let child of this.branches) {
      child.start = { x: this.end.x, y: this.end.y }; // connects child to parent's end
      child.update(); // recursive update!!! yay
    }
  }

  // physics (i hate math)
  physicsUpdate() {
    let sway = sin(frameCount * this.swayRate) * this.swayAmount; // TWEAK2 sway angle
    let swayedAngle = this.angle + sway; // calculates swayed angle

    let targetX = this.start.x + cos(swayedAngle) * this.len; // base target x without bias
    let targetY = this.start.y + sin(swayedAngle) * this.len; // base target y without bias

    // bias forces toward mouse
    let biasStrength = 0.001; // TWEAK4 bias pull
    let noiseStrength = 0.5; // TWEAK5 random noise

    // add mouse bias and noise
    let offsetX = mouseX - targetX + random(-noiseStrength, noiseStrength);
    let offsetY = mouseY - targetY + random(-noiseStrength, noiseStrength);

    // updates acceleration
    this.accX += offsetX * biasStrength;
    this.accY += offsetY * biasStrength;

    // updates velocity
    this.velX += this.accX;
    this.velY += this.accY;

    // apply friction
    let friction = 0.9; // TWEAK4 friction
    this.velX *= friction;
    this.velY *= friction;

    // reset acceleration
    this.accX = 0;
    this.accY = 0;

    // updates final position
    this.end.x = targetX + this.velX;
    this.end.y = targetY + this.velY;
  }

  // make child branches
  makeBranch() {
    const newChild = int(random(2, 3)); // TWEAK choose 2 or 3 children
    let created = false; // whether child was made

    for (let i = 0; i < newChild; i++) {
      const newAngle = this.angle + random(-PI / 4, PI / 4); // TWEAK angle spread
      const newGeneration = this.generation - 1; // next generation
      const spawnChance = map(this.generation, 1, 8, 0.2, 1.0); // TWEAK spawn chance

      // if allowed to spawn
      if (random() < spawnChance) {
        const newLen = random(newGeneration * 10 + 20, newGeneration * 30 + 40); // TWEAK child length
        // makes a new child with branch class!!!!
        const child = new Branch(
          { x: this.end.x, y: this.end.y },
          newAngle,
          newLen,
          newGeneration,
          this,
          this.swayAmount,
          this.swayRate
        );
        this.branches.push(child); // adds child
        created = true; // marks created
      }
    }

    if (!created && random() < 0.5) {
      this.startGlitch(); // chance to glitch instead
    }
  }

  startGlitch() {
    this.glitching = true; // start glitching
    this.finished = false; // mark active again
  }

  // draw branch
  show(colonyColor, colonyAlpha) {
    if (this.targetLength < 15) return; // skip tiny branches

    let c = color(colonyColor); // colony color
    c.setAlpha(map(this.generation, 0, 8, 100, colonyAlpha)); // fade by generation
    stroke(c); // set stroke color and alpha
    strokeWeight(map(this.generation, 0, 8, 1, 4)); // TWEAK stroke weight
    line(this.start.x, this.start.y, this.end.x, this.end.y); // draw line

    for (let child of this.branches) {
      child.show(colonyColor, colonyAlpha); // recursively show children
    }
  }
}
```

This is what I got! To be honest it isn't actually what I wanted, I still think it doesn't move as naturally as it could but I could't figure it out and to be honest I am so ready to be done with this assignment... Other than the bias I changed the colors and made it choose random colors from an array. I changed it to have 'colony' clusters instead, and saved those (becuase it wasn't being store anywhere previously) so I could also add my own colonies on the click so its more chaotic I guess.

I noticed that when you clicked too much it became too messy and less structured, so I limited the amount of total clusters on screen to 5, and when it went over, the transparency of the oldest cluster would slowly decrease before being completely removed from the array. And yeah! It's so easy to make these changes now with the branches and colonies being in objects and such!

# Final Assignment 2!

THIS IS THE FINAL ASSIGNMENT YAY!!!! IM SO HAPPY! Anyways I just basically did osme last minute changes and added the audio! Fun fact I am doing sound design for a specialisation so I had a lot of fun in terms of the oscillators and stuff, I wish tehre were physical knobs!

 <iframe id="A2.8" src="https://editor.p5js.org/yeahlia/sketches/JXq-CAQv1"></iframe>

<script type="module">

    const iframe  = document.getElementById (`A2.8`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

```js
let colonies = []; // array for each colony
let maxColonies = 5; // how many colonies stay on screen
const colorPalette = ["#e7bc91", "#bc8a5f", "#8b5e34", "#6f4518", "#583101"]; // color palette
let audioContext; // stores the audio context for sosund stuff
let color1 = "#ffedd8"; // color 1 for background
let color2 = "#fcf5ca"; // color 2 for background

// SETUP ----------------------------------------------------------------------------------------------------

// initializes canvas
function setup() {
  createCanvas(windowWidth, windowHeight); // canvas to fit the window size
  strokeWeight(2); // stroke weight for lines

  // create AudioContext
  audioContext = new (window.AudioContext || window.webkitAudioContext)();

  spawnColony(width / 2, height / 2); // spawns colony right in the middle
}

// DRAW -----------------------------------------------------------------------------------------------------

// runs every frame
function draw() {
  // checks every 220 frames
  if (frameCount % 220 === 0) {
    let temp = color1; // temporarily stores the first color
    color1 = color2; // sets first color to second color
    color2 = temp; // sets the second color back to temporary first color
  }

  // maps frame count, then blends the 2 colors for a smooth transition
  let lerpPos = map(frameCount % 220, 0, 100, 0, 1);
  let backgroundColor = lerpColor(color(color1), color(color2), lerpPos);

  background(backgroundColor); // sets the background

  // draw branches
  // loops through each colony
  for (let colony of colonies) {
    // loops through each branch of that colony
    for (let branch of colony.branches) {
      branch.update(); // update logic
      branch.show(colony.color, colony.alpha); // draws branch using that color
    }
  }

  // colony limit
  // if too many colonies on screen
  if (colonies.length > maxColonies) {
    colonies[0].alpha -= 1; // fades out the oldest colony slowly
    // when fully faded and cant see anymore
    if (colonies[0].alpha <= 0) {
      let c = colonies.shift(); // remove from array

      // fades out the sound smoothly
      c.volume.gain.exponentialRampToValueAtTime(
        0.0001,
        audioContext.currentTime + 1
      );
      c.oscillator.stop(audioContext.currentTime + 1); // stops the oscillator after 1 second
      c.lfo.stop(audioContext.currentTime + 1); // stops LFO after 1 second
    }
  }

  // loops through all colonies
  for (let colony of colonies) {
    let bendAmount = map(mouseX, 0, width, -100, 100); //maps mouse to pitch bend range + or - 100Hz
    colony.oscillator.frequency.setValueAtTime(
      colony.baseFreq + bendAmount, // base frequency and bend
      audioContext.currentTime
    );
  }
}

// MOUSE CLICK ----------------------------------------------------------------------------------------------

// runs when mouse is clicked
function mousePressed() {
  // if audio is not playing
  if (audioContext.state !== "running") {
    audioContext.resume(); // resume audio
  }
  spawnColony(mouseX, mouseY); // spawns new colony at mouse location
}

// SPAWN COLONY ------------------------------------------------------------------------------------

// function to spawn a new colony
function spawnColony(x, y) {
  let waveform = ["sine", "square", "sawtooth"]; // defines the different waveform
  let waveformType = random(waveform); // chooses random

  let oscillator = audioContext.createOscillator(); // makes sound generator
  let volume = audioContext.createGain(); // volume controller
  let lfo = audioContext.createOscillator(); // LFO for vibrato
  let lfoGain = audioContext.createGain(); // LFO affecting pitch

  oscillator.type = waveformType; // sets up waveform shape
  oscillator.frequency.setValueAtTime(
    random(200, 800), // picks random base freq
    audioContext.currentTime // sets now
  );

  volume.gain.setValueAtTime(0.05, audioContext.currentTime); // low volume

  lfo.frequency.setValueAtTime(random(5, 12), audioContext.currentTime); // cibrato between 5 and 12 Hz
  lfoGain.gain.setValueAtTime(20, audioContext.currentTime); // how fast it wiggles

  lfo.connect(lfoGain); // connects LFO output to gain
  lfoGain.connect(oscillator.frequency); //connects LFO to change pitch

  oscillator.connect(volume); // oscillator to volume
  volume.connect(audioContext.destination); // volume to speakers

  oscillator.start(); // starts oscillator
  lfo.start(); // start LFO

  // create colony
  let colony = {
    branches: [], // holds its branches
    color: random(colorPalette), // chooses random color from palette
    alpha: 255, // opacity
    oscillator: oscillator, // stores oscillator
    volume: volume, // stores volume
    lfo: lfo, // stores lfo
    lfoGain: lfoGain, // stores lfo volume
    baseFreq: oscillator.frequency.value, // base frequency for pitch shifting
  };

  // loops through 10 starting branches
  for (let i = 0; i < 10; i++) {
    let startAngle = random(TWO_PI); // random starting angle
    startAngle += sin(i) * 0.2; // wave variation
    let startLength = random(100, 200); // random starting length
    let swayAmount = random(0.01, 0.05); // random sway amount
    let swayRate = random(0.01, 0.03); // random sway seed

    // new branch
    let b = new Branch(
      { x: x, y: y }, // where branch starts
      startAngle, // angle
      startLength, // length
      8, // generation
      null, // parent
      swayAmount, // sway amount
      swayRate, // sway speed
      colony // pass colony
    );
    colony.branches.push(b); // add branch to colony
  }

  colonies.push(colony); // add colony ro colonies array
}

// BRANCH CLASS ---------------------------------------------------------------------------------------------

class Branch {
  constructor(
    start, // start position
    angle, // angle
    targetLength, // tartget length
    generation, // geneartion amount
    parent, // parent branch
    swayAmount, // sway amount
    swayRate, // swayrate
    colony // reference colony
  ) {
    this.start = { x: start.x, y: start.y }; // sets the start position of the branch
    this.end = { x: start.x, y: start.y }; // end starts at same point, will grow over time
    this.angle = angle; // direction
    this.targetLength = targetLength; // max length this branch will grow to
    this.generation = generation; // generation number

    this.parent = parent; // stsore parents
    this.colony = colony; // store colony

    this.len = 0; // how much it has currently grown
    this.speed = random(0.1, 1.5); // TWEAK1 how fast it grows
    this.shrinkSpeed = random(0.5, 1.2); // TWEAK1 how fast it shrinks if glitching

    this.finished = false; // true when branch stops growing or glitching
    this.childrenBranch = false; // tracks if children have been created already
    this.branches = []; // array to store child branches

    this.glitching = false; // true when branch is shrinking

    this.swayAmount = swayAmount * random(0.9, 1.1); // TWEAK2 sway amount with randomness
    this.swayRate = swayRate * random(0.9, 1.1); // TWEAK2 sway rate with randomness

    // physics variables
    this.velX = 0; // TWEAK4 x velocity for soft movement
    this.velY = 0; // TWEAK4 y velocity for soft movement
    this.accX = 0; // TWEAK4 x acceleration based on mouse bias
    this.accY = 0; // TWEAK4 y acceleration based on mouse bias
  }

  // update logic
  update() {
    // if larget length istoo short
    if (this.targetLength < 15) {
      this.finished = true; // mark as done
      return;
    }

    // if it is glitching
    if (this.glitching) {
      this.len -= this.shrinkSpeed; // shrink backwards towards start point
      // if done shrinking
      if (this.len <= 0) {
        this.len = 0; // prevents going to negatives
        this.finished = false; // starts growing again
        this.glitching = false; // stop glitching
        this.childrenBranch = false; // allow new children later

        this.angle += random(-PI / 4, PI / 4); // TWEAK1 random new angle
        this.speed = random(0.3, 0.7); // TWEAK1 new speed
        this.targetLength = random(40, 70); // TWEAK1 new target length
        this.end = { x: this.start.x, y: this.start.y }; // reset end position
      } else {
        this.physicsUpdate(); // update physics when glitching
      }
    } else {
      if (!this.finished && this.len < this.targetLength) {
        this.len += this.speed; // continue growing
      }

      this.physicsUpdate(); // update physics while growing

      // if reached target length
      if (!this.finished && this.len >= this.targetLength) {
        this.finished = true; // mark as finished growing
      }

      // if finished and no children
      if (this.finished && !this.childrenBranch) {
        if (this.generation > 0) {
          this.makeBranch(); // make children if not last generation
        } else {
          if (random() < 0.5) {
            this.startGlitch(); // 50 % chance to start glitching
          }
        }
        this.childrenBranch = true; // prevent double creating
      }
    }

    // updates children
    for (let child of this.branches) {
      child.start = { x: this.end.x, y: this.end.y }; // connects child to parent's end
      child.update(); // recursive update!!! yay
    }
  }

  // physics (i hate math)
  physicsUpdate() {
    let sway = sin(frameCount * this.swayRate) * this.swayAmount; // TWEAK2 sway angle
    let swayedAngle = this.angle + sway; // calculates swayed angle

    let targetX = this.start.x + cos(swayedAngle) * this.len; // base target x without bias
    let targetY = this.start.y + sin(swayedAngle) * this.len; // base target y without bias

    // bias forces toward mouse
    let biasStrength = 0.001; // TWEAK4 bias pull
    let noiseStrength = 0.5; // TWEAK5 random noise

    // add mouse bias and noise
    let offsetX = mouseX - targetX + random(-noiseStrength, noiseStrength);
    let offsetY = mouseY - targetY + random(-noiseStrength, noiseStrength);

    // updates acceleration
    this.accX += offsetX * biasStrength;
    this.accY += offsetY * biasStrength;

    // updates velocity
    this.velX += this.accX;
    this.velY += this.accY;

    // apply friction
    let friction = 0.9; // TWEAK4 friction
    this.velX *= friction;
    this.velY *= friction;

    // reset acceleration
    this.accX = 0;
    this.accY = 0;

    // updates final position
    this.end.x = targetX + this.velX;
    this.end.y = targetY + this.velY;
  }

  // make child branches
  makeBranch() {
    const newChild = int(random(2, 3)); // TWEAK choose 2 or 3 children
    let created = false; // whether child was made

    for (let i = 0; i < newChild; i++) {
      const newAngle = this.angle + random(-PI / 4, PI / 4); // TWEAK angle spread
      const newGeneration = this.generation - 1; // next generation
      const spawnChance = map(this.generation, 1, 8, 0.2, 1.0); // TWEAK spawn chance

      // if allowed to spawn
      if (random() < spawnChance) {
        const newLen = random(newGeneration * 10 + 20, newGeneration * 30 + 40); // TWEAK child length
        // makes a new child with branch class!!!!
        const child = new Branch(
          { x: this.end.x, y: this.end.y },
          newAngle,
          newLen,
          newGeneration,
          this,
          this.swayAmount,
          this.swayRate,
          this.colony
        );
        this.branches.push(child); // adds child
        created = true; // marks created
      }
    }

    if (!created && random() < 0.5) {
      this.startGlitch(); // chance to glitch instead
    }
  }

  startGlitch() {
    this.glitching = true; // marks glitching
    this.finished = false; // marks not finished

    // if linked to a colony
    if (this.colony) {
      this.colony.lfo.frequency.setValueAtTime(
        random(20, 50), // fast vibrato for glitch
        audioContext.currentTime
      );
      setTimeout(() => {
        // reset
        this.colony.lfo.frequency.setValueAtTime(
          random(5, 12), // back to softer vibrato
          audioContext.currentTime
        );
      }, 300);
    }
  }

  // draw branch
  show(colonyColor, colonyAlpha) {
    if (this.targetLength < 15) return; // skip tiny branches

    let c = color(colonyColor); // colony color
    c.setAlpha(map(this.generation, 0, 8, 100, colonyAlpha)); // fade by generation
    stroke(c); // set stroke color and alpha
    strokeWeight(map(this.generation, 0, 8, 1, 4)); // TWEAK stroke weight
    line(this.start.x, this.start.y, this.end.x, this.end.y); // draw line

    for (let child of this.branches) {
      child.show(colonyColor, colonyAlpha); // recursively show children
    }
  }
}
```

I made it so it basically chooses a random frequency from a range and also choose if it was a sine, sawtooth or square wave. I forgot about triangle when I made it, but it's okay. When I create a new colony, it repeats this. Every frame, the pitch bends based on the location of the mouse, which I think is super cool. While the branches grow (which is all the time) I added vibrato and made it wiggle really fast so it had more texture. And when a branch glitches, I add the LFO super fast for a bit before it goes back to normal. Everything just adds a bit of randomness! Also, I had some trouble with getting the original colony to have audio, I think chrome has some restraints about audio playing, and will only play if theres user interaction, and I couldn't really get around that.

I also added a lerping background (exactly the same as I used last assignment) because I felt the background felt a bit too plain, so it fixed that a bit. I think overall it definitely could have been more chaotic, as I think it isn't that chaotic until the user clicks, it isn't chaotic to begin with. BUT I guess it kind of symbolizes how fungul eco systems grow over time and evolves into this massive, layered system. And that's basically it! I hope you like it, many nights spent on this and going crazy.
