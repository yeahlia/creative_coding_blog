---
title: Assignment 3
published_at: 2025-06-10
snippet:
disable_html_sanitization: true
allow_math: true
---

# Music Helper 2000

I have finally finished my Assignment 3!

You can use it [here](https://liaaguilar.github.io/musichelper/).

### Final Reflection

Music Helper 2000 is a web-based creative tool designed to support improvisational music-making. Built in HTML, CSS, and JavaScript using Pitchy.js for pitch detection and SVG for the fretboard visualisation, it listens to live audio input, detects the most likely key, and displays related notes on a colour-coded fretboard. It offers users a choice of musical modes (like Dorian or Mixolydian), and allows them to see the relationships between their input and the music theory surrounding it. While the pitch detection isn't always accurate, that’s part of the point, as its role is to guide, not tell you what to play. And sometimes, those “mistakes” become the spark for creative breakthroughs.

The design philosophy behind Music Helper 2000 os spomething that is not flashy,it’s something that gently catches your attention and makes you thnik. Something interesting. This project reflects this philosopgy, the interface is quiet and minimal. It’s a reflective layer over live sound, encouraging the user to connect what they’re hearing with what they’re seeing, and to ask questions about what’s musically possible rather than what’s musically correct.

From a technical perspective, the tool operates on a clean and modular foundation. Pitchy.js handles incoming microphone data, guesses the pitch, and stores the most frequent notes over time. When the user hits “stop,” the app analyses the dominant notes and uses that to guess the musical key. It then maps the notes of the selected mode onto the SVG fretboard and has the option to add custom styles like colour coding and note labels. Simple fade transitions and clean layout choices make the tool feel smooth and unobtrusive.

This whole process reflects mycelial creativity, both in how the project was developed and how it’s used. Development was non-linear and exploratory, with features branching out, being tested, and sometimes cut (like the chord view or scale degrees). The final result grew omnidirectionally, layering functions bit by bit while staying sensitive to what actually served the user. It also supports mycelial growth within the band: during jams or rehearsals, it helps resolve confusion, reinforces confidence, and offers subtle paths forward. By not being strict or prescriptive, it gives each player the freedom to create while still feeling supported—like a mycelial network offering nutrients and signals invisibly beneath the surface.

Finally, Music Helper 2000 is grounded in the needs and values of my community of practice—my band. It was designed to reflect how we actually work: intuitively, collaboratively, and often without formal theory. This tool doesn’t teach, it joins in. It reflects our domain (improvised live music), our repertoire (looping, jamming, expressive playing), and our values (support, accessibility, and open-ended creativity). It's not just an aid—it’s part of our musical environment now. A quiet contributor to the noise we make together.
