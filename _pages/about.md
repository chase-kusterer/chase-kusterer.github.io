---
permalink: /about/
title: "About"
layout: single
classes: wide
sidebar: null
author_profile: True
---
<h2 class="h2" style="margin:.25rem 0 .35rem;">My Career Journey</h2>

<style>
  :root{
    /* Map */
    --map-h: 60vh;
    --overlay-frac: .42;
    --oval-rx: 50%;
    --oval-ry: 42%;
    --oval-cx: 50%;
    --oval-cy: 50%;

    /* Timeline */
    --tl-line: #0f172a33;
    --tl-dot:  #0f172a;
    --tl-muted:#6b7280;
    --tl-gap:  12px;        /* baseline ↔ card gap (before the 50% reduction) */

    /* Spacing + geometry (tune these 3 first) */
    --tl-track: 200px;      /* fixed step between dots (try 180–240px) */
    --tl-height: 280px;     /* total vertical working height of each column */
    --tl-gap-factor: .5;    /* 0.5 = cards 50% closer to baseline */

    /* Card & tick */
    --tl-card-offset: 12px; /* space from tick to card’s left edge */
    --tl-dot-size: 12px;    /* dot size (keep in sync with .tick) */
  }

  /* ===== Map (unchanged) ===== */
  .map-shell { position: relative; width: 100%; margin: 0; }
  .map-viewport{
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

  .map-legend{
    align-self:center; display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;
    text-align:center; font-size:.90em; margin:.15rem 0 0;
  }
  .map-legend .dot{
    width:10px; height:10px; border-radius:50%; display:inline-block;
    box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;
  }

  /* ===== Timeline (clean, single set of rules) ===== */
  .timeline{
    position: relative;
    margin: 1.5rem 0 2rem;
    padding: 3.2rem 0 2.5rem; /* ~one extra line on top for “up” cards */
    background: transparent;
    isolation: isolate;
  }

  /* baseline drawn as background so it can’t cover ticks; starts under first dot */
  .tl-list{
    list-style:none; margin:0; padding:0;
    display:grid;
    grid-auto-flow: column;
    grid-auto-columns: var(--tl-track);     /* FIXED column width = equal spacing */
    gap: .75rem;                            /* inter-dot gap; halve/raise as needed */
    overflow-x:auto; overflow-y:visible;
    overscroll-behavior-x:contain; scroll-snap-type:x proximity;
    min-height: var(--tl-height);

    /* Baseline that starts at the first dot’s center and runs to the right edge */
    background: linear-gradient(to right, var(--tl-line), var(--tl-line)) no-repeat;
    background-position: calc(var(--tl-track)/2) 50%;
    background-size: calc(100% - (var(--tl-track)/2)) 2px;
  }

  .tl-item{
    position: relative;
    height: var(--tl-height);
    overflow: visible;
    scroll-snap-align: center;
  }

  /* Dot sits centered on the baseline; add thin ring for crispness */
  .tl-item .tick{
    position:absolute; left:50%; top:50%;
    width: var(--tl-dot-size); height: var(--tl-dot-size); border-radius:50%;
    background: var(--tl-dot);
    transform: translate(-50%, -50%);
    z-index: 2;
    box-shadow: 0 0 0 2px #fff; /* change #fff if page bg isn’t white */
  }

  /* Stems are 50% of original; under dot, over baseline */
  .tl-item .stem{ position:absolute; left:50%; width:2px; background:var(--tl-line);
                  transform: translateX(-50%); z-index:1; }
  .tl-item.up   .stem{ height: calc(var(--stem, 110px) * .5);
                       top: calc(50% - (var(--stem,110px) * .5)); }
  .tl-item.down .stem{ height: calc(var(--stem, 110px) * .5);
                       top: 50%; }

  /* Cards: start at tick line, 50% closer to baseline */
  .tl-item.up   .card{ position:absolute; left:50%;
                       bottom: calc(50% + (var(--tl-gap) * var(--tl-gap-factor)));
                       margin-left: var(--tl-card-offset); text-align:left; }
  .tl-item.down .card{ position:absolute; left:50%;
                       top:    calc(50% + (var(--tl-gap) * var(--tl-gap-factor)));
                       margin-left: var(--tl-card-offset); text-align:left; }

  /* Optional: sensible width for cards (responsive but bounded) */
  .tl-item .card{ width: clamp(260px, 26vw, 400px); max-width: 48ch; }

  /* Text styles */
  .tl-eyebrow{ font-size:.70rem; letter-spacing:.03em; text-transform:uppercase; color:var(--tl-muted); }
  .tl-range{   font-size:.80rem; color:var(--tl-muted); margin:.15rem 0 .35rem; }
  .tl-title{   margin:0; font-size:1.10rem; line-height:1.25; font-weight:700; }
  .tl-sub{     margin:.15rem 0 0; color:var(--tl-muted); }
  .tl-pill{    display:inline-block; padding:.2rem .5rem; border-radius:999px;
               background:#caff00; color:#0f172a; font-weight:600; font-size:.75rem; }

  @media (max-width: 640px){
    :root{ --overlay-frac:.40; --map-h:50vh; }
  }
  @media (max-width: 800px){
    .tl-item .stem{ height: calc(var(--stem,110px) * .75); top:auto; } /* slightly longer stems on small screens */
  }

  /* NEW */
  .layout--single .page__inner-wrap{
    max-width: min(95vw, 1400px);
  }

/* longer timeline */
/* Stack the author profile ABOVE the content (so no left column steals width) */
.layout--single .page__sidebar{ float:none; width:auto; max-width:100%; margin:0 0 1rem 0; position:static; }
.layout--single .sidebar{ position:static; }  /* disable sticky/float */

/* Full-bleed wrapper that spans the entire viewport width */
.fullbleed{
  width:100vw; max-width:100vw;
  margin-left:50%; transform:translateX(-50%);
  padding-inline: clamp(8px, 2.5vw, 24px);
}

/* (Optional) ensure nothing clips the full-bleed 
.layout--single .page__inner-wrap{ overflow: visible; } */

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
        <h4 class="tl-title">Assistant of Student Affairs</h4>
        <div class="tl-sub">Shantou University Business School</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 120px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2009–2018 · 9 years</div>
        <h4 class="tl-title">Director / Adjunct Professor</h4>
        <div class="tl-sub">EF Education First · Hult International Business School</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 110px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2016</div>
        <h4 class="tl-title">Chair &amp; Keynote Speaker</h4>
        <div class="tl-sub">DataX · Shenzhen &amp; Seoul</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 130px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2018–2025 · 7 years</div>
        <h4 class="tl-title">Faculty of Analytics</h4>
        <div class="tl-sub">Hult International Business School · San Francisco</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 115px;">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <div class="tl-range">2022, 2025</div>
        <h4 class="tl-title">Faculty (Visiting)</h4>
        <div class="tl-su
