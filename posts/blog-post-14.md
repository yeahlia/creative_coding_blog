---
title: Web Audio API
published_at: 2025-04-20
snippet:
disable_html_sanitization: true
allow_math: true
---

# How Will I Make Use of Sound in Assignment 2?

To function in the chaotic aesthetic register, I need to balance between predictability and unpredictability. If the sound is too ordered it becomes monotonous and predictable, but if it's too random then it becomes noise. I aim to maintain effective complexity by implementing some structure, but also unpredictableness. I plan to do this by having simple cause and effect noises like when the user clicks, it makes a sound. This follows peoples regular perception of sound, when something happens, a sound forms. But I also want this to be more chaotic by randomly glitching the sound. I also want the growth sounds to be more melodic, while the death sounds may be more noisy. As music is definitely seen as more structured, and noise is more random and unpredictable. I don't want any voice as it is often tied to intentionallity, as people speaking is often always intentional. I want to keep this project more strange and chaotic rather than familiar, by avoiding anything that is voiced.

I want users to be de-familiarized by breaking musical expectations as the branches grow, make the user unsure of if the system is alive or decaying, and create strangeness by the constant states of decay and growth.

To conclude, I want my assignment to play a droning hum as a background noise, and some melodic notes as the branches grow. When a branch reaches a state of death, there is a distorted glitch sound, and while it retracts, there is sped up noise. There will also be a sound for when the user clicks and spawns a new node.

NOTE FROM FUTURE SELF: I did not do this because I saw that oscillators and synths were an option and got really excited.

# Implementation of a Sound Design Experiment

This was my test of doing sound design using web audio API

```js
let audioContext;
let oscillator;
let notes = [261.63, 293.66, 329.63, 349.23, 392.0]; // notes from the C major scale
let currentNote = 0;

function setup() {
  createCanvas(400, 400);

  audioContext = new (window.AudioContext || window.webkitAudioContext)();

  oscillator = audioContext.createOscillator(); // create the sound
  oscillator.type = "sine"; // sine wave
  oscillator.frequency.setValueAtTime(
    notes[currentNote],
    audioContext.currentTime
  ); // set first note

  let volume = audioContext.createGain(); // make a gain node
  volume.gain.setValueAtTime(0.1, audioContext.currentTime); // low volume

  oscillator.connect(volume); // connect oscillator to volume
  volume.connect(audioContext.destination); // connect volume to speakers

  oscillator.start(); // start the sound

  setInterval(changeNote, 2000); // change note every 2 seconds
}

function changeNote() {
  currentNote = (currentNote + 1) % notes.length; // move to next note in array
  oscillator.frequency.setValueAtTime(
    notes[currentNote],
    audioContext.currentTime
  );
}
```
