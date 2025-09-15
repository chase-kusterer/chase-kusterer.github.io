---
permalink: /about/
title: "About"
layout: single
classes: wide
---
<!-- yet ANOTHER career map -->
<style>
  /* Tweak these to taste */
  :root{
    --map-aspect: 3 / 1;     /* wide + short; try 16 / 9 or 2.5 / 1 */
    --oval-rx: 50%;          /* horizontal radius of the oval */
    --oval-ry: 42%;          /* vertical radius of the oval (lower = tighter crop) */
    --oval-cx: 50%;          /* oval center X (shift left/right: 48%, 52%, …) */
    --oval-cy: 50%;          /* oval center Y (shift up/down) */
  }

  .map-oval-wrap{
    position: relative;
    width: 100%;
    aspect-ratio: var(--map-aspect);  /* gives the container a real height */
    margin: 0;                        /* kill extra spacing */
    overflow: hidden;                 /* trim anything outside the mask/clip */
    /* Primary: CSS mask (clips children but keeps events) */
    -webkit-mask-image: radial-gradient(
      ellipse var(--oval-rx) var(--oval-ry) at var(--oval-cx) var(--oval-cy),
      #000 98%, transparent 100%);
    mask-image: radial-gradient(
      ellipse var(--oval-rx) var(--oval-ry) at var(--oval-cx) var(--oval-cy),
      #000 98%, transparent 100%);
    /* Fallback: clip-path if mask isn’t supported */
    clip-path: ellipse(var(--oval-rx) var(--oval-ry) at var(--oval-cx) var(--oval-cy));
  }

  .map-oval-wrap > iframe{
    display: block;
    width: 100%;
    height: 100%;
    border: 0;
  }
</style>

<figure style="margin:0;">
  <div class="map-oval-wrap">
    <iframe
      src="{{ '/assets/maps/career_map2.html' | relative_url }}"
      title="Career Map">
    </iframe>
  </div>

  <figcaption style="font-size:.5em; text-align:center; margin:.15rem 0 0;">
    <span style="--dot:10px; display:inline-flex; align-items:center; gap:.4rem;">
      <span aria-hidden="true" style="width:var(--dot); height:var(--dot); border-radius:50%;
        background:#e11d48; box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;"></span>
      Places I’ve Worked (red)
    </span>
    <span style="margin-left:1rem; --dot:10px; display:inline-flex; align-items:center; gap:.4rem;">
      <span aria-hidden="true" style="width:var(--dot); height:var(--dot); border-radius:50%;
        background:#2563eb; box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;"></span>
      Presentations &amp; Workshops (blue)
    </span>
  </figcaption>
</figure>


<!-- ANOTHER career map -->
<!-- Put this <style> somewhere on the page (top or just above the figure) -->
<style>
  /* Kill theme margins around this specific iframe */
  .page__content iframe[title="Career Map"] { margin-bottom: 0 !important; display:block; }

  /* Optional: also remove any bottom margin MM adds to the wrapper figure */
  .page__content figure.map-figure { margin: 0 !important; }
</style>

<figure class="map-figure" style="margin:0;">
  <iframe
    src="{{ '/assets/maps/career_map2.html' | relative_url }}"
    title="Career Map"
    style="display:block; width:100%; height:60vh; max-height:800px; border:0; margin:0;"
    loading="lazy">
  </iframe>

  <figcaption style="font-size:.5em; text-align:center; margin:.15rem 0 0;">
    <span style="--dot:10px; display:inline-flex; align-items:center; gap:.4rem;">
      <span aria-hidden="true" style="width:var(--dot); height:var(--dot); border-radius:50%;
        background:#e11d48; box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;"></span>
      Places I've Worked (red)
    </span>
    <span style="margin-left:1rem; --dot:10px; display:inline-flex; align-items:center; gap:.4rem;">
      <span aria-hidden="true" style="width:var(--dot); height:var(--dot); border-radius:50%;
        background:#2563eb; box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;"></span>
      Presentations &amp; Workshops (blue)
    </span>
  </figcaption>
</figure>


<!-- career map -->
## My Career Journey
<figure style="margin:0;">
  <figcaption style="font-size:.75em; text-align:center; margin:.15rem 0 0;">
    <span style="--dot:10px; display:inline-flex; align-items:center; gap:.4rem;">
      <span aria-hidden="true" style="width:var(--dot); height:var(--dot); border-radius:50%;
        background:#e11d48; box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;"></span>
      Work
    </span>
    <span style="margin-left:1rem; --dot:10px; display:inline-flex; align-items:center; gap:.4rem;">
      <span aria-hidden="true" style="width:var(--dot); height:var(--dot); border-radius:50%;
        background:#2563eb; box-shadow:0 0 0 2px #fff, 0 0 0 3px #e5e7eb;"></span>
      Presentations and Workshops
    </span>
  </figcaption>
  <iframe
    src="{{ '/assets/maps/career_map2.html' | relative_url }}"
    title="Career Map"
    style="display:block; width:100%; aspect-ratio: 16 / 9; border:0;"
  ></iframe>
  <iframe
    src="{{ '/assets/maps/career_map2.html' | relative_url }}"
    title="Career Map"
    style="display:block; width:100%; aspect-ratio: 16 / 9; border:0;"
  ></iframe>
</figure>

## Professional Highlights

  * 10-time Faculty of the Year
  * Author of From Print to Prediction: A Beginner's Guide to Data Analysis in Python
  * Quoted in New York Times newspaper

## Personal Highlights

  * Bilingual (English and Mandarin Chinese)
