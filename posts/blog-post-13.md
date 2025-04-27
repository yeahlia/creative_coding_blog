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
you do not need render the passages in your composition explicitly
it is sufficient for the passages to be informing your creative decisions / influencing the composition, etc.

## How Well Does My Rough Draft:
### Respond to my Chosen Text

### As an Example of Post Digital (Why/Why Not)

### Functioning in a Chaotic Aesthetic Register
reference effective complexity

### How Will This Inform the Next Stage of Assignment 2