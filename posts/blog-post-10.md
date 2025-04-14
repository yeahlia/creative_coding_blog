---
title: Post Digital Artists
published_at: 2025-04-3
snippet:
disable_html_sanitization: true
allow_math: true
---

This is just a practice on how to use p5.JS library directly onto vs code!

<script src="./scripts/p5.js"></script>

<canvas id="p5_example"></canvas>

<script>
  const cnv = document.getElementById("p5_example");
  const w = cnv.parentNode.scrollWidth;
  const h = (w * 9) / 16;

  function setup() {
    createCanvas(w, h, P2D, cnv);
  }

  function draw() {
    background(`turquoise`);
    console.log(frameCount);
  }
</script>

```html
<script src="./scripts/p5.js"></script>

<canvas id="p5_example"></canvas>

<script>
  const cnv = document.getElementById("p5_example");
  const w = cnv.parentNode.scrollWidth;
  const h = (w * 9) / 16;

  function setup() {
    createCanvas(w, h, P2D, cnv);
  }

  function draw() {
    background(`turquoise`);
    console.log(frameCount);
  }
</script>
```

# Why Does Saeko Ehara Classify as Post-Digital?

Saeko Ehara classifies as a post digital artist because her work extends beyond just using digital tools,s he also engages with culture and technology and how they shape experiences and perceptions. She blends digital techniques with physical inspirations, exploring themes like memory and impermanence.

Saeko's work 'Collectible Scape':

This artwork scans objects and turns them into a glitch digital sculpture. The end result kind of looks like the objects are from a distorted video game! This work fits Cramer's post-digital definition because it reflects on the limits of digital tools and doesn't just use it. Post-digital often combines digital and analog, some even resisting digital altogether and Saeko's work embraces the imperfection of digital tools and its failure to fully capture the physical world.

### What Technology is Saeko Ehara Using to Produce Their Work?

In terms of 'Collectible Scape', Saeko most likely used 3D scanning software and devices, photogrammetry to crate a 3D mesh, some modeling and 3D editing software as well as custom scripts to introduce the glitch aesthetics.

Some rograms, libraries and API's that she could have used is three.js for rendering the 3D scenes in the browser, TouchDesigner, Python, Unity, WebGL/WebXR and MediaPipe, etc.
