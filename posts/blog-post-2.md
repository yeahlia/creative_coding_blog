---
title: Rafaël Rozendaal and Replication
published_at: 2025-03-06
snippet:
disable_html_sanitization: true
allow_math: true
---

# Missing by Rafaël Rozendaal

### How do I think the code works?

I think that the code first begins with creating a canvas that is dependent on the size of the window, as I noticed when I changed the window size, the amount of squares change. It then creates a 'grid' of squares (with the minimum being a 3x3 grid) with some of them being gray and some of them being colored. The colored squares then move one at a time across the gray areas, colored squares never overlapping with other colored squares.

I think they used a randomizer for the color of the colored squares, but kept it between certain choices to keep the aesthetic and colors that Rozendaal wanted. Then I think it creates a grid by drawing squares and then randomizes which one is animated.

### Concepts needed to replicate the work

I think that I'll need to understand arrays and lerps in order to replicate Rozendaal's work. Learning how to animate using framecounts as well as conditional logic to ensure that no errors occur.

### Resources that will help me learn these concepts

Using the resource tab in p5js would be extremely helpful, as well as the Coding Train on youtube. If I have any specific questions or need things explained simpler, I tend to use ChatGPT (sorry) to explain things. I also look at exisiting code, whether that be on Reddit or Github, and ask ChatGPT to explain what lines of code I don't understand.

### Replicating the Code

<iframe id="Array" src="https://editor.p5js.org/yeahlia/sketches/M95TcrHh5"></iframe>

<script type="module">

    const iframe  = document.getElementById (`Array`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

This code basically uses the 'square' array to store objects that have the position on the canvas with the x and y axis. It then loops through the squares in that array and draws it using the stored color as well as its x and y position. I noticed in Rozendaals work that every time I refreshed the page the squares would be different colors, so I decided to use a randomizer in my code as well, using a 'color' array to store the color palette, and using the randomizer so each square would choose a random color.

In order to create this code, I used looked through p5.js forum and Reddit to look for any similar questions that has previously been asked, and looked through the answers to see if it was what I needed. I also watched a video on youtube on the basics of arrays, which helped me really grasp the concept.
