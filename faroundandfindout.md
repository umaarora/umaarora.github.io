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

<div id="scroll-map-wrapper" style="height: 1000vh;">
  <div id="scroll-map" style="position: relative; height: 100vh; overflow: hidden;">
    <img id="map-img" src="/assets/images/world-map.jpg"
     style="width: 2560px; height: auto; position: sticky; top: 0; transform-origin: center center;" />

    <!-- ICONS -->
    <a href="/heron-island" class="map-pin" id="pin-heron" target="_blank">
      <img src="/assets/images/scuba.jpg" alt="Heron Island" />
    </a>
    <a href="https://bangaloremirror.indiatimes.com/opinion/sunday-read/on-top-of-the-world/articleshow/53890829.cms" class="map-pin" id="pin-kili" target="_blank">
      <img src="/assets/images/mountain.png" alt="Kilimanjaro" />
    </a>
    <a href="/haleakala" class="map-pin" id="pin-haleakala" target="_blank">
      <img src="/assets/images/hike.jpg" alt="Haleakala" />
    </a>
    <a href="/mont-blanc" class="map-pin" id="pin-montblanc" target="_blank">
      <img src="/assets/images/hike.jpg" alt="Mont Blanc" />
    </a>
    <a href="/white-mountains" class="map-pin" id="pin-white" target="_blank">
      <img src="/assets/images/mountain.png" alt="White Mountains" />
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
const naturalWidth = 2560;

function getScaleFactor() {
  return map.clientWidth / naturalWidth;
}

function setPinPositions() {
  const s = getScaleFactor();
  pins.heron.style.left = `${2159 * s}px`;
  pins.heron.style.top = `${655 * s}px`;
  pins.kili.style.left = `${1544 * s}px`;
  pins.kili.style.top = `${661 * s}px`;
  pins.haleakala.style.left = `${170 * s}px`;
  pins.haleakala.style.top = `${482 * s}px`;
  pins.montblanc.style.left = `${1343 * s}px`;
  pins.montblanc.style.top = `${313 * s}px`;
  pins.white.style.left = `${772 * s}px`;
  pins.white.style.top = `${329 * s}px`;
}

function buildTimeline() {
  ScrollTrigger.getAll().forEach(t => t.kill());
  const scale = getScaleFactor();
  const mapRect = map.getBoundingClientRect();
  const naturalHeight = mapRect.height / scale; // Calculate natural height from current dimensions
  
  // With center transform origin, we need to offset from the center of the image
  const centerX = (naturalWidth * scale) / 2;
  const centerY = (naturalHeight * scale) / 2;
  
  const zooms = [
    { pin: pins.heron, x: centerX - (2159 * scale), y: centerY - (655 * scale), zoomScale: 6.5 },
    { pin: pins.kili, x: centerX - (1544 * scale), y: centerY - (661 * scale), zoomScale: 6.5 },
    { pin: pins.haleakala, x: centerX - (170 * scale), y: centerY - (482 * scale), zoomScale: 7 },
    { pin: pins.montblanc, x: centerX - (1343 * scale), y: centerY - (313 * scale), zoomScale: 6.5 },
    { pin: pins.white, x: centerX - (772 * scale), y: centerY - (329 * scale), zoomScale: 6.5 }
  ];

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

  zooms.forEach((z, i) => {
    const base = i * 2;

    tl.to(map, { 
      scale: z.zoomScale, 
      x: z.x, 
      y: z.y, 
      duration: 1 
    }, base);
    tl.set(z.pin, { display: "block" }, base + 0.3);
    tl.set(z.pin, { display: "none" }, base + 1);
    tl.to(map, { scale: 1, x: 0, y: 0, duration: 1 }, base + 1);
  });
}

// Use ResizeObserver to rebuild after the map image resizes or loads
const observer = new ResizeObserver(() => {
  setPinPositions();
  buildTimeline();
});
observer.observe(map);

// In-case image was already loaded before JS runs
if (map.complete) {
  setPinPositions();
  buildTimeline();
}
</script>