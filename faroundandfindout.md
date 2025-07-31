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

// Create scroll regions (each region = 100vh)
const zooms = [
  { scale: 6.5, x: -2304, y: -1064, pin: pins.heron },
  { scale: 6.5, x: -1565, y: -788, pin: pins.kili },
  { scale: 7,   x: -596,  y: -703, pin: pins.haleakala },
  { scale: 6.5, x: -1512, y: -490, pin: pins.montblanc },
  { scale: 6.5, x: -1331, y: -426, pin: pins.white }
];

// Apply zoom + show/hide pin
zooms.forEach((z, i) => {
  gsap.to(map, {
    scrollTrigger: {
      trigger: "#scroll-map-wrapper",
      start: `${i * 100}vh top`,
      end: `${(i + 1) * 100}vh top`,
      scrub: true,
      onEnter: () => z.pin.style.display = "block",
      onLeave: () => z.pin.style.display = "none",
      onEnterBack: () => z.pin.style.display = "block",
      onLeaveBack: () => z.pin.style.display = "none",
    },
    scale: z.scale,
    x: z.x,
    y: z.y,
    ease: "none"
  });
});
</script>
