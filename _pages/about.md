---
permalink: /about/
title: "About"
layout: single
classes: wide
---
<!-- yet ANOTHER career map -->
<style>
  :root{
    --overlay-h: 75%;           /* how much of the iframe the overlay covers */
    --panel-bg: rgba(255,255,255,.94);  /* panel background (use a dark rgba for dark maps) */
  }

  .map-wrap{
    position: relative;
    width: 100%;
    height: 60vh;               /* give the iframe real height; tweak to taste */
    max-height: 800px;
    margin: 0;
  }
  .map-wrap > iframe{
    position:absolute; inset:0;
    width:100%; height:100%;
    border:0;
    display:block;
  }

/* bottom overlay that “crops” the map and holds text */
  .map-overlay{
    position:absolute; left:0; right:0; bottom:0;
    height: var(--overlay-h);
    display:flex; align-items:flex-end; justify-content:center;
    /* fade the map out toward the panel */
    background: linear-gradient(to top, var(--panel-bg) 35%, rgba(255,255,255,0) 100%);
    /* if you prefer a solid panel only, replace the line above with: background: var(--panel-bg); */
  }

  .map-overlay .content{
    /* text block centered on the panel */
    background: var(--panel-bg);
    padding: .75rem 1rem 1rem;
    text-align:center;
    border-radius: 10px;
    box-shadow: 0 6px 20px rgba(0,0,0,.12);
    max-width: 900px;
    margin: 0 1rem .5rem;
  }

  /* legend dots */
  .map-legend { font-size:.50em; display:flex; gap:1rem; justify-content:center; flex-wrap:wrap; margin-top:.25rem; }
  .map-legend .dot{ width:10px; height:10px; border-radius:50%; display:inline-block; box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb; }

  /* Mobile: make the overlay shallower so more map remains interactive */
  @media (max-width: 640px){
    :root{ --overlay-h: 40%; }
    .map-wrap{ height: 50vh; }
    .map-legend{ font-size:.7em; }
  }
</style>

<figure style="margin:0;">
  <div class="map-wrap">
    <iframe
      src="{{ '/assets/maps/career_map2.html' | relative_url }}"
      title="Career Map">
    </iframe>

    <!-- Bottom-half overlay with H2 + legend -->
    <div class="map-overlay">
      <div class="content">
        <div class="map-legend" role="group" aria-label="Map legend">
          <span><span class="dot" style="background:#e11d48;"></span> Places I’ve Worked</span>
          <span><span class="dot" style="background:#2563eb;"></span> Presentations &amp; Workshops</span>
          <br>
          <h2 class="h2" style="margin:.25rem 0 .35rem;">Random Task</h2>
        </div>
      </div>
    </div>
  </div>
</figure>
