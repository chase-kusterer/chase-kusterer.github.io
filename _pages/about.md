---
permalink: /about/
title: "About"
layout: single
classes: wide
---
<h2 class="h2" style="margin:.25rem 0 .35rem;">My Career Journey</h2>
<style>
  :root{
    --map-h: 60vh;      /* full iframe height */
    --overlay-frac: .35;/* portion reserved for overlay (0.50 = bottom 50%) */

    /* optional: keep the oval mask on the visible part */
    --oval-rx: 50%;
    --oval-ry: 42%;
    --oval-cx: 50%;
    --oval-cy: 50%;
  }

  .map-shell { position: relative; width: 100%; margin: 0; }

  /* Only shows the TOP (1 - overlay) of the iframe */
  .map-viewport {
    position: relative;
    height: calc(var(--map-h) * (1 - var(--overlay-frac)));
    overflow: hidden;           /* hides the bottom part of the iframe */
    /* optional: oval mask on the visible part */
    -webkit-mask-image: radial-gradient(ellipse var(--oval-rx) var(--oval-ry)
      at var(--oval-cx) var(--oval-cy), #000 98%, transparent 100%);
    mask-image: radial-gradient(ellipse var(--oval-rx) var(--oval-ry)
      at var(--oval-cx) var(--oval-cy), #000 98%, transparent 100%);
  }

  .map-viewport iframe{
    display:block; width:100%; height: var(--map-h); border:0;
  }

  /* Transparent overlay area: feels like normal page content */
  .map-overlay{
    position: relative;  /* sits right below the cropped map */
    margin: .25rem 0 0;  /* tiny gap; set to 0 if you want it touching */
    background: transparent;   /* no color */
    color: inherit;            /* use your site’s text color */
    padding: 0;                /* no box feel */
  }

  .map-legend{ font-size:.75em; display:flex; gap:1rem; flex-wrap:wrap; }
  .map-legend .dot{
    width:10px; height:10px; border-radius:50%; display:inline-block;
    box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;
  }

  /* Mobile: reveal more of the map if you like */
  @media (max-width: 640px){
    :root{ --overlay-frac: .40; --map-h: 50vh; }
  }
</style>

<figure style="margin:0;">
  <div class="map-shell">
    <div class="map-viewport">
      <iframe
        src="{{ '/assets/maps/career_map2.html' | relative_url }}"
        title="Career Map" loading="lazy"></iframe>
    </div>

    <!-- Transparent overlay area = normal page content -->
    <div class="map-overlay">
      <div class="map-legend" role="group" aria-label="Map legend">
        <span><span class="dot" style="background:#e11d48;"></span> Places I’ve Worked (red)</span>
        <span><span class="dot" style="background:#2563eb;"></span> Presentations &amp; Workshops (blue)</span>
      <h2 class="h2" style="margin:.25rem 0 .35rem;">Career Timeline</h2>
      </div>
    </div>
  </div>
</figure>

## Professional Highlights
  * 10-time Faculty of the Year
  * Author of From Print to Prediction: A Beginner's Guide to Data Analysis in Python
  * Quoted in New York Times newspaper
