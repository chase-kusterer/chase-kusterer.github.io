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
    --bleed-bias: 0.35;  /* move left (<0.5), center (=0.5), right (>0.5) */
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
    left: 50%;
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
  .tl-title{   margin:0; font-size:var(--tl-title-size); line-height:1.25; font-weight:700; hyphens: auto; overflow-wrap: anywhere;}
  .tl-sub{     margin:.15rem 0 0; color:var(--tl-muted); }
  .tl-pill{
    --pill-bg:#caff00;   /* default bg */
    --pill-fg:#0f172a;   /* default fg */
    display:inline-block;
    padding:.2rem .5rem;
    border-radius:999px;
    font-weight:600;
    font-size:.75rem;
    line-height:1.2;
    background:var(--pill-bg);
    color:var(--pill-fg);
  }
  .tl-pill--work{ --pill-bg:#f54927; --pill-fg:#ffffff; }
  .tl-pill--pres{ --pill-bg:#4734E0; --pill-fg:#ffffff; }

  @media (max-width: 640px){
    :root{ --overlay-frac:.40; --map-h:50vh; }
  }
  @media (max-width: 800px){
    .tl-item .stem{ height: calc(var(--stem,110px) * .75); top:auto; } /* slightly longer stems on small screens */
  }

  /* ===========================
     Layout wrappers
     =========================== */
  .layout--single .page__inner-wrap{ max-width: min(95vw, 1400px); overflow: visible; }
  .layout--single .page__sidebar{ float:none; width:auto; max-width:100%; margin:0 0 1rem 0; position:static; }
  .layout--single .sidebar{ position:static; }

  /* Zoom-stable full-bleed with left↔right bias */
  .fullbleed{
    width: var(--bleed-w);
    margin-left:  calc((100vw - var(--bleed-w)) * var(--bleed-bias));
    margin-right: calc((100vw - var(--bleed-w)) * (1 - var(--bleed-bias)));
    padding-inline: clamp(8px, 2.5vw, 24px);
    transform: none;
  }
  @media (max-width: 640px){
    .fullbleed{
      --bleed-w: 100vw;
      --bleed-bias: 0;   /* flush left on narrow screens */
      padding-inline: 8px;
    }
  }

  /* ===========================
     Chips (bottom of page)
     =========================== */
  .chips{
    display:flex; flex-wrap:wrap; justify-content:center;
    gap:.75rem; margin:.5rem 0 0;
  }
  .chip{
    display:inline-block; padding:.45rem 1rem; border-radius:9999px;
    background:#f3f4f6; border:1px solid #e5e7eb; box-shadow:0 1px 0 rgba(0,0,0,.02) inset;
    color:#111827; font-weight:700; line-height:1; white-space:nowrap;
    font-size:clamp(.85rem,.9vw,1rem);
  }
  .chip-marquee{
    --gap: .75rem; --speed: 35s; --gutter: calc(var(--tl-track)/2);
    --fadeL: 16px; --fadeR: 8%;
    position: relative; overflow: hidden; margin-top: .25rem;
    -webkit-mask-image: linear-gradient(
      to right,
      transparent 0,
      transparent calc(var(--gutter) - var(--fadeL)),
      #000        var(--gutter),
      #000        calc(100% - var(--fadeR)),
      transparent 100%
    );
            mask-image: linear-gradient(
      to right,
      transparent 0,
      transparent calc(var(--gutter) - var(--fadeL)),
      #000        var(--gutter),
      #000        calc(100% - var(--fadeR)),
      transparent 100%
    );
  }
  .chip-track{ display:inline-flex; gap:var(--gap); width:max-content; animation: chip-marquee var(--speed) linear infinite; }
  .chip-marquee:hover .chip-track{ animation-play-state: paused; }
  @media (prefers-reduced-motion: reduce){ .chip-track{ animation: none; } }
  @keyframes chip-marquee{ from{transform:translateX(0);} to{transform:translateX(-50%);} }
</style>

<!-- ===== Map Section ===== -->
<figure style="margin:0;">
  <div class="map-shell">
    <div class="map-viewport">
      <iframe
        src="{{ '/assets/maps/career_map2.html' | relative_url }}"
        title="Career Map"
        loading="lazy"
        id="career-map-iframe"></iframe>
    </div>

    <!-- Legend proxy (we fill this from INSIDE the iframe) -->
    <div class="legend-proxy" role="group" aria-label="Map legend"></div>
  </div>
</figure>

<!-------------->
<!-- Timeline -->
<!-------------->
<div class="fullbleed">
  <div class="timeline" aria-label="Career timeline">
  <ol class="tl-list">

<!--            -->
<!-- START 2008 -->
<!--            -->
    <li class="tl-item up" style="--stem: 140px;" data-key="fargo-usa">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill">Education</span>
        <div class="tl-range">2004–2008 · 4 years</div>
        <h4 class="tl-title">Bachelor's of Business Administration</h4>
        <div class="tl-sub">North Dakota State University</div>
        <div class="tl-sub">Fargo · USA</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 140px;" data-key="shantou-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2008–2009 · 1 year</div>
        <h4 class="tl-title">Assistant of Student Affairs</h4>
        <div class="tl-sub">Shantou University Business School</div>
        <div class="tl-sub">Shantou · China</div>
      </div>
    </li>

<!--            -->
<!-- START 2010 -->
<!--            -->
    <li class="tl-item up" style="--stem: 110px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill">Education</span>
        <div class="tl-range">2010 · 4 months</div>
        <h4 class="tl-title">Chinese Language Certificate</h4>
        <div class="tl-sub">Donghua University</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

<!--            -->
<!-- START 2011 -->
<!--            -->
    <li class="tl-item down" style="--stem: 120px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2011 · 6 months</div>
        <h4 class="tl-title">Special Assistant to the CFO</h4>
        <div class="tl-sub">China US Strategy Capital Group, Ltd.</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

<!--            -->
<!-- START 2013 -->
<!--            -->
    <li class="tl-item up" style="--stem: 110px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2011-2014 · 3+ years</div>
        <h4 class="tl-title">Media Intelligence Client Manager</h4>
        <div class="tl-sub">CTR Market Research</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Publication</span>
        <div class="tl-range">2013</div>
        <h4 class="tl-title">Consumers, Ecommerce, and Media in China</h4>
        <div class="tl-sub">China Business Handbook</div>
        <div class="tl-sub">US Commercial Service</div>
      </div>
    </li>  

    <li class="tl-item up" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2013-2017 · 5 years</div>
        <h4 class="tl-title">Adjunct Faculty</h4>
        <div class="tl-sub">Hult International Business School</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 130px;" data-key="beijing-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Speaker</span>
        <div class="tl-range">2014</div>
        <h4 class="tl-title">InfoSys OOH (in Mandarin)</h4>
        <div class="tl-sub">CTR Market Research</div>
        <div class="tl-sub">Beijing · China</div>
      </div>
    </li>
    
    <li class="tl-item up" style="--stem: 130px;" data-key="chicago-usa">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill">Education</span>
        <div class="tl-range">2014-2016 · 2 years</div>
        <h4 class="tl-title">Master's of Predictive Analytics</h4>
        <div class="tl-sub">Northwestern University</div>
        <div class="tl-sub">Chicago/Evanston · USA</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Speaker</span>
        <div class="tl-range">2015</div>
        <h4 class="tl-title">The Fridge has Facebook</h4>
        <div class="tl-sub">TedX</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="dubai-uae">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2015-2021 · 7 years</div>
        <h4 class="tl-title">Faculty (Visiting)</h4>
        <div class="tl-sub">Hult International Business School</div>
        <div class="tl-sub">Dubai · UAE</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2015-2017 · 2+ years</div>
        <h4 class="tl-title">Director of Marketing Analytics</h4>
        <div class="tl-sub">Education First - Kids &amp; Teens</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="shenzhen-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Keynote</span>
        <div class="tl-range">2016</div>
        <h4 class="tl-title">Big Data &amp; Analytics Innovation Summit</h4>
        <div class="tl-sub">Innovation Enterprise</div>
        <div class="tl-sub">Shenzhen · China</div>
      </div>
    </li>   

    <li class="tl-item down" style="--stem: 130px;" data-key="bangkok-thailand">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Workshop</span>
        <div class="tl-range">2016</div>
        <h4 class="tl-title">Regional Division Conference</h4>
        <div class="tl-sub">Education First - Kids &amp; Teens</div>
        <div class="tl-sub">Bangkok · Thailand</div>
      </div>
    </li>   

    <li class="tl-item up" style="--stem: 130px;" data-key="jakarta-indonesia">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Master Class</span>
        <div class="tl-range">2016</div>
        <h4 class="tl-title">International Recruitment Seminar</h4>
        <div class="tl-sub">Hult International Business School</div>
        <div class="tl-sub">Jakarta · Indonesia</div>
      </div>
    </li>    

    <li class="tl-item down" style="--stem: 130px;" data-key="manila-philippines">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Master Class</span>
        <div class="tl-range">2016</div>
        <h4 class="tl-title">International Recruitment Seminar</h4>
        <div class="tl-sub">Hult International Business School</div>
        <div class="tl-sub">Manila · Philippines</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="budapest-hungary">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Workshop</span>
        <div class="tl-range">2016</div>
        <h4 class="tl-title">Global Division Conference</h4>
        <div class="tl-sub">Education First - Kids &amp; Teens</div>
        <div class="tl-sub">Budapest · Hungary</div>
      </div>
    </li>  

    <li class="tl-item down" style="--stem: 130px;" data-key="seoul-south-korea">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Keynote</span>
        <div class="tl-range">2016</div>
        <h4 class="tl-title">DataX</h4>
        <div class="tl-sub">Innovation Enterprise</div>
        <div class="tl-sub">Seoul · South Korea</div>
      </div>
    </li>   

    <li class="tl-item up" style="--stem: 130px;" data-key="hong-kong">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Speaker</span>
        <div class="tl-range">2017</div>
        <h4 class="tl-title">Big Data &amp; Analytics for Banking Summit</h4>
        <div class="tl-sub">Innovation Enterprise</div>
        <div class="tl-sub">Hong Kong</div>
      </div>
    </li>
    
    <li class="tl-item down" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2017-2018 · 1 year</div>
        <h4 class="tl-title">Director of Advanced Analytics &amp; Research</h4>
        <div class="tl-sub">Education First - Kids and Teens</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="hong-kong">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Keynote</span>
        <div class="tl-range">2017</div>
        <h4 class="tl-title">Big Data &amp; Analytics Innovation Summit</h4>
        <div class="tl-sub">Innovation Enterprise</div>
        <div class="tl-sub">Hong Kong</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 130px;" data-key="singapore">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Workshop</span>
        <div class="tl-range">2017</div>
        <h4 class="tl-title">Regional Division Conference</h4>
        <div class="tl-sub">Education First - Kids &amp; Teens</div>
        <div class="tl-sub">Singapore</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Chairperson</span>
        <div class="tl-range">2017</div>
        <h4 class="tl-title">Chief Innovation Officer Summit</h4>
        <div class="tl-sub">Innovation Enterprise</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>   

    <li class="tl-item down" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Speaker</span>
        <div class="tl-range">2017</div>
        <h4 class="tl-title">Global Marketing and Tech Innovation Summit</h4>
        <div class="tl-sub">Innovation Enterprise</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Speaker</span>
        <div class="tl-range">2017</div>
        <h4 class="tl-title">A Jump Start to Internal Analytical Capabilities</h4>
        <div class="tl-sub">American Chamber of Commerce</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>   
    
<!--            -->
<!-- START 2018 -->
<!--            -->
    <li class="tl-item down" style="--stem: 115px;" data-key="paris-france">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2018</div>
        <h4 class="tl-title">Guest Speaker</h4>
        <div class="tl-sub">ParisTech University</div>
        <div class="tl-sub">Paris · France</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="siem-reap-cambodia">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Workshop</span>
        <div class="tl-range">2018</div>
        <h4 class="tl-title">Regional Division Conference</h4>
        <div class="tl-sub">Education First - Kids &amp; Teens</div>
        <div class="tl-sub">Siem Reap · Cambodia</div>
      </div>
    </li>    

    <li class="tl-item down" style="--stem: 130px;" data-key="shanghai-china">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Chairperson</span>
        <div class="tl-range">2018</div>
        <h4 class="tl-title">DataX</h4>
        <div class="tl-sub">Innovation Enterprise</div>
        <div class="tl-sub">Shanghai · China</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="new-orleans-usa">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Workshop</span>
        <div class="tl-range">2018</div>
        <h4 class="tl-title">Global Division Conference</h4>
        <div class="tl-sub">Education First - Kids &amp; Teens</div>
        <div class="tl-sub">New Orleans · USA</div>
      </div>
    </li>    
    
    <li class="tl-item down" style="--stem: 130px;" data-key="san-francisco-usa">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2018-Present · 7+ years</div>
        <h4 class="tl-title">Faculty of Analytics</h4>
        <div class="tl-sub">Hult International Business School</div>
        <div class="tl-sub">San Francisco · USA</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="san-francisco-usa">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Publication</span>
        <div class="tl-range">2019</div>
        <h4 class="tl-title">From Print to Prediction - </h4>
        <h4 class="tl-title">A Beginner's Guide to Data Analysis in Python</h4>
        <div class="tl-sub">San Francisco · USA</div>
      </div>
    </li>    
    
    <li class="tl-item down" style="--stem: 115px;" data-key="new-york-city-usa">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2022</div>
        <h4 class="tl-title">Faculty (Visiting)</h4>
        <div class="tl-sub">Hult International Business School</div>
        <div class="tl-sub">New York City · USA</div>
      </div>
    </li>

    <li class="tl-item up" style="--stem: 130px;" data-key="san-francisco-usa">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--pres">Panel Host</span>
        <div class="tl-range">2025</div>
        <h4 class="tl-title">Autodesk Analytics in Action</h4>
        <div class="tl-sub">AutoDesk</div>
        <div class="tl-sub">San Francisco · USA</div>
      </div>
    </li>

    <li class="tl-item down" style="--stem: 115px;" data-key="new-york-city-usa">
      <span class="tick"></span>
      <span class="stem"></span>
      <div class="card">
        <span class="tl-pill tl-pill--work">Work</span>
        <div class="tl-range">2025</div>
        <h4 class="tl-title">Faculty (Visiting)</h4>
        <div class="tl-sub">Hult International Business School</div>
        <div class="tl-sub">New York City · USA</div>
      </div>
    </li>
    </ol>

  <!-- scroll buttons -->
  <button class="tl-nudge tl-nudge--left"  aria-label="Scroll timeline left"  type="button">
    <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
      <path d="M15 18l-6-6 6-6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  </button>
  <button class="tl-nudge tl-nudge--right" aria-label="Scroll timeline right" type="button">
    <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
      <path d="M9 6l6 6-6 6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  </button>

  </div>
</div>

<!----------------------------->
<!-- Chips UNDER the timeline -->
<!----------------------------->
<div class="fullbleed">
  <div class="chip-marquee" aria-label="Expertise">
    <div class="chips chip-track">
      <!-- set #1 -->
      <span class="chip">10-Time Faculty of the Year</span>
      <span class="chip">Machine Learning</span>
      <span class="chip">AI</span>
      <span class="chip">Analytics</span>
      <span class="chip">Python</span>
      <span class="chip">SQL</span>
      <span class="chip">R</span>
      <span class="chip">HTML5</span>
      <span class="chip">CSS</span>
      <span class="chip">Jupyter</span>
      <span class="chip">scikit-learn</span>
      <span class="chip">PyTorch</span>
      <span class="chip">Bilingual</span>

      <!-- set #2 (duplicate for seamless scroll) -->
      <span class="chip">10-Time Faculty of the Year</span>
      <span class="chip">Machine Learning</span>
      <span class="chip">AI</span>
      <span class="chip">Analytics</span>
      <span class="chip">Python</span>
      <span class="chip">SQL</span>
      <span class="chip">R</span>
      <span class="chip">HTML5</span>
      <span class="chip">CSS</span>
      <span class="chip">Jupyter</span>
      <span class="chip">scikit-learn</span>
      <span class="chip">PyTorch</span>
      <span class="chip">Bilingual</span>
    </div>
  </div>
</div>

<!-------------->
<!-- Scripts  -->
<!-------------->

<script>
/* Clone the legend from INSIDE the iframe into our .legend-proxy (same-origin) */
(function(){
  const iframe = document.getElementById('career-map-iframe');
  const proxy  = document.querySelector('.legend-proxy');

  function mirrorLegend(){
    try{
      const doc = iframe.contentDocument || iframe.contentWindow?.document;
      if (!doc) return;
      const src = doc.querySelector('.map-legend');  // legend already inside career_map2.html
      if (!src) return;

      // Copy the legend items into the proxy; keep layout via our CSS
      proxy.innerHTML = src.innerHTML;

      // Hide the legend inside the iframe to avoid duplication
      src.style.display = 'none';
      src.setAttribute('aria-hidden', 'true');
    }catch(e){ /* ignore cross-origin issues if any */ }
  }

  if (iframe){ iframe.addEventListener('load', mirrorLegend); }
})();
</script>

<script>
/* Timeline ↔ Map messaging (unchanged logic) */
(function(){
  const mapFrame = document.querySelector('.map-viewport iframe');
  const tlList   = document.querySelector('.timeline .tl-list');

  const leftBtn  = document.querySelector('.timeline .tl-nudge--left');
  const rightBtn = document.querySelector('.timeline .tl-nudge--right');

  // read --tl-track (defaults to 200 if not found)
  const rootStyles = getComputedStyle(document.documentElement);
  const step = parseInt(rootStyles.getPropertyValue('--tl-track')) || 200;

  function updateNudges(){
    if (!tlList || !leftBtn || !rightBtn) return;
    const max = tlList.scrollWidth - tlList.clientWidth - 1;
    const x   = tlList.scrollLeft;
    leftBtn.style.visibility  = x <= 2 ? 'hidden' : 'visible';
    rightBtn.style.visibility = x >= max ? 'hidden' : 'visible';
  }
  leftBtn?.addEventListener('click',  ()=> tlList?.scrollBy({ left: -step*2, behavior:'smooth' }));
  rightBtn?.addEventListener('click', ()=> tlList?.scrollBy({ left:  step*2, behavior:'smooth' }));
  tlList?.addEventListener('scroll', updateNudges);
  window.addEventListener('resize', updateNudges);
  updateNudges();

  const itemsByKey = {};

  function slug(s){
    return String(s || '').toLowerCase()
      .replace(/<[^>]+>/g,'')
      .replace(/&[^;]+;/g,' ')
      .replace(/[^a-z0-9]+/g,'-')
      .replace(/^-+|-+$/g,'');
  }

  // index timeline items
  document.querySelectorAll('.timeline .tl-item[data-key]').forEach(el=>{
    const key = el.getAttribute('data-key').trim().toLowerCase();
    itemsByKey[key] = el;
    el.addEventListener('click', ()=>{
      if (mapFrame?.contentWindow) {
        mapFrame.contentWindow.postMessage({type:'showCity', key}, '*');
      }
      activate(key);
    });
  });

  function activate(key){
    document.querySelectorAll('.timeline .tl-item.is-active')
      .forEach(el=>el.classList.remove('is-active'));
    const el = itemsByKey[key];
    if (!el || !tlList) return;
    el.classList.add('is-active');
    const target = el.offsetLeft - (tlList.clientWidth - el.clientWidth)/2;
    tlList.scrollTo({left: Math.max(0,target), behavior:'smooth'});
  }

  // map -> timeline
  window.addEventListener('message', (ev)=>{
    const data = ev.data || {};
    if (data.type === 'mapClick' && data.key){ activate(data.key); }
  });

  mapFrame?.addEventListener('load', ()=>{
    const w = mapFrame.contentWindow, d = w.document;
    const code = `
      (function(){
        function ready(fn){
          if (document.readyState !== 'loading') fn();
          else document.addEventListener('DOMContentLoaded', fn);
        }
        function slug(s){
          return String(s || '').toLowerCase()
            .replace(/<[^>]+>/g,'')
            .replace(/&[^;]+;/g,' ')
            .replace(/[^a-z0-9]+/g,'-')
            .replace(/^-+|-+$/g,'');
        }
        ready(function(){
          var L = window.L; if (!L) return;

          // find map
          var map = null;
          for (var k in window){
            try { if (window[k] instanceof L.Map){ map = window[k]; break; } } catch(e){}
          }
          if (!map) return;

          var markersByKey = {};
          var currentKey = null;  // track what's open

          // open exactly one thing at a time
          function openForKey(key){
            if (!key || !markersByKey[key]) return;
            try { map.closeTooltip(); } catch(e){}
            try { map.closePopup(); }   catch(e){}
            if (currentKey && markersByKey[currentKey] && currentKey !== key){
              try { markersByKey[currentKey].closeTooltip && markersByKey[currentKey].closeTooltip(); } catch(e){}
              try { markersByKey[currentKey].closePopup   && markersByKey[currentKey].closePopup(); }   catch(e){}
            }
            var layer = markersByKey[key];
            try {
              if (layer.getTooltip && layer.getTooltip()) layer.openTooltip();
              else if (layer.getPopup && layer.getPopup()) layer.openPopup();
            } catch(e){}
            try {
              var center = layer.getLatLng ? layer.getLatLng()
                         : (layer.getBounds ? layer.getBounds().getCenter() : null);
              if (center) map.setView(center, map.getZoom(), {animate:true});
            } catch(e){}
            currentKey = key;
          }

          function indexLayer(layer){
            try{
              var txt = '';
              if (layer.getTooltip && layer.getTooltip()) txt = layer.getTooltip().getContent();
              else if (layer.getPopup && layer.getPopup()) txt = layer.getPopup().getContent();
              else if (layer.options && layer.options.title) txt = layer.options.title;

              var first = String(txt || '').split('<br')[0];
              var key = slug(first);

              var pos = null;
              if (layer.getLatLng) pos = layer.getLatLng();
              else if (layer.getBounds){ try{ pos = layer.getBounds().getCenter(); }catch(e){} }

              if (key && pos){
                layer.__key = key;
                markersByKey[key] = layer;

                // map click → parent, but also enforce single open here
                if (layer.on){
                  layer.on('click', function(){
                    openForKey(this.__key);
                    window.parent.postMessage({type:'mapClick', key: this.__key}, '*');
                  });
                }
              }

              if (layer.eachLayer) layer.eachLayer(indexLayer);
            }catch(e){}
          }

          function buildIndex(){
            try { map.eachLayer(indexLayer); } catch(e){}
          }

          map.whenReady(function(){
            buildIndex();
            setTimeout(buildIndex, 250); // in case layers add late
          });

          // parent → map (timeline click)
          window.addEventListener('message', function(ev){
            var data = ev.data || {};
            if (data.type === 'showCity' && data.key){
              openForKey(data.key);
            }
          });

          window.__markersByKey = markersByKey; // debug
        });
      })();`;
    const s = d.createElement('script');
    s.type = 'text/javascript';
    s.textContent = code;
    d.body.appendChild(s);
  });
})();
</script>
