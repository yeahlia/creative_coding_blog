---
title: Creating my Cute Assignment!
published_at: 2025-03-22
snippet:
disable_html_sanitization: true
allow_math: true
---

This shows all my drafts to create the assignment, as well as the process on how I got there, my difficulties and just my general thoughts!

# Assignment Draft Version 2:

<iframe id="cuteDraft2" src="https://editor.p5js.org/yeahlia/sketches/3S1UhwX2x"></iframe>

<script type="module">

    const iframe  = document.getElementById (`cuteDraft2`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

I decided to do a few more things before the next class! I was able to figure out how to make sure that the bubbles don't spawn over each other when the canvas is first drawn. I used The Coding Train's [video](https://www.youtube.com/watch?v=XATr_jdh-44) to help me out. Since he uses more simpler code and my code uses more classes and functions, I had to figure out how to make it work with my code. I decided to make a variable that checks the same thing that The Coding Train does (the distance between the new circles and then existing ones) and found some ways to make it more efficient by using break; to stop the code once it sees if it is overlapping.

To make the bubbles grow when pressed, it was kind of difficult to figure out. I knew that I would need functions for when the mouse is pressed and released, but also I need the code to check if it is over a bubble, and only grow that specific one. This one really stumped me for a bit, mainly because I could think about what certain things needed to be done and what constraints etc., but I just didn't know how to translate my thoughts into code. I saw that there was already a grow() method, which really helped, but I had to figure out how to track the mouse interactions properly. I then remembered The Coding Train and how they used the radius and the distance to figure out if the bubbles were overlapping, and realized I could also use that to see if the mouse was overlapping!

Then I just assigned that bubble (if the mouse was over a bubble) to a variable, then in the draw() function, it checks if the variable is assigned, and if it is, it calls the grow() method and causes it to grow over time! But it didn't work! I got so annoyed and asked my mom and brother for help and they basically found out (after a very long time) that we needed to check if the specific bubble being pressed is the same one that was selected, which basically just makes sure that not very bubble grows. Lowkey still confused how the code all works together as a whole, but hey working at one thing at a time is working!

Now my next session will be (hopefully) allowing the users to click new circles in, adding sound and the bubbles disappearing when it hits the others. My original idea was for the bubbles to be kind of like blobs/organic shapes, but I think the calculations for those wuold be much more advanced that what I am currently capable of. To replace this, I kind of what the background to be moving in some way, maybe color shifting using lerp or just some slight variations, so I don't feel as if the canvas is static, or maybe make the bubbles jitter, but I'm not sure if that will affect the code a lot, so I'm most likely going to stick with the background moving.

# Assignment Draft Version 3:

<iframe id="cuteDraft3" src="https://editor.p5js.org/yeahlia/sketches/MAyvAB2lp"></iframe>

<script type="module">

    const iframe  = document.getElementById (`cuteDraft3`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

This time I added something where the user can click new circles in! Unfortunately I had to redo most of the code, but the old code really helped me understand what I needed to add to the new one! I added a variable that I use to let the computer know if the clicked spot has a bubble or not. To calculate this, I used my old code of sorting through all existing bubbles in the array, and calculating the radius distance to see if the mouse click is inside any bubbles. If it is, it sets that bubble to grow, lets the variable know that a bubble was clicked, and exits the loop, which is basically what my old code did.

However, if a bubble was not clicked, then I made a variable that assumes that a new bubble can be made there. The code repeats, checking the distance between mouse click and each bubble in the array, and if the position is valid, it adds a new bubble to the array!

Other than that, I also added code to make the background color lerp between 2 colors (which I hope to change to more). I used [this](https://editor.p5js.org/yeahlia/sketches/CelvRaf8c) existing code that I found and basically used the same code in mine!

 <!-- 
 how to add the sound
 how to do the click animation
 maybe animation of it popping, maybe disappear from the inside out
  -->
