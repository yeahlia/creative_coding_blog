---
title: Using For Loops to Create a Grid
published_at: 2025-01-06
snippet: Meow
disable_html_sanitization: true
allow_math: true
---

# Initial Thoughts

Using the for loop to create a grid could be useful so we wouldn't need to write code for each square. I was thinking that to create the grid, there would be a background and multiple squares to act as the centre of the grid and the background would be the 'lines'

I could use the for loop to create a line of squares based on the canvas width, and another for loop to create columns for every row there is. I took some ideas from [this](https://gist.github.com/periode/f4faff249d4f73214d5f) website. It was pretty confusing but I used ChatGPT to simplify it and explain what each line of code was so I was able to understand it a bit easier!

## Attempt 1

From this, I created this sketch with some trial and error:

<iframe id="Grid attempt 1" src="https://editor.p5js.org/yeahlia/sketches/UqTvZSdlj"></iframe>

<script type="module">

    const iframe  = document.getElementById (`Grid attempt 1`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

The squares were a bit too small so it looks more like squares in a background instead of a grid.

## Attempt 2

<iframe id="Grid attempt 2" src="https://editor.p5js.org/yeahlia/sketches/7nTFE9cOk"></iframe>

<script type="module">

    const iframe  = document.getElementById (`Grid attempt 2`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

This looked much better! However I am still not sure on how to move the squares so it doesn't stick to the top and left side of the canvas. I also just realized I can also use lines using the draw() function instead of tweaking and trying to centre the squares and such! Just a future note for next time, but at least I was able to think of multiple ways to create the same thing, which can lead to more creative possibilities in the future!
