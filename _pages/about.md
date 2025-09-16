---
permalink: /about/
title: "About"
layout: single
classes: wide
---
<h2 class="h2" style="margin:.25rem 0 .35rem;">My Career Journey</h2>

<style>
  :root{
    --map-h: 60vh;
    --overlay-frac: .42;
    --oval-rx: 50%;
    --oval-ry: 42%;
    --oval-cx: 50%;
    --oval-cy: 50%;

    /* Timeline vars */
    --tl-line: #0f172a33;
    --tl-dot:  #0f172a;
    --tl-muted:#6b7280;
    --tl-gap:  12px;
  }

  .map-shell { position: relative; width: 100%; margin: 0; }

  /* Show only the TOP (1 - overlay) of the iframe */
  .map-viewport {
    position: relative;
    height: calc(var(--map-h) * (1 - var(--overlay-frac)));
    overflow: hidden;
    -webkit-mask-image: radial-gradient(ellipse var(--oval-rx) var(--oval-ry)
      at var(--oval-cx) var(--oval-cy), #000 98%, transparent 100%);
    mask-image: radial-gradient(ellipse var(--oval-rx) var(--oval-ry)
      at var(--oval-cx) var(--oval-cy), #000 98%, transparent 100%);
  }
  .map-viewport iframe{
    display:block; width:100%; height: var(--map-h); border:0;
  }

  /* Transparent overlay area */
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

  /* Center ONLY the legend */
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

  /* ===== Timeline layout ===== */
  .timeline{
    position: relative;
    margin: 1.5rem 0 2rem;
    padding: 2.5rem 0;
    background: transparent;
    isolation: isolate; /* ensures clean stacking context */
  }

  /* Hide pseudo-element baseline (we'll draw it on .tl-list) */
  .timeline::before{ display:none; }

  .tl-list{
    list-style:none; margin:0; padding:0;
    display:grid;
    grid-auto-flow: column;
    grid-auto-columns: minmax(220px, 1fr);
    gap: 3rem;
    overflow-x: auto;
    overscroll-behavior-x: contain;
    scroll-snap-type: x proximity;

    /* Baseline as background so it can’t cover ticks */
    background: linear-gradient(to right, var(--tl-line), var(--tl-line)) center/100% 2px no-repeat;
    overflow-y: visible; /* let ticks cross the line */
  }

  .tl-item{
    position: relative;
    scroll-snap-align: center;
  }

  /* Ticks + stems + cards */
  .tl-item .tick{
    position:absolute; left:50%; top:50%;
    width:12px; height:12px; border-radius:50%;
    background: var(--tl-dot);
    transform: translate(-50%, -50%);
    z-index: 2;
    box-shadow: 0 0 0 2px #fff; /* change if page bg isn’t white */
  }
  .tl-item .stem{ z-index: 1; }

  .tl-item.up   .stem{ position:absolute; left:50%; width:2px; background:var(--tl-line);
                       height: var(--stem, 110px);
                       top: calc(50% - var(--stem, 110px)); transform: translateX(-50%); }
  .tl-item.down .stem{ position:absolute; left:50%; width:2px; background:var(--tl-line);
                       height: var(--stem, 110px);
                       top: 50%; transform: translateX(-50%); }

  .tl-item.up   .card{ position:absolute; left:50%; bottom: calc(50% + var(--tl-gap));
                       transform: translateX(-50%); text-align:left; }
  .tl-item.down .card{ position:absolute; left:50%; top:    calc(50% + var(--tl-gap));
                       transform: translateX(-50%); text-align:left; }

  /* Text styles */
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
  .tl-pill{
    display:inline-block; padding:.2rem .5rem; border-radius:999px;
    background:#caff00; color:#0f172a; font-weight:600; font-size:.75rem;
  }

  @media (max-width: 640px){
    :root{ --overlay-frac: .40; --map-h: 50vh; }
  }
  @media (max-width: 800px){
    .tl-item .stem{ height: calc(var(--stem,110px) * .75); top:auto; }
  }

  /* ---- Timeline geometry fix: make items tall and keep baseline behind ---- */

  /* 1) One height for the whole timeline row (tweak to taste) */
  :root { --tl-height: 260px; }  /* try 240–300px depending on your stem lengths */
  
  /* 2) Baseline handled by .tl-list background (not a pseudo-element) */
  .timeline::before { display: none; }
  
  /* 3) The list owns the baseline and the vertical space */
  .timeline .tl-list{
    position: relative;
    min-height: var(--tl-height);
    background: linear-gradient(to right, var(--tl-line), var(--tl-line)) center/100% 2px no-repeat;
    overflow-y: visible;         /* dots/stems won’t be clipped crossing the line */
  }
  
  /* 4) Each item has the same height as the list; allow overflow just in case */
  .timeline .tl-item{
    position: relative;
    height: var(--tl-height);
    overflow: visible;
  }
  
  /* 5) Stacking order: line (background) < stem < tick */
  .timeline .tl-item .stem { z-index: 1; }
  .timeline .tl-item .tick{
    z-index: 2;
    /* Optional thin ring so the dot sits crisply over the line.
       Change #fff to your page background if not white. */
    box-shadow: 0 0 0 2px #fff;
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
        <span><span class="dot" style="background:#e11d48;"></span> Places I’ve Worked</span>
        <span><span class="dot" style="background:#2563eb;"></span> Presentations &amp; Workshops</span>
      </div>

      <h2 class="h2" style="margin:.25rem 0 .35rem;">Career Timeline</h2>
    </div>
  </div> <!-- /map-shell -->
</figure> <!-- /figure -->

<h3>Professional Highlights</h3>
<ul>
  <li>10-time Faculty of the Year</li>
  <li>Author of <em>From Print to Prediction: A Beginner’s Guide to Data Analysis in Python</em></li>
  <li>Quoted in <em>The New York Times</em></li>
</ul>

<!-- Timeline -->
<div class="timeline" aria-label="Career timeline">
  <ol class="tl-list">
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

    <li class="tl-item down" style="--stem: 120px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2009–2018 · 9 years</div>
        <h3 class="tl-title">Director / Adjunct Professor</h3>
        <div class="tl-sub">EF Education First · Hult International Business School</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 110px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2016</div>
        <h3 class="tl-title">Chair &amp; Keynote Speaker</h3>
        <div class="tl-sub">DataX · Shenzhen &amp; Seoul</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 130px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2018–2025 · 7 years</div>
        <h3 class="tl-title">Faculty of Analytics</h3>
        <div class="tl-sub">Hult International Business School · San Francisco</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 115px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2022, 2025</div>
        <h3 class="tl-title">Faculty (Visiting)</h3>
        <div class="tl-sub">Hult · New York City</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 120px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2024–Now</div>
        <h3 class="tl-title">Presenter &amp; Workshop Host</h3>
        <div class="tl-sub">Conferences across Asia &amp; U.S.</div>
      </div>
    </li>
  </ol>
</div>
