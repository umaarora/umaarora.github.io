---
layout: page
title: F Around and Find Out
permalink: /faroundandfindout/
---

Pushing limits, chasing peaks, and collecting stories the hard way.

<div id="scroll-map" style="position: relative; height: 600vh;">
  <img id="map-img" src="/assets/images/world-map.jpg"
       style="width:100%; position: sticky; top: 0; transform-origin: top left;" />
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/ScrollTrigger.min.js"></script>

<script>
gsap.registerPlugin(ScrollTrigger);

const map = document.getElementById("map-img");

const tl = gsap.timeline({
  scrollTrigger: {
    trigger: "#scroll-map",
    start: "top top",
    end: "bottom bottom",
    scrub: true,
    pin: true,
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
  duration: 1
});
</script>


<!--

<div id="scroll-map" style="position: relative; height: 200vh;">
  <img id="map-img" src="/assets/images/world-map.jpg" style="width:100%; position: sticky; top:0;" />
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/ScrollTrigger.min.js"></script>

<script>
gsap.registerPlugin(ScrollTrigger);

const regions = [
  {
    scroll: "20%",
    zoom: 8,
    x: -650,
    y: -410,
    url: "/heron-island"
  },
  {
    scroll: "40%",
    zoom: 7.5,
    x: -250,
    y: -330,
    url: "https://bangaloremirror.indiatimes.com/opinion/sunday-read/on-top-of-the-world/articleshow/53890829.cms"
  },
  {
    scroll: "60%",
    zoom: 8,
    x: -480,
    y: -290,
    url: "/haleakala"
  },
  {
    scroll: "80%",
    zoom: 8,
    x: -130,
    y: -220,
    url: "/mont-blanc"
  },
  {
    scroll: "100%",
    zoom: 7.5,
    x: -40,
    y: -190,
    url: "/white-mountains"
  }
];

regions.forEach(({scroll, zoom, x, y, url}) => {
  ScrollTrigger.create({
    trigger: "#scroll-map",
    start: scroll,
    onEnter: () => {
      gsap.to("#map-img", {
        duration: 1,
        scale: zoom,
        x: x,
        y: y
      });
      document.getElementById("map-img").style.cursor = "pointer";
      document.getElementById("map-img").onclick = () => window.location.href = url;
    }
  });
});
</script>

-->
