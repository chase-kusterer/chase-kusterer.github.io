---
permalink: /about/
title: "About"
layout: single
classes: wide
---
<!-- yet ANOTHER career map -->
<style>
  :root{
    --overlay-h: 50%;                 /* how much of the iframe the overlay covers */
    --panel-bg: rgba(255,255,255,.92);/* use rgba(17,24,39,.90) for dark-theme pages */
    --gutter: 1rem;                   /* side padding so text isn’t flush to the edge */
  }

  .map-wrap{
    position: relative;
    width: 100%;
    height: 60vh; max-height: 800px;
    margin: 0;
  }
  .map-wrap > iframe{
    position:absolute; inset:0; width:100%; height:100%; border:0; display:block;
  }

  /* Bottom overlay: left-aligned, no box */
  .map-overlay{
    position:absolute; left:0; right:0; bottom:0;
    height: var(--overlay-h);
    display:flex; align-items:flex-end; justify-content:flex-start;
    /* soft fade so the map merges into the page; reduce 35%→20% for subtler fade */
    background: linear-gradient(to top, var(--panel-bg) 35%, rgba(255,255,255,0) 100%);
    padding: 0 var(--gutter) .6rem var(--gutter);   /* simple page-like gutters */
  }

  .map-overlay .content{
    /* make it feel like normal flow — no background, no border, no shadow */
    background: none; box-shadow:none; border-radius:0; padding:0;
    text-align:left;
    color: inherit;      /* use site’s default text color */
    pointer-events:auto; /* links are clickable (overlay itself remains interactive) */
  }

  .map-overlay h2{
    margin:.25rem 0 .35rem;           /* tight spacing */
  }

  /* Legend inline, left-aligned */
  .map-legend{ font-size:.75em; display:flex; gap:1rem; flex-wrap:wrap; margin-top:.15rem; }
  .map-legend .dot{ width:10px; height:10px; border-radius:50%; display:inline-block;
                    box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb; }

  /* Mobile: show a bit more map and keep text readable */
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

    <!-- bottom-left caption area that reads like page content -->
    <div class="map-overlay">
      <div class="content">
        <h2 class="h2">My Career Journey</h2>
        <div class="map-legend" role="group" aria-label="Map legend">
          <span><span class="dot" style="background:#e11d48;"></span> Places I’ve Worked (red)</span>
          <span><span class="dot" style="background:#2563eb;"></span> Presentations &amp; Workshops (blue)</span>
        </div>
      </div>
    </div>
  </div>
</figure>
  </div>
</figure>
