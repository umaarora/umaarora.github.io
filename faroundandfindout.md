---
layout: page
title: F Around and Find Out
permalink: /faroundandfindout/
---

Pushing limits, chasing peaks, and collecting stories the hard way.

<div id="scroll-map-wrapper" style="height: 600vh;">
  <div id="scroll-map" style="position: relative; height: 100vh;">
    <img id="map-img" src="/assets/images/world-map.jpg"
         style="width:100%; position: sticky; top: 0; transform-origin: top left;" />
  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/ScrollTrigger.min.js"></script>

<script>
gsap.registerPlugin(ScrollTrigger);

const map = document.getElementById("map-img");

const tl = gsap.timeline({
  scrollTrigger: {
    trigger: "#scroll-map-wrapper",
    start: "top top",
    end: "bottom top", // stop at end of wrapper
    scrub: true,
    pin: "#scroll-map", // pin just the image container
    anticipatePin: 1
  }
});

// Add animations for each region
tl.to(map, {
  scale: 8,
  x: -650,
  y: -410,
  duration: 1
})
.to(map, {
  scale: 7.5,
  x: -250,
  y: -330,
  duration: 1
})
.to(map, {
  scale: 8,
  x: -480,
  y: -290,
  duration: 1
})
.to(map, {
  scale: 8,
  x: -130,
  y: -220,
  duration: 1
})
.to(map, {
  scale: 7.5,
  x: -40,
  y: -190,
  duration: 1,
  onComplete: () => {
    gsap.set(map, { clearProps: "position,top,left" }); // optional reset safety
  }
});
</script>


