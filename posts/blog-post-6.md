---
title: Starting Assignment 1
published_at: 2025-03-21
snippet:
disable_html_sanitization: true
allow_math: true
---
# How Does My Idea Use Each of the Following Concepts:
### Variables
My idea uses variables to store information. For example, variables will store the properties of the bubbles such as its size, position and color, as well as store the sounds that play for all the interactions. These variables will allow my to modify and change the current state of bubbles throughout the interaction.

### Functions
It will help organize the different interactions and behaviors of certain things. This includes creating new bubbles when the user clicks on the canvas, the growth of the bubbles when long-pressed, and checking if these shapes are colliding. It will help me organize, understand and maintain the code as each 'task' can basically be broken down and seperated using functions.

### Iteration
Iteration will help me avoid long code, like using a iterative loop to create bubbles at the start, instead of manually coding them in. I can also use to check certain states of objects in an easier way and will make the program more efficient. This is particularly useful in my idea for if the user creates a lot of bubbles/blobs, and the program needs to be constantly checking if it has been clicked or collided with another object.

### Boolean Logic
I will use this to make certain decisions in my assignment based on true/false. Something like whether the user click is within the boundaries of a bubble (true if it is, false if not), and then an action will occur based on the outcome, in this case, if it is true, the bubble will burst. I can also use it to determine if any of the bubbles collide, or if the user is long clicking a bubble to trigger its growth.

### Arrays
Arrays will help me store and manage objects, which in my idea, will be bubbles. Each bubble on the screen will have its own properties and instead of creating a bunch of seperate variables for each one, I will just store this information in an array. It allows my code to be more easily found and read, and that means I could also easily add, remove and update the objects as the user interacts with my work. I will also use it to store information like the possible colors that each bubble can be, then use a randomizer to choose a random position in the color array.

### Classes
I will classes in my assignment to define the properties and behaviors of the bubbles. It allows me to organize the code and create new bubbles with all the necessary properties and behaviors without having to reenter the code a bunch of times. It allows me to reuse code really easily, which helps me manage the interactions that happen within the canvas.

# Assignment 1 Draft:

<iframe id="cuteDraft1" src="https://editor.p5js.org/yeahlia/sketches/GxC7-T_cK"></iframe>

<script type="module">

    const iframe  = document.getElementById (`cuteDraft1`)
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width 

</script>

### What Communities and Learning Resources Did You Draw on to do the Bulk of Your Learning?
The main thing that really helped me whilst learning was my mother and my brother. They both code as jobs and are familiar with a variety of coding languages, javascript being one of them. They were able to sit down and help me and explained to me their thought process and how I could translate my ideas into code. It was really helpful having someone there to give me immediate feedback on what I was doing, as well as explain my mistakes as it was happening. I was also able to annoy them with questions without feeling bad lol! Other than that, I'm not sure if this is the best practice, but honestly ChatGPT really helped me. I used the p5.js library and online forums to learn what the different methods are, and the general explanation, as well as guidelines on what methods and functions to use/make, but I never really knew how to use them. Like I knew what they did, but when I was writing code without any help, I just had no idea what to write. By putting my code through ChatGPT, it was able to tell me what I was missing (which was so useful when I was getting frustrated and stuck), and it helped me understand what I was doing. If it told me to do something, I asked what it did and why I need to use it which was extremely helpful. I was also able to make my code more efficient using this, I kept asking if there were ways to help make my code more efficient, and it really helped as I noticed a lot of my code was repeating, but I didn't know what to do to avoid that.

### What Aspects Have You Enjoyed the Most About This Process?  What Have You Found to be Most Surprising?
I really like learning something new, I think when I finally get something or my code works how I want I get really excited and proud of myself. I didn't realize how rewarding it can be once you understand certain concepts (but of course understanding them is the most difficult part).

### What Aspects Have You Struggled with the Most?  What Have You Found the Most Confusing? 
In general, I think the learning aspect has been the hardest for me. I can't really sit still in long classes and its hard for me to focus, so I tend to zone out and then I feel super behind even if I miss like 10 minutes class. I think in terms of the content, I get the most confused of the difference between a function and a class, but also the vocabulary in general. I hear a lot of new vocabulary and I forget what they are, and then I get lost because I'm trying to search up what an attribute is, but we've already moved on and I lose part of that lesson, which gets pretty frustrating. I also think the frameCount parts always confused me lol, but that's just a personal math issue.