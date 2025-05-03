---
title: Zany
published_at: 2025-04-29
snippet:
disable_html_sanitization: true
allow_math: true
---

# In Sianne Ngai's essay she writes: "Unlike the interesting, the zany really works against its constraints." What do you think she means by this?

Means that zany isn't careful or calm. Interesting tends to stay controlled and neat without fighting them. However, zany is more messy and unpredictable. It breaks expectations and rules, and makes things actually unstable rather than just analyzing them.

### In what ways would you consider the chaotic and the zany to be similar? In what ways are they different?

I think mainly both being unstable, messy and full of unexpected behavior. However I think chaotic is way more random and has less purpose, but zany has more purpose, just doing more things at once than what you would usually expect.

### In what ways would you consider your AT2 to be zany?

I think the fact its constantly, growing, glitching, decaying and regrowing, there isn't a single moment where thigngs are still. The branches also don't grow normally, theres a lot of randomness and bias, especially with the sound being kinda crazy.

### What might be some ways to make your AT2 more zany?

I feel like I could add more exaggerated physics rather than try being more natural, as well as the angles of which branches grow, I tried to keep them within a certain range so it didn't look too messy, but I could definitely change that to be more zany. I could have weirder sound changes or bursts of branches, or do something with the color.

# Assignment 2 and Where It Uses and How It:

### Variables

I use variables to store the colonies, branches, oscillator types, sway amounts, sway rate, colors, I could keep going on forever. It just stores information so I could use it later.

### Iteration

A lot of for loops are used to create the branches, most evidently the starting branches. I also use it to go through all the positions in a certain array (aka to go through the branches array). Most used for to check certain states of each branch, and make something happen (grow/glitch) based on the state of the branch.

### Functions

I used p5.js functions like setup(), draw(), etc but also made custom functions like spawnColony(). This was very useful because I could call it anytime and I didn't have to keep rewriting my code.

### Boolean Logic

I used it to check if a the colonies length is over the max allowed of colonies, I used it to check if branches were finished growing, and so many other more. It lets my code make decisions automatically and could make thigns happen when certain conditions were met.

### Arrays

I used it to store colonies, its branches, etc. Lets me group related things together and loop through them easily so I dont have to manually give variable names to every single thing.

### Classes

My main class was the Branch class and it defined how it growed, glitched, how it spawns new ones and how it glitches. It let me make branches that share the same set of rules, but had the potential to behave differently

### Recursion

Recursion was a main part of my assignment. For example, I used child.update() int he update() function, and the child.show() inside show(). It let my assignment naturally grow this complex colonies without needing to know how many branches deep it goes. Each branch takes care of updating its children automatically and made it super easy to make the structures.

### Responds to the Chosen Text

It responds to Sheldrake's ideas about how fungi live with networtks, growth and branching forms. My project mimics the fungul growth patterns, branching outwards, sprouts sprouting from other sprouts and not having a single brain the controls it. Each branch grows from its parent, and uses physics and randomness to do the rest. These colonies spread across the screen, overlapping, fading, glitching, regrowing, similar to fungal ecosystems. The glitching branches also represent the adaptability of fungi, showing that when conditions change, they don't die, they reorganize, regrow differently and adapt. The sound itself also behaves organically, bending and vibrating based on its environment, instead of it being methodical and mechanical. I basically designe a living system that grows and decays, adapting and showing how growth can be messy, responsive and decentralized.

### Is Considered Post Digital

I blended digital coding with unstable behabiors. I took branches and sounds, but integrated weird behaviors like wobbles, glitches and mouse bias. I dont hind randomness or errors, isntead I embrace them and let them contribute to the project, which helps it become fmore chaotic.
