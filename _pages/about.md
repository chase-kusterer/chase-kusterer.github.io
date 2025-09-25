---
permalink: /about/
title: "My Career Journey"
layout: single
classes: wide
sidebar: null
author_profile: True
---

<style>
  /* ===========================
     Global variables
     =========================== */
  :root{
    /* Map geometry */
    --map-h: 60vh;
    --overlay-frac: .42;   /* how much “white band” shows under the oval */
    --oval-rx: 50%;
    --oval-ry: 42%;
    --oval-cx: 50%;
    --oval-cy: 50%;
    /* Legend overlap that adapts to map size (closer to map edge) */
    --legend-overlap: clamp(4px, calc(var(--map-h) * 0.02), 14px);

    /* Timeline base (we'll scale these below with --tl-scale) */
    --tl-line: #0f172a33;
    --tl-dot:  #0f172a;
    --tl-muted:#6b7280;
    --tl-gap-factor: 1.00;  /* closer to 1 = farther from the line */

    /* Base sizes (do not edit; change --tl-scale instead) */
    --tl-track-base:        200px;  /* spacing between dots */
    --tl-height-base:       360px;  /* total vertical working height */
    --tl-gap-base:          2rem;   /* dot ↔ card distance */
    --tl-dot-size-base:     12px;   /* dot */
    --tl-card-offset-base:  12px;   /* card x-offset */
    --tl-title-size-base:   1.10rem;

    /* One knob to resize the entire timeline */
    --tl-scale: 0.85; /* 1.00 = original size, <1 smaller, >1 larger */

    /* Zoom-stable full-bleed width + bias
       0   = flush left, 0.5 = centered, 1 = flush right */
    --bleed-w: min(80vw, 1400px);
    --bleed-bias: -1.25;  /* move left (<0.5), center (=0.5), right (>0.5) */
  }

  /* Derived timeline sizes (auto) */
  :root{
    --tl-track:        calc(var(--tl-track-base)       * var(--tl-scale));
    --tl-height:       calc(var(--tl-height-base)      * var(--tl-scale));
    --tl-gap:          calc(var(--tl-gap-base)         * var(--tl-scale));
    --tl-dot-size:     calc(var(--tl-dot-size-base)    * var(--tl-scale));
    --tl-card-offset:  calc(var(--tl-card-offset-base) * var(--tl-scale));
    --tl-title-size:   calc(var(--tl-title-size-base)  * var(--tl-scale));
    --tl-stem-scale:   var(--tl-scale); /* stems follow the same scale */
  }

  /* ===========================
     Map (legend mirrors from iframe)
     =========================== */
  .map-shell{ position: relative; width: 100%; margin: 0; }

  .map-viewport{
    position: relative;
    height: calc(var(--map-h) * (1 - var(--overlay-frac)));
    overflow: hidden;
    -webkit-mask-image: radial-gradient(
      ellipse var(--oval-rx) var(--oval-ry) at var(--oval-cx) var(--oval-cy),
      #000 98%, transparent 100%);
            mask-image: radial-gradient(
      ellipse var(--oval-rx) var(--oval-ry) at var(--oval-cx) var(--oval-cy),
      #000 98%, transparent 100%);
    z-index: 1; /* legend sits above this */
  }
  .map-viewport iframe{
    display:block; width:100%; height: var(--map-h); border:0;
  }

  /* Legend proxy (cloned from inside career_map2.html) */
  .legend-proxy{
    position: absolute;      /* anchored to .map-shell (the map) */
    left: 46%;
    bottom: calc(var(--legend-overlap) * -1); /* tuck onto the white band */
    transform: translateX(-50%);
    z-index: 10;

    /* visual: no border/shadow per your request */
    background: transparent;
    border: 0;
    box-shadow: none;

    display: grid;
    grid-auto-flow: column;  /* keep items horizontal */
    gap: 14px;
    align-items: center;
    font: 500 14px/1.3 system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
  }
  .legend-proxy > span{
    display:inline-flex; align-items:center; gap:8px; white-space:nowrap;
  }
  .legend-proxy .dot{
    width: 12px; height: 12px; border-radius: 9999px;
    border: 1px solid rgba(0,0,0,.25);
    display: inline-block; flex: 0 0 auto;
  }
  @media (max-width: 640px){
    .legend-proxy{ gap: 10px; }
  }

  /* ===========================
     Timeline (driven by variables above)
     =========================== */
  .timeline{
    position: relative;
    margin: 1.0rem 0 1.0rem; /* distance between map and timeline */
    padding: 1.5rem 0 1.5rem;  /* ~one extra line on top for “up” cards */
    background: transparent;
    isolation: isolate;
  }

  .tl-list{
    list-style:none; margin:0; padding:0;
    display:grid;
    grid-auto-flow: column;
    grid-auto-columns: var(--tl-track);     /* column width = equal spacing */
    gap: calc(.75rem * var(--tl-scale));    /* inter-dot gap scales */
    overflow-x:auto; overflow-y:visible;
    overscroll-behavior-x:contain; scroll-snap-type:x proximity;
    min-height: var(--tl-height);
    /* Baseline under first dot */
    background: linear-gradient(to right, var(--tl-line), var(--tl-line)) no-repeat;
    background-position: calc(var(--tl-track)/2) 50%;
    background-size: calc(100% - (var(--tl-track)/2)) calc(2px * var(--tl-scale));
  }

  .tl-item{
    position: relative;
    height: var(--tl-height);
    overflow: visible;
    scroll-snap-align: center;
  }

  .tl-item .tick{
    position:absolute; left:50%; top:50%;
    width: var(--tl-dot-size); height: var(--tl-dot-size); border-radius:50%;
    background: var(--tl-dot);
    transform: translate(-50%, -50%);
    z-index: 2;
    box-shadow: 0 0 0 calc(2px * var(--tl-scale)) #fff; /* thin ring scales */
  }

  .tl-item .stem{
    position:absolute; left:50%;
    width: calc(2px * var(--tl-scale));
    background:var(--tl-line);
    transform: translateX(-50%);
    z-index:1;
  }
  .tl-item.up   .stem{
    height: calc((var(--stem, 110px) * .5 * var(--tl-stem-scale)) + (var(--tl-gap) * var(--tl-gap-factor)));
    top:    calc(50% - ((var(--stem, 110px) * .5 * var(--tl-stem-scale)) + (var(--tl-gap) * var(--tl-gap-factor))));
  }
  .tl-item.down .stem{
    height: calc((var(--stem, 110px) * .5 * var(--tl-stem-scale)) + (var(--tl-gap) * var(--tl-gap-factor)));
    top: 50%;
  }

  .tl-item.up   .card{ position:absolute; left:50%;
                       bottom: calc(50% + (var(--tl-gap) * var(--tl-gap-factor)));
                       margin-left: var(--tl-card-offset); text-align:left; }
  .tl-item.down .card{ position:absolute; left:50%;
                       top:    calc(50% + (var(--tl-gap) * var(--tl-gap-factor)));
                       margin-left: var(--tl-card-offset); text-align:left; }

  .tl-item .card{
    width: clamp(calc(220px * var(--tl-scale)), calc(26vw * var(--tl-scale)), calc(400px * var(--tl-scale)));
    max-width: 48ch;
  }

  .tl-nudge{
    position:absolute; top:50%;
    transform:translateY(-50%);
    width: calc(38px * var(--tl-scale));
    height: calc(38px * var(--tl-scale));
    border-radius:9999px;
    border:1px solid #e5e7eb;
    background: rgba(255,255,255,.9);
    box-shadow:0 2px 8px rgba(0,0,0,.08);
    display:grid; place-items:center;
    cursor:pointer; z-index:5;
  }
  .tl-nudge--left  { left:.5rem; }
  .tl-nudge--right { right:.5rem; }
  .tl-nudge:hover  { background:#fff; }
  .tl-nudge svg    { display:block; width: calc(18px * var(--tl-scale)); height: calc(18px * var(--tl-scale)); }
  @media (max-width: 480px){ .tl-nudge{ display:none; } }

  .tl-eyebrow{ font-size:.70rem; letter-spacing:.03em; text-transform:uppercase; color:var(--tl-muted); }
  .tl-range{   font-size:.80rem; color:var(--tl-muted); margin:.15rem 0 .35rem; }
  .tl-title{   margin:0; font-size:var(--tl-title-size
