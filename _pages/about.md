---
permalink: /about/
title: "About"
layout: single
classes: wide
---
<h2 class="h2" style="margin:.25rem 0 .35rem;">My Career Journey</h2>
<style>
  :root{
    --map-h: 60vh;       /* full iframe height */
    --overlay-frac: .42; /* portion reserved for overlay (0.50 = bottom 50%) */

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
  
  /* -------------------------------------------------------- */
  /* transparent overlay area: feels like normal page content */
  /* -------------------------------------------------------- */

  /* transparent overlay area */
  .map-overlay{
    position: relative;
    margin: .25rem 0 0;
    background: transparent;
    color: inherit;
    padding: 0;

    /* stack children: legend then h2 */
    display: flex;
    flex-direction: column;
    align-items: flex-start;   /* keep H2 left-aligned */
  }

  /* center ONLY the legend */
  .map-legend{
    align-self: center;        /* centers the legend block */
    display: flex;
    justify-content: center;   /* centers the items inside */
    gap: 1rem;
    flex-wrap: wrap;
    text-align: center;
    font-size: .90em;
    margin: .15rem 0 0;
  }
  .map-legend .dot{
    width:10px; height:10px; border-radius:50%; display:inline-block;
    box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;
  }

  /* Mobile: reveal more of the map if you like */
  @media (max-width: 640px){
    :root{ --overlay-frac: .40; --map-h: 50vh; }
  }

/* ===== Timeline vars (tweak colors and sizes) ===== */
:root{
  --tl-line: #0f172a33;        /* timeline line + stems */
  --tl-dot:  #0f172a;          /* node dot color */
  --tl-muted:#6b7280;          /* secondary text */
  --tl-gap:  12px;             /* gap between baseline and text */
}

/* ===== Layout ===== */
.timeline{
  position: relative;
  margin: 1.5rem 0 2rem;
  padding: 2.5rem 0;           /* space for above/below labels */
  background: transparent;     /* keep page background visible */
}

.timeline::before{
  /* baseline */
  content:"";
  position:absolute; left:0; right:0; top:50%;
  border-top: 2px solid var(--tl-line);
}

/* scrollable horizontal flow on small screens */
.tl-list{
  list-style:none; margin:0; padding:0;
  display:grid;
  grid-auto-flow: column;
  grid-auto-columns: minmax(220px, 1fr);
  gap: 3rem;
  overflow-x: auto;
  overscroll-behavior-x: contain;
  scroll-snap-type: x proximity;
}

/* each event */
.tl-item{
  position: relative;
  scroll-snap-align: center;
}

/* node on the baseline */
.tl-item .tick{
  position:absolute; left:50%; top:50%;
  width:12px; height:12px; border-radius:50%;
  background: var(--tl-dot);
  transform: translate(-50%, -50%);
}

/* vertical stems */
.tl-item.up   .stem{ position:absolute; left:50%; width:2px; background:var(--tl-line);
                     height: var(--stem, 110px);
                     top: calc(50% - var(--stem, 110px)); transform: translateX(-50%); }
.tl-item.down .stem{ position:absolute; left:50%; width:2px; background:var(--tl-line);
                     height: var(--stem, 110px);
                     top: 50%; transform: translateX(-50%); }

/* content blocks (no boxes; text only) */
.tl-item.up   .card{ position:absolute; left:50%; bottom: calc(50% + var(--tl-gap));
                     transform: translateX(-50%); text-align:left; }
.tl-item.down .card{ position:absolute; left:50%; top:    calc(50% + var(--tl-gap));
                     transform: translateX(-50%); text-align:left; }

/* text styles */
.tl-eyebrow{
  font-size: .70rem; letter-spacing:.03em; text-transform:uppercase;
  color: var(--tl-muted);
}
.tl-range{
  font-size: .80rem; color: var(--tl-muted); margin:.15rem 0 .35rem;
}
.tl-title{
  margin: 0; font-size: 1.10rem; line-height: 1.25; font-weight: 700;
}
.tl-sub{
  margin: .15rem 0 0; color: var(--tl-muted);
}

/* optional neon "Education" pill like your sample */
.tl-pill{
  display:inline-block; padding:.2rem .5rem; border-radius:999px;
  background:#caff00; color:#0f172a; font-weight:600; font-size:.75rem;
}

/* responsive: shorten stems on narrow screens */
@media (max-width: 800px){
  .tl-item .stem{ height: calc(var(--stem,110px) * .75); top:auto; }
}

/* === Timeline tick rendering fix (full circles) === */
/* Keep the baseline behind everything */
.timeline::before { z-index: 0; }

/* Stems sit above the line, below the dots */
.tl-item .stem { z-index: 1; }

/* Dots sit on top; an optional small ring keeps them crisp on the line */
.tl-item .tick {
  z-index: 2;
  box-shadow: 0 0 0 2px #fff; /* change #fff to your page background color if not white */
}

/* Make sure nothing clips the dots vertically */
.tl-list { overflow-y: visible; }
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
    <span><span class="dot" style="background:#e11d48;"></span> Places I’ve Worked</span>
    <span><span class="dot" style="background:#2563eb;"></span> Presentations &amp; Workshops</span>
  </div>

  <br>
  <h2 class="h2" style="margin:.25rem 0 .35rem;">Career Timeline</h2>
</div>



<h3>Professional Highlights</h3>
<ul>
  <li>10-time Faculty of the Year</li>
  <li>Author of <em>From Print to Prediction: A Beginner’s Guide to Data Analysis in Python</em></li>
  <li>Quoted in <em>The New York Times</em></li>
</ul>


<!-- Role (below the line) -->
<div class="timeline" aria-label="Career timeline">
  <ol class="tl-list">

    <!-- Education (above the line) -->
    <li class="tl-item up" style="--stem: 140px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill">Education</span>
        <div class="tl-range">2008–2009 · 1 year</div>
        <h3 class="tl-title">Assistant of Student Affairs</h3>
        <div class="tl-sub">Shantou University Business School</div>
      </div>
    </li>

    <!-- Role (below the line) -->
    <li class="tl-item down" style="--stem: 120px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2009–2018 · 9 years</div>
        <h3 class="tl-title">Director / Adjunct Professor</h3>
        <div class="tl-sub">EF Education First · Hult International Business School</div>
      </div>
    </li>

    <!-- Speaker (above) -->
    <li class="tl-item up" style="--stem: 110px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2016</div>
        <h3 class="tl-title">Chair & Keynote Speaker</h3>
        <div class="tl-sub">DataX · Shenzhen & Seoul</div>
      </div>
    </li>

    <!-- Faculty (below) -->
    <li class="tl-item down" style="--stem: 130px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2018–2025 · 7 years</div>
        <h3 class="tl-title">Faculty of Analytics</h3>
        <div class="tl-sub">Hult International Business School · San Francisco</div>
      </div>
    </li>

    <!-- NYC (above) -->
    <li class="tl-item up" style="--stem: 115px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2022, 2025</div>
        <h3 class="tl-title">Faculty (Visiting)</h3>
        <div class="tl-sub">Hult · New York City</div>
      </div>
    </li>

    <!-- Recent (below) -->
    <li class="tl-item down" style="--stem: 120px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2024–Now</div>
        <h3 class="tl-title">Presenter & Workshop Host</h3>
        <div class="tl-sub">Conferences across Asia & U.S.</div>
      </div>
    </li>

  </ol>
</div>
