---
layout: page
title: F Around and Find Out
permalink: /faroundandfindout/
---

Pushing limits, chasing peaks, and collecting stories the hard way.

<div id="scroll-map" style="position: relative; height: 200vh;">
  <img id="map-img" src="/assets/world-map.jpg" style="width:100%; position: sticky; top:0;" />
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/ScrollTrigger.min.js"></script>

<script>
gsap.registerPlugin(ScrollTrigger);

const regions = [
  {
    scroll: "20%",
    zoom: 8,
    x: -2200,
    y: -1100,
    url: "/heron-island"
  },
  {
    scroll: "40%",
    zoom: 7,
    x: -900,
    y: -800,
    url: "https://bangaloremirror.indiatimes.com/opinion/sunday-read/on-top-of-the-world/articleshow/53890829.cms"
  },
  {
    scroll: "60%",
    zoom: 8,
    x: -400,
    y: -400,
    url: "/haleakala"
  },
  {
    scroll: "80%",
    zoom: 8,
    x: -950,
    y: -500,
    url: "/mont-blanc"
  },
  {
    scroll: "100%",
    zoom: 7.5,
    x: -1150,
    y: -300,
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

