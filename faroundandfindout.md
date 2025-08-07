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
    /* This will be scaled down to counteract the parent's scale */
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

<div style="text-align: center; margin-top: 40px;">
  <a href="/faroundandfindout/" style="display: inline-block; padding: 15px 30px; text-decoration: none; border-radius: 5px; font-weight: bold; font-size: 16px; border: 2px solid currentColor;">Back to Top</a>
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
  
  // Calculate viewport center
  const viewportCenterX = containerWidth / 2;
  const viewportCenterY = containerHeight / 2;
  
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

  // Initially hide all pins
  gsap.set(Object.values(pins), { display: 'none' });

  zooms.forEach((z, i) => {
    const base = i * 2;
    
    // Calculate translation to center the target point in viewport
    const translateX = viewportCenterX - (z.x * z.zoomScale);
    const translateY = viewportCenterY - (z.y * z.zoomScale);

    // Zoom in on the map and pin
    tl.to([map, z.pin], { 
      scale: z.zoomScale, 
      x: translateX, 
      y: translateY, 
      duration: 1 
    }, base);
    
    // Counter-scale the pin's image to keep its size constant
    tl.to(z.pin.querySelector('img'), {
      scale: 1 / z.zoomScale,
      duration: 1
    }, base);
    
    // Position pin at viewport center when zoom reaches 6x
    tl.set(z.pin, { 
      left: `${viewportCenterX}px`,
      top: `${viewportCenterY}px`,
      display: "block" 
    }, base + (6 / z.zoomScale));
    
    // Hide pin when zoom drops below 6x during zoom out
    tl.set(z.pin, { display: "none" }, base + 1 + (1 - 6 / z.zoomScale));

    // Zoom out the map and pin
    tl.to([map, z.pin], { 
      scale: 1, 
      x: 0, 
      y: 0, 
      duration: 1 
    }, base + 1);

    // Reset the pin's image scale
    tl.to(z.pin.querySelector('img'), {
      scale: 1,
      duration: 1
    }, base + 1);
    
    // Reset pin position after zoom out
    tl.call(() => setPinPositions(), [], base + 2);
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