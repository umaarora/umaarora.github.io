---
layout: page
title: F Around and Find Out
permalink: /faroundandfindout/
---

Pushing limits, chasing peaks, and collecting stories the hard way.

<style>
.map-pin {
  position: absolute;
  width: 32px;
  height: 32px;
  transform: translate(-50%, -100%);
  display: none;
  z-index: 10;
}

.map-pin img {
  width: 100%;
  height: auto;
}
</style>


<div id="scroll-map-wrapper" style="height: 600vh;">
  <div id="scroll-map" style="position: relative; height: 100vh;">
    <img id="map-img" src="/assets/images/world-map.jpg"
         style="width:100%; position: sticky; top: 0; transform-origin: top left;" />

<!-- 🔧 TEST PIN HERE -->
    <a href="#" class="map-pin" style="display: block; left: 1000px; top: 500px;">
      <img src="/assets/images/summit.jpeg" />
    </a>

<!-- ICONS -->
    <a href="/heron-island" class="map-pin" id="pin-heron" target="_blank">
      <img src="/assets/images/scuba.jpg" alt="Heron Island" />
    </a>
    <a href="/kilimanjaro" class="map-pin" id="pin-kili" target="_blank">
      <img src="/assets/images/summit.jpeg" alt="Kilimanjaro" />
    </a>
    <a href="/haleakala" class="map-pin" id="pin-haleakala" target="_blank">
      <img src="/assets/images/hike.jpg" alt="Haleakala" />
    </a>
    <a href="/mont-blanc" class="map-pin" id="pin-montblanc" target="_blank">
      <img src="/assets/images/hike.jpg" alt="Mont Blanc" />
    </a>
    <a href="/white-mountains" class="map-pin" id="pin-white" target="_blank">
      <img src="/assets/images/summit.jpeg" alt="White Mountains" />
    </a>


  </div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/ScrollTrigger.min.js"></script>

<script>
gsap.registerPlugin(ScrollTrigger);

const map = document.getElementById("map-img");
const pins = {
  heron: document.getElementById("pin-heron"),
  kili: document.getElementById("pin-kili"),
  haleakala: document.getElementById("pin-haleakala"),
  montblanc: document.getElementById("pin-montblanc"),
  white: document.getElementById("pin-white")
};

// Set icon positions relative to the map (absolute inside container)
pins.heron.style.left = "2304px";
pins.heron.style.top = "1064px";

pins.kili.style.left = "1565px";
pins.kili.style.top = "788px";

pins.haleakala.style.left = "596px";
pins.haleakala.style.top = "703px";

pins.montblanc.style.left = "1512px";
pins.montblanc.style.top = "490px";

pins.white.style.left = "1331px";
pins.white.style.top = "426px";


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

// Animation + pin control
tl.to(map, {
  scale: 6.5,
  x: -2304,
  y: -1064,
  duration: 1,
  onStart: () => pins.heron.style.display = "block",
  onReverseComplete: () => pins.heron.style.display = "none"
})
.to(map, {
  scale: 6.5,
  x: -1565,
  y: -788,
  duration: 1,
  onStart: () => pins.kili.style.display = "block",
  onReverseComplete: () => pins.kili.style.display = "none"
})
.to(map, {
  scale: 7,
  x: -596,
  y: -703,
  duration: 1,
  onStart: () => pins.haleakala.style.display = "block",
  onReverseComplete: () => pins.haleakala.style.display = "none"
})
.to(map, {
  scale: 6.5,
  x: -1512,
  y: -490,
  duration: 1,
  onStart: () => pins.montblanc.style.display = "block",
  onReverseComplete: () => pins.montblanc.style.display = "none"
})
.to(map, {
  scale: 6.5,
  x: -1331,
  y: -426,
  duration: 1,
  onStart: () => pins.white.style.display = "block",
  onReverseComplete: () => pins.white.style.display = "none",
  onComplete: () => {
    gsap.set(map, { clearProps: "position,top,left" }); // optional reset safety
  }
});
</script>

