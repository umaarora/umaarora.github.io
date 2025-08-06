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
     style="width: 2560px; height: auto; position: sticky; top: 0; transform-origin: top left;" />

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
  pins.heron.style.left = `${2374 * s}px`;
  pins.heron.style.top = `${813 * s}px`;
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
  const mapContainer = document.getElementById("scroll-map");
  const containerWidth = mapContainer.clientWidth;
  const containerHeight = mapContainer.clientHeight;
  
  const zooms = [
    { pin: pins.heron, x: 2374 * scale, y: 813 * scale, zoomScale: 6.5 },
    { pin: pins.kili, x: 1544 * scale, y: 661 * scale, zoomScale: 6.5 },
    { pin: pins.haleakala, x: 170 * scale, y: 482 * scale, zoomScale: 7 },
    { pin: pins.montblanc, x: 1343 * scale, y: 313 * scale, zoomScale: 6.5 },
    { pin: pins.white, x: 772 * scale, y: 329 * scale, zoomScale: 6.5 }
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

  // Make all pins visible from the start
  gsap.set(Object.values(pins), { display: 'block', opacity: 1 });

  zooms.forEach((z, i) => {
    const base = i * 2;
    
    // Calculate translation to center the target point in viewport
    const translateX = (containerWidth / 2) - (z.x * z.zoomScale);
    const translateY = (containerHeight / 2) - (z.y * z.zoomScale);

    // Zoom in: transform both map and the current pin together
    tl.to([map, z.pin], { 
      scale: z.zoomScale, 
      x: translateX, 
      y: translateY, 
      duration: 1 
    }, base);
    
    // Zoom out: reset both map and current pin
    tl.to([map, z.pin], { 
      scale: 1, 
      x: 0, 
      y: 0, 
      duration: 1 
    }, base + 1);
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
---
This video shows how to create a scroll-based zoom effect using GSAP's ScrollTrigger plugin, which is similar to what you're trying to achieve with your map.