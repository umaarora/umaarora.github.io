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

const naturalWidth = 2560; // natural pixel width of your image

function getScaleFactor() {
  return map.clientWidth / naturalWidth;
}

// Set icon positions relative to the map (absolute inside container)
function setPinPositions() {
  const scaleFactor = getScaleFactor();

  pins.heron.style.left = `${2374 * scaleFactor}px`;
  pins.heron.style.top = `${813 * scaleFactor}px`;

  pins.kili.style.left = `${1534 * scaleFactor}px`;
  pins.kili.style.top = `${666 * scaleFactor}px`;

  pins.haleakala.style.left = `${175 * scaleFactor}px`;
  pins.haleakala.style.top = `${499 * scaleFactor}px`;

  pins.montblanc.style.left = `${1348 * scaleFactor}px`;
  pins.montblanc.style.top = `${306 * scaleFactor}px`;

  pins.white.style.left = `${775 * scaleFactor}px`;
  pins.white.style.top = `${330 * scaleFactor}px`;
}

window.addEventListener("load", setPinPositions);
window.addEventListener("resize", setPinPositions);

// Create scroll regions (each region = 100vh)
function getZooms() {
  const scaleFactor = getScaleFactor();
  return [
    { scale: 6.5, x: -2374 * scaleFactor, y: -813 * scaleFactor, pin: pins.heron },
    { scale: 6.5, x: -1534 * scaleFactor, y: -666 * scaleFactor, pin: pins.kili },
    { scale: 7,   x: -175  * scaleFactor, y: -499 * scaleFactor, pin: pins.haleakala },
    { scale: 6.5, x: -1348 * scaleFactor, y: -306 * scaleFactor, pin: pins.montblanc },
    { scale: 6.5, x: -775  * scaleFactor, y: -330 * scaleFactor, pin: pins.white }
  ];
}

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
    scale: 6.5 * getScaleFactor(),
    x: -2374 * getScaleFactor(),
    y: -813 * getScaleFactor(),
    duration: 1
  }, 0)
  .set(pins.heron, { display: "none" }, 1);

// Kilimanjaro
tl.set(pins.kili, { display: "block" }, 1)
  .to(map, {
    scale: 6.5 * getScaleFactor(),
    x: -1534 * getScaleFactor(),
    y: -666 * getScaleFactor(),
    duration: 1
  }, 1)
  .set(pins.kili, { display: "none" }, 2);

// Haleakala
tl.set(pins.haleakala, { display: "block" }, 2)
  .to(map, {
    scale: 7 * getScaleFactor(),
    x: -175 * getScaleFactor(),
    y: -499 * getScaleFactor(),
    duration: 1
  }, 2)
  .set(pins.haleakala, { display: "none" }, 3);

// Mont Blanc
tl.set(pins.montblanc, { display: "block" }, 3)
  .to(map, {
    scale: 6.5 * getScaleFactor(),
    x: -1348 * getScaleFactor(),
    y: -306 * getScaleFactor(),
    duration: 1
  }, 3)
  .set(pins.montblanc, { display: "none" }, 4);

// White Mountains
tl.set(pins.white, { display: "block" }, 4)
  .to(map, {
    scale: 6.5 * getScaleFactor(),
    x: -775 * getScaleFactor(),
    y: -330 * getScaleFactor(),
    duration: 1
  }, 4)
  // Don't hide this one unless you want the final view cleared
  .set(pins.white, { display: "none" }, 5);

</script>

