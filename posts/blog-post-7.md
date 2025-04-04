---
title: Using p5.js in Static Folder
published_at: 2025-04-3
snippet:
disable_html_sanitization: true
allow_math: true
---

<script src="./scripts/p5.js"></script>

<canvas id="p5_example"></canvas>

<script>
    const cnv = document.getElementById ("p5_example")
    const w = cnv.parentNode.scrollWidth
    const h = w * 9 / 16

    let circle = {
        x = 200,
        y: 200,
        size: 50,
        phase: 0,
    };

    let col1 = '#D6F2E3';
    let col2 = '#EECDED';

    function setup () {
        createCanvas (w, h, P2D, cnv)
    }

    function draw () {
        console.log (frameCount)
        background('blue')

        circle.size = 50 + sin(circle.phase) * 25;

        fill (100, 150, 255);
        noStroke();
        ellipse(circle.x, circle.y, circle.size, circle.size);

        circle.phase += 0.1;
        
    }
    
</script>
