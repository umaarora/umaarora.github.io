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

<!-- ICONS -->
    <a href="/heron-island" class="map-pin" id="pin-heron" target="_blank">
      <img src="/assets/images/scuba.jpg" alt="Heron Island" />
    </a>
    <a href="https://bangaloremirror.indiatimes.com/opinion/sunday-read/on-top-of-the-world/articleshow/53890829.cms" class="map-pin" id="pin-kili" target="_blank">
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
pins.heron.style.left = "1115px";
pins.heron.style.top = "378px";

pins.kili.style.left = "722px";
pins.kili.style.top = "310px";

pins.haleakala.style.left = "78px";
pins.haleakala.style.top = "232px";

pins.montblanc.style.left = "630px";
pins.montblanc.style.top = "141px";

pins.white.style.left = "361px";
pins.white.style.top = "153px";

// Create scroll regions (each region = 100vh)
const zooms = [
  { scale: 6.5, x: -1115, y: -378, pin: pins.heron },
  { scale: 6.5, x: -722, y: -310, pin: pins.kili },
  { scale: 7,   x: -78,  y: -232, pin: pins.haleakala },
  { scale: 6.5, x: -630, y: -141, pin: pins.montblanc },
  { scale: 6.5, x: -361, y: -153, pin: pins.white }
];

// Hide all pins initially
Object.values(pins).forEach(pin => pin.style.display = "none");

const tl = gsap.timeline({
  scrollTrigger: {
    trigger: "#scroll-map-wrapper",
    start: "top top",
    end: "bottom top",
    scrub: true,
    pin: "#scroll-map",
    anticipatePin: 1
  }
});

// Heron Island
tl.set(pins.heron, { display: "block" }, 0)
  .to(map, {
    scale: 6.5,
    x: -1115,
    y: -378,
    duration: 1
  }, 0)
  .set(pins.heron, { display: "none" }, 1);

// Kilimanjaro
tl.set(pins.kili, { display: "block" }, 1)
  .to(map, {
    scale: 6.5,
    x: -722,
    y: -310,
    duration: 1
  }, 1)
  .set(pins.kili, { display: "none" }, 2);

// Haleakala
tl.set(pins.haleakala, { display: "block" }, 2)
  .to(map, {
    scale: 7,
    x: -78,
    y: -232,
    duration: 1
  }, 2)
  .set(pins.haleakala, { display: "none" }, 3);

// Mont Blanc
tl.set(pins.montblanc, { display: "block" }, 3)
  .to(map, {
    scale: 6.5,
    x: -630,
    y: -141,
    duration: 1
  }, 3)
  .set(pins.montblanc, { display: "none" }, 4);

// White Mountains
tl.set(pins.white, { display: "block" }, 4)
  .to(map, {
    scale: 6.5,
    x: -361,
    y: -153,
    duration: 1
  }, 4)
  // Don't hide this one unless you want the final view cleared
  .set(pins.white, { display: "none" }, 5);

</script>

