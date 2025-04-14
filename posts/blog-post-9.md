---
title: Self Portrait
published_at: 2025-04-1
snippet:
disable_html_sanitization: true
allow_math: true
---

# Self Portrait using Pixel Sort

This is what I wrote for my code but honestly I don't know why it doesn't work...

<canvas id="pixelSort"></canvas>

<script type="module">
   import { PixelSorter } from "./static/photos/pixel_sort.js" 

   const cnv = document.getElementById("pixelSort");
   cnv.width = cnv.parentNode.scrollWidth;
   cnv.height = cnv.width * 9 / 16;   

   const ctx = cnv.getContext("2d");
   const sorter = new PixelSorter(ctx);

   const img = new Image();

   img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width);
      ctx.drawImage(img, 0, 0, cnv.width, cnv.height);
      sorter.init();
      draw_frame();
   };

   img.src = "./static/photos/self.jpg"; 

   let frame_count = 0;
   const draw_frame = () => {
      ctx.drawImage(img, 0, 0, cnv.width, cnv.height);

      let sig = Math.cos(frame_count * 2 * Math.PI / 500);

      const mid = {
         x: cnv.width / 2,
         y: cnv.height / 2
      };

      const dim = {
         x: Math.floor((sig + 3) * (cnv.width / 6)) + 1,
         y: Math.floor((sig + 1) * (cnv.height / 6)) + 1
      };

      const pos = {
         x: Math.floor(mid.x - (dim.x / 2)),
         y: Math.floor(mid.y - (dim.y / 2))
      };

      sorter.glitch(pos, dim);

      frame_count++;
      requestAnimationFrame(draw_frame);
   };
</script>

```html
<canvas id="pixelSort"></canvas>

<script type="module">
  import { PixelSorter } from "/static/photos/pixel_sort.js";

  const cnv = document.getElementById("pixelSort");
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;

  const ctx = cnv.getContext("2d");
  const sorter = new PixelSorter(ctx);

  const img = new Image();

  img.onload = () => {
    cnv.height = cnv.width * (img.height / img.width);
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);
    sorter.init();
    draw_frame();
  };

  img.src = "/static/photos/self.jpg";

  let frame_count = 0;
  const draw_frame = () => {
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);

    let sig = Math.cos((frame_count * 2 * Math.PI) / 500);

    const mid = {
      x: cnv.width / 2,
      y: cnv.height / 2,
    };

    const dim = {
      x: Math.floor((sig + 3) * (cnv.width / 6)) + 1,
      y: Math.floor((sig + 1) * (cnv.height / 6)) + 1,
    };

    const pos = {
      x: Math.floor(mid.x - dim.x / 2),
      y: Math.floor(mid.y - dim.y / 2),
    };

    sorter.glitch(pos, dim);

    frame_count++;
    requestAnimationFrame(draw_frame);
  };
</script>
```

# How Does Rendering Your Likeness in This Way Affect its Aesthetic Register?

Rendering my self portrait turns it from a clear photo, to a more interesting and zany aesthetic registers. It becomes more interesting in Ngai's standards by the glitch making people think about whats happening, how it works and why. While the zany aspect is because it is weird, fun and a bit overwhelming at times. It features chaos and high-energy.

From the glitch readings, Kane talks about how glitches show noise inside systems, while Briz sees glitches as political. By breaking my image through with glitches, I am able to expose the tools behind it, while pushing back against digital perfection and showing something more raw.

Ippolito says that online art isn't always permanent or user friendly. My work is more about the process rather than the finished product. From a posthumanism view, the glitch portrait is a combination of human and machine, and that digital identity is shaped by systems and algorithms.

In terms of effective complexity, the image sits betwen chaos and order. It's not total noises, as you're still able to see me in the self-portrait, but it isn't completely clean or pure either.
