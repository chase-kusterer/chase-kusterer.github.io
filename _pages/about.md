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
    width:1
