<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>SBFI Procurement — Roles &amp; Workflows</title>
<style>
  /* ============================================================
     Apple-inspired design system
     ============================================================ */
  :root {
    --bg:            #ffffff;
    --bg-alt:        #fbfbfd;
    --bg-grey:       #f5f5f7;
    --bg-dark:       #000000;
    --bg-deep:       #0a0a0a;

    --text:          #1d1d1f;
    --text-2:        #515154;
    --text-3:        #86868b;
    --text-on-dark:  #f5f5f7;
    --text-on-dark-2:#a1a1a6;

    --line:          rgba(0,0,0,0.08);
    --line-dark:     rgba(255,255,255,0.10);

    --accent:        #0066cc;          /* Apple blue – familiar */
    --suntory:       #0E4D7B;          /* Suntory deep blue */
    --suntory-2:     #2E8FB5;          /* Suntory cyan-dark */
    --suntory-3:     #52B5DA;          /* Suntory cyan */
    --warm:          #f5a623;          /* Warm amber accent */

    --radius-s:      10px;
    --radius-m:      18px;
    --radius-l:      28px;
    --radius-xl:     44px;

    --ease:          cubic-bezier(.22,.61,.36,1);
    --ease-out:      cubic-bezier(.16,1,.3,1);

    --maxw:          1280px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale; }
  html { scroll-behavior: smooth; }
  body {
    font-family: "SF Pro Display", "SF Pro Text", -apple-system, BlinkMacSystemFont, "Helvetica Neue", "Segoe UI", Helvetica, Arial, sans-serif;
    color: var(--text);
    background: var(--bg);
    line-height: 1.47;
    font-size: 17px;
    letter-spacing: -0.01em;
  }
  ::selection { background: var(--suntory); color: #fff; }
  a { color: inherit; text-decoration: none; }
  button { font: inherit; color: inherit; cursor: pointer; background: none; border: none; }

  /* ============================================================
     Sticky top nav (Apple style)
     ============================================================ */
  .nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 48px;
    background: rgba(251,251,253,0.72);
    -webkit-backdrop-filter: saturate(180%) blur(20px);
            backdrop-filter: saturate(180%) blur(20px);
    border-bottom: 1px solid var(--line);
    z-index: 100;
    transition: background .4s var(--ease), color .4s var(--ease), border-color .4s var(--ease);
  }
  .nav-inner {
    max-width: var(--maxw);
    margin: 0 auto;
    height: 100%;
    padding: 0 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 14px;
  }
  .nav-brand {
    font-weight: 600;
    letter-spacing: 0.02em;
    color: var(--text);
    white-space: nowrap;
  }
  .nav-brand .dot {
    display: inline-block;
    width: 6px; height: 6px; border-radius: 50%;
    background: var(--suntory-3);
    margin: 0 8px 1px;
    vertical-align: middle;
  }
  .nav-brand .brand-extra {
    font-weight: 400;
    color: var(--text-2);
  }
  @media (max-width: 480px) {
    .nav-brand .dot,
    .nav-brand .brand-extra { display: none; }
    .nav-links { gap: 18px; font-size: 13px; }
  }
  .nav-links { display: flex; gap: 28px; }
  .nav-links a {
    color: var(--text-2);
    transition: color .25s var(--ease);
    font-weight: 400;
  }
  .nav-links a:hover { color: var(--text); }
  .nav.dark { background: rgba(0,0,0,0.72); border-bottom-color: var(--line-dark); }
  .nav.dark .nav-brand { color: #fff; }
  .nav.dark .nav-links a { color: var(--text-on-dark-2); }
  .nav.dark .nav-links a:hover { color: #fff; }

  /* ============================================================
     Section primitives
     ============================================================ */
  section {
    width: 100%;
    overflow: hidden;
    position: relative;
  }
  .container {
    max-width: var(--maxw);
    margin: 0 auto;
    padding: 0 32px;
  }
  .eyebrow {
    text-transform: uppercase;
    letter-spacing: 0.08em;
    font-size: 12px;
    font-weight: 600;
    color: var(--suntory-2);
  }
  .eyebrow.on-dark { color: var(--suntory-3); }

  /* ============================================================
     HERO – pure black, massive type
     ============================================================ */
  .hero {
    min-height: 100vh;
    background: #000;
    color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 120px 24px 80px;
    position: relative;
  }
  /* Subtle radial glow */
  .hero::before {
    content: "";
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at 50% 30%, rgba(82,181,218,0.18), transparent 55%),
                radial-gradient(ellipse at 80% 80%, rgba(245,166,35,0.10), transparent 55%);
    pointer-events: none;
  }
  .hero-eyebrow {
    text-transform: uppercase;
    letter-spacing: 0.18em;
    font-size: 12px;
    color: var(--suntory-3);
    margin-bottom: 28px;
    opacity: 0;
    animation: fadeUp 1s var(--ease-out) .15s forwards;
  }
  .hero h1 {
    font-size: clamp(48px, 9vw, 128px);
    font-weight: 600;
    line-height: 1.02;
    letter-spacing: -0.045em;
    max-width: 16ch;
    background: linear-gradient(180deg, #ffffff 0%, #d8d8dd 100%);
    -webkit-background-clip: text;
            background-clip: text;
    -webkit-text-fill-color: transparent;
    opacity: 0;
    animation: fadeUp 1.1s var(--ease-out) .35s forwards;
  }
  .hero-sub {
    margin-top: 36px;
    max-width: 640px;
    font-size: clamp(18px, 1.6vw, 22px);
    color: var(--text-on-dark-2);
    font-weight: 400;
    line-height: 1.45;
    opacity: 0;
    animation: fadeUp 1.1s var(--ease-out) .55s forwards;
  }
  .hero-cta {
    margin-top: 48px;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    color: var(--suntory-3);
    font-size: 17px;
    font-weight: 500;
    padding: 12px 22px;
    border-radius: 980px;
    background: rgba(82,181,218,0.10);
    border: 1px solid rgba(82,181,218,0.25);
    transition: background .25s var(--ease), transform .25s var(--ease);
    opacity: 0;
    animation: fadeUp 1.1s var(--ease-out) .75s forwards;
  }
  .hero-cta:hover { background: rgba(82,181,218,0.18); transform: translateY(-1px); }
  .hero-cta .arrow {
    display: inline-block;
    transition: transform .35s var(--ease);
  }
  .hero-cta:hover .arrow { transform: translateY(2px); }

  .scroll-indicator {
    position: absolute;
    bottom: 40px; left: 50%; transform: translateX(-50%);
    color: var(--text-on-dark-2);
    font-size: 12px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    opacity: 0;
    animation: fadeIn 1s var(--ease-out) 1.2s forwards;
  }
  .scroll-indicator .line {
    display: block;
    width: 1px; height: 28px; margin: 14px auto 0;
    background: linear-gradient(180deg, var(--text-on-dark-2), transparent);
    animation: scrollDown 2.2s var(--ease-out) infinite;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(28px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
  @keyframes scrollDown {
    0%   { transform: scaleY(0); transform-origin: top; opacity: 1; }
    50%  { transform: scaleY(1); transform-origin: top; opacity: 1; }
    51%  { transform: scaleY(1); transform-origin: bottom; }
    100% { transform: scaleY(0); transform-origin: bottom; opacity: 0; }
  }

  /* ============================================================
     INTRO section
     ============================================================ */
  .intro {
    background: var(--bg);
    padding: 160px 0 120px;
    text-align: center;
  }
  .intro-headline {
    font-size: clamp(36px, 5.5vw, 72px);
    font-weight: 600;
    line-height: 1.06;
    letter-spacing: -0.035em;
    max-width: 22ch;
    margin: 32px auto 0;
  }
  .intro-headline .accent {
    background: linear-gradient(120deg, var(--suntory) 0%, var(--suntory-3) 100%);
    -webkit-background-clip: text;
            background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .intro-sub {
    margin: 36px auto 0;
    max-width: 640px;
    font-size: clamp(18px, 1.5vw, 21px);
    color: var(--text-2);
    line-height: 1.5;
  }
  .stats {
    margin-top: 96px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 20px;
    max-width: 1080px;
    margin-left: auto;
    margin-right: auto;
  }
  @media (max-width: 760px) { .stats { grid-template-columns: repeat(2, 1fr); } }
  .stat {
    padding: 36px 24px;
    border-radius: var(--radius-l);
    background: var(--bg-grey);
    text-align: center;
    transition: transform .35s var(--ease), background .35s var(--ease);
  }
  .stat:hover { transform: translateY(-4px); background: #ededf0; }
  .stat-num {
    font-size: clamp(40px, 5vw, 64px);
    font-weight: 600;
    letter-spacing: -0.04em;
    background: linear-gradient(180deg, var(--suntory) 0%, var(--suntory-2) 100%);
    -webkit-background-clip: text;
            background-clip: text;
    -webkit-text-fill-color: transparent;
    line-height: 1;
  }
  .stat-label {
    margin-top: 14px;
    color: var(--text-2);
    font-size: 14px;
    letter-spacing: 0.01em;
  }

  /* ============================================================
     ROLE EXPLORER — main interactive section
     ============================================================ */
  .roles-section {
    background: var(--bg-grey);
    padding: 160px 0 180px;
  }
  .roles-header {
    text-align: center;
    max-width: 760px;
    margin: 0 auto 90px;
  }
  .roles-header h2 {
    font-size: clamp(40px, 6vw, 80px);
    font-weight: 600;
    line-height: 1.04;
    letter-spacing: -0.04em;
    margin-top: 24px;
  }
  .roles-header h2 .em {
    background: linear-gradient(120deg, var(--suntory) 0%, var(--suntory-3) 100%);
    -webkit-background-clip: text;
            background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .roles-header p {
    margin-top: 28px;
    font-size: 19px;
    color: var(--text-2);
    line-height: 1.5;
  }

  .explorer {
    display: grid;
    grid-template-columns: 320px 1fr;
    gap: 56px;
    align-items: start;
  }
  @media (max-width: 1024px) {
    .explorer { grid-template-columns: 1fr; gap: 40px; }
  }

  /* Left: role list (sticky on desktop) */
  .role-list {
    position: sticky;
    top: 80px;
    display: flex;
    flex-direction: column;
    gap: 6px;
  }
  @media (max-width: 1024px) {
    .role-list {
      position: relative; top: 0;
      flex-direction: row;
      overflow-x: auto;
      gap: 8px;
      padding-bottom: 12px;
      scroll-snap-type: x mandatory;
      -webkit-overflow-scrolling: touch;
    }
    .role-list::-webkit-scrollbar { display: none; }
  }
  .role-list-label {
    text-transform: uppercase;
    font-size: 11px;
    letter-spacing: 0.12em;
    color: var(--text-3);
    font-weight: 600;
    margin: 22px 0 8px;
    padding: 0 16px;
  }
  .role-list-label:first-child { margin-top: 0; }
  @media (max-width: 1024px) { .role-list-label { display: none; } }
  .role-btn {
    text-align: left;
    padding: 14px 16px;
    border-radius: var(--radius-m);
    color: var(--text-2);
    font-size: 16px;
    font-weight: 500;
    transition: all .3s var(--ease);
    position: relative;
    background: transparent;
    line-height: 1.3;
    white-space: nowrap;
    flex-shrink: 0;
  }
  .role-btn:hover { color: var(--text); background: rgba(0,0,0,0.035); }
  .role-btn.active {
    background: #fff;
    color: var(--text);
    font-weight: 600;
    box-shadow: 0 1px 2px rgba(0,0,0,0.04), 0 4px 16px rgba(0,0,0,0.06);
  }
  .role-btn.active::before {
    content: "";
    position: absolute;
    left: 0; top: 50%;
    width: 3px; height: 22px;
    transform: translateY(-50%);
    background: var(--suntory);
    border-radius: 0 3px 3px 0;
  }
  @media (max-width: 1024px) {
    .role-btn.active::before { display: none; }
    .role-btn { white-space: nowrap; }
  }

  /* Right: detail panel */
  .role-detail {
    background: #fff;
    border-radius: var(--radius-xl);
    padding: 56px 56px 64px;
    box-shadow: 0 1px 2px rgba(0,0,0,0.04), 0 30px 60px -20px rgba(0,0,0,0.08);
    min-height: 600px;
    transition: opacity .3s var(--ease);
  }
  @media (max-width: 720px) { .role-detail { padding: 40px 28px 48px; border-radius: var(--radius-l); } }
  .role-detail.fading { opacity: 0; }

  .role-tag {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 6px 14px;
    border-radius: 980px;
    background: rgba(14,77,123,0.08);
    color: var(--suntory);
    font-size: 13px;
    font-weight: 600;
    letter-spacing: 0.01em;
  }
  .role-tag .dot {
    width: 6px; height: 6px; border-radius: 50%;
    background: var(--suntory);
  }
  .role-title {
    margin-top: 24px;
    font-size: clamp(36px, 4.5vw, 56px);
    font-weight: 600;
    line-height: 1.05;
    letter-spacing: -0.035em;
    color: var(--text);
  }
  .role-tagline {
    margin-top: 18px;
    font-size: 22px;
    color: var(--text-2);
    line-height: 1.4;
    font-weight: 400;
    max-width: 32ch;
  }
  .role-description {
    margin-top: 14px;
    font-size: 17px;
    color: var(--text-3);
    line-height: 1.55;
    max-width: 48ch;
  }

  /* Workflow steps */
  .workflow {
    margin-top: 56px;
  }
  .workflow-label {
    text-transform: uppercase;
    font-size: 11px;
    letter-spacing: 0.14em;
    color: var(--text-3);
    font-weight: 600;
    margin-bottom: 28px;
  }
  .workflow-steps {
    display: flex;
    flex-direction: column;
    gap: 0;
    position: relative;
  }
  .workflow-step {
    display: grid;
    grid-template-columns: 56px 1fr;
    gap: 24px;
    padding: 22px 0;
    border-bottom: 1px solid var(--line);
    transition: background .25s var(--ease);
    cursor: default;
  }
  .workflow-step:last-child { border-bottom: none; }
  .workflow-step:hover { background: rgba(14,77,123,0.025); }
  .step-num {
    width: 40px; height: 40px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--suntory) 0%, var(--suntory-2) 100%);
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 600;
    font-size: 15px;
    letter-spacing: -0.01em;
    flex-shrink: 0;
    box-shadow: 0 4px 12px rgba(14,77,123,0.18);
  }
  .step-content { padding-top: 8px; }
  .step-title {
    font-size: 19px;
    font-weight: 600;
    color: var(--text);
    letter-spacing: -0.01em;
  }
  .step-detail {
    margin-top: 6px;
    font-size: 15px;
    color: var(--text-2);
    line-height: 1.55;
  }

  /* Responsibilities & meta */
  .meta-grid {
    margin-top: 56px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 32px;
  }
  @media (max-width: 720px) { .meta-grid { grid-template-columns: 1fr; gap: 28px; } }
  .meta-block { }
  .meta-block-title {
    text-transform: uppercase;
    font-size: 11px;
    letter-spacing: 0.14em;
    color: var(--text-3);
    font-weight: 600;
    margin-bottom: 16px;
  }
  .meta-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .meta-list li {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    font-size: 15px;
    color: var(--text);
    line-height: 1.45;
  }
  .meta-list li::before {
    content: "";
    width: 5px; height: 5px;
    background: var(--suntory-3);
    border-radius: 50%;
    margin-top: 8px;
    flex-shrink: 0;
  }
  .chip-row {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }
  .chip {
    padding: 7px 14px;
    border-radius: 980px;
    background: var(--bg-grey);
    color: var(--text);
    font-size: 13px;
    font-weight: 500;
    border: 1px solid transparent;
    transition: border-color .2s var(--ease);
  }
  .chip:hover { border-color: var(--line); }

  /* ============================================================
     LIFECYCLE — black, three columns
     ============================================================ */
  .lifecycle {
    background: #000;
    color: #fff;
    padding: 160px 0 180px;
  }
  .lifecycle-header {
    text-align: center;
    max-width: 760px;
    margin: 0 auto 90px;
  }
  .lifecycle-header h2 {
    font-size: clamp(40px, 6vw, 80px);
    font-weight: 600;
    line-height: 1.04;
    letter-spacing: -0.04em;
    margin-top: 24px;
  }
  .lifecycle-header h2 .em {
    background: linear-gradient(120deg, var(--suntory-3) 0%, var(--warm) 100%);
    -webkit-background-clip: text;
            background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .lifecycle-header p {
    margin-top: 28px;
    font-size: 19px;
    color: var(--text-on-dark-2);
    line-height: 1.5;
  }

  .phases {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
  }
  @media (max-width: 900px) {
    .phases { grid-template-columns: 1fr; gap: 20px; }
  }
  .phase {
    background: linear-gradient(180deg, #0e0e10 0%, #060607 100%);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: var(--radius-xl);
    padding: 48px 36px;
    transition: transform .4s var(--ease-out), border-color .4s var(--ease-out);
    position: relative;
    overflow: hidden;
  }
  .phase::after {
    content: "";
    position: absolute;
    inset: 0;
    border-radius: var(--radius-xl);
    background: radial-gradient(ellipse at top, rgba(82,181,218,0.10), transparent 60%);
    opacity: 0;
    transition: opacity .5s var(--ease);
    pointer-events: none;
  }
  .phase:hover { transform: translateY(-6px); border-color: rgba(82,181,218,0.25); }
  .phase:hover::after { opacity: 1; }
  .phase-num {
    font-size: 64px;
    font-weight: 600;
    letter-spacing: -0.04em;
    line-height: 1;
    background: linear-gradient(180deg, #fff 0%, #555 100%);
    -webkit-background-clip: text;
            background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .phase-name {
    margin-top: 24px;
    font-size: 28px;
    font-weight: 600;
    letter-spacing: -0.02em;
    color: #fff;
  }
  .phase-desc {
    margin-top: 14px;
    color: var(--text-on-dark-2);
    font-size: 16px;
    line-height: 1.5;
  }
  .phase-roles {
    margin-top: 32px;
    padding-top: 28px;
    border-top: 1px solid rgba(255,255,255,0.08);
  }
  .phase-roles-label {
    text-transform: uppercase;
    font-size: 11px;
    letter-spacing: 0.14em;
    color: var(--text-on-dark-2);
    font-weight: 600;
    margin-bottom: 14px;
  }
  .phase-roles-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }
  .phase-roles-list li {
    color: #f5f5f7;
    font-size: 14px;
    padding: 8px 12px;
    border-radius: var(--radius-s);
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.04);
    transition: background .2s var(--ease);
    cursor: pointer;
  }
  .phase-roles-list li:hover {
    background: rgba(82,181,218,0.10);
    border-color: rgba(82,181,218,0.20);
  }

  /* ============================================================
     CLOSING
     ============================================================ */
  .closing {
    padding: 200px 0 220px;
    text-align: center;
    background: var(--bg);
    position: relative;
  }
  .closing-text {
    font-size: clamp(40px, 6.5vw, 88px);
    font-weight: 600;
    line-height: 1.05;
    letter-spacing: -0.04em;
    max-width: 18ch;
    margin: 0 auto;
  }
  .closing-text .em {
    background: linear-gradient(120deg, var(--suntory) 0%, var(--suntory-3) 60%, var(--warm) 100%);
    -webkit-background-clip: text;
            background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .closing-sub {
    margin: 36px auto 0;
    max-width: 600px;
    font-size: 19px;
    color: var(--text-2);
  }

  /* Footer */
  footer {
    border-top: 1px solid var(--line);
    background: var(--bg-grey);
    padding: 48px 0;
    text-align: center;
    font-size: 13px;
    color: var(--text-3);
  }
  footer .footer-brand { color: var(--text-2); font-weight: 600; }

  /* ============================================================
     Reveal-on-scroll utility
     ============================================================ */
  .reveal {
    opacity: 0;
    transform: translateY(28px);
    transition: opacity .9s var(--ease-out), transform .9s var(--ease-out);
  }
  .reveal.in { opacity: 1; transform: translateY(0); }

  /* Stagger children */
  .reveal.stagger > * {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity .8s var(--ease-out), transform .8s var(--ease-out);
  }
  .reveal.stagger.in > *:nth-child(1) { transition-delay: .05s; opacity: 1; transform: none; }
  .reveal.stagger.in > *:nth-child(2) { transition-delay: .15s; opacity: 1; transform: none; }
  .reveal.stagger.in > *:nth-child(3) { transition-delay: .25s; opacity: 1; transform: none; }
  .reveal.stagger.in > *:nth-child(4) { transition-delay: .35s; opacity: 1; transform: none; }

  /* Smooth detail step entry */
  .workflow-step {
    opacity: 0;
    transform: translateY(8px);
    animation: stepIn .55s var(--ease-out) forwards;
  }
  @keyframes stepIn {
    to { opacity: 1; transform: none; }
  }
</style>
</head>
<body>

<!-- ============================== NAV ============================== -->
<nav class="nav" id="nav">
  <div class="nav-inner">
    <div class="nav-brand">
      SUNTORY <span class="dot"></span><span class="brand-extra">SBFI Procurement</span>
    </div>
    <div class="nav-links">
      <a href="#intro">Overview</a>
      <a href="#roles">Roles</a>
      <a href="#lifecycle">Lifecycle</a>
    </div>
  </div>
</nav>

<!-- ============================== HERO ============================== -->
<section class="hero">
  <div class="hero-eyebrow">SBFI Procurement Policy</div>
  <h1>How procurement actually works.</h1>
  <p class="hero-sub">From the Chief Procurement Officer to the team member raising a Purchase Order — every role, every workflow, beautifully laid out.</p>
  <a href="#roles" class="hero-cta">
    Explore the roles <span class="arrow">↓</span>
  </a>
  <div class="scroll-indicator">
    Scroll
    <span class="line"></span>
  </div>
</section>

<!-- ============================== INTRO ============================== -->
<section class="intro" id="intro">
  <div class="container">
    <div class="reveal">
      <div class="eyebrow">The big picture</div>
      <h2 class="intro-headline">One unified policy. <span class="accent">Many specialised hands.</span></h2>
      <p class="intro-sub">Procurement at SBFI runs on collaboration. A single playbook, executed by clearly defined roles across global, regional and market teams — each with their own authority and workflow.</p>
    </div>

    <div class="stats reveal stagger">
      <div class="stat"><div class="stat-num">9</div><div class="stat-label">Key roles in motion</div></div>
      <div class="stat"><div class="stat-num">3</div><div class="stat-label">Process phases</div></div>
      <div class="stat"><div class="stat-num">5</div><div class="stat-label">Onboarding steps</div></div>
      <div class="stat"><div class="stat-num">1</div><div class="stat-label">Golden rule: No PO, no pay</div></div>
    </div>
  </div>
</section>

<!-- ============================== ROLE EXPLORER ============================== -->
<section class="roles-section" id="roles">
  <div class="container">
    <div class="roles-header reveal">
      <div class="eyebrow">Interactive role explorer</div>
      <h2>Pick a role. <span class="em">See exactly what they do.</span></h2>
      <p>Click any role on the left to discover their tagline, day-to-day responsibilities, the workflow they own, and the people they collaborate with.</p>
    </div>

    <div class="explorer">
      <!-- Left: Role list (sticky) -->
      <aside class="role-list" id="roleList">
        <!-- Populated via JS -->
      </aside>

      <!-- Right: Detail panel -->
      <article class="role-detail reveal" id="roleDetail">
        <!-- Populated via JS -->
      </article>
    </div>
  </div>
</section>

<!-- ============================== LIFECYCLE ============================== -->
<section class="lifecycle" id="lifecycle">
  <div class="container">
    <div class="lifecycle-header reveal">
      <div class="eyebrow on-dark">The procurement lifecycle</div>
      <h2>Three phases. <span class="em">All hands on deck.</span></h2>
      <p>Every procurement journey moves through these three connected phases. Different roles take the lead in each — but everyone plays a part.</p>
    </div>

    <div class="phases reveal stagger">
      <div class="phase">
        <div class="phase-num">01</div>
        <div class="phase-name">Strategy &amp; Planning</div>
        <div class="phase-desc">Aligning early with the business and building forward-looking category strategies.</div>
        <div class="phase-roles">
          <div class="phase-roles-label">Lead roles</div>
          <ul class="phase-roles-list">
            <li data-role="cpo">Chief Procurement Officer</li>
            <li data-role="category">Category Lead / Manager</li>
            <li data-role="stakeholder">Business Stakeholder</li>
          </ul>
        </div>
      </div>
      <div class="phase">
        <div class="phase-num">02</div>
        <div class="phase-name">Source‑to‑Contract</div>
        <div class="phase-desc">Identifying, evaluating, selecting and contracting suppliers — with risk &amp; ESG built in.</div>
        <div class="phase-roles">
          <div class="phase-roles-label">Lead roles</div>
          <ul class="phase-roles-list">
            <li data-role="category">Category Lead / Manager</li>
            <li data-role="cprm">CPRM Lead</li>
            <li data-role="esg">Sustainable Sourcing &amp; ESG Lead</li>
            <li data-role="team">Procurement Team Member</li>
          </ul>
        </div>
      </div>
      <div class="phase">
        <div class="phase-num">03</div>
        <div class="phase-name">Procure‑to‑Pay</div>
        <div class="phase-desc">From requisition to payment — every purchase backed by a valid Purchase Order.</div>
        <div class="phase-roles">
          <div class="phase-roles-label">Lead roles</div>
          <ul class="phase-roles-list">
            <li data-role="requestor">Requestor / Employee</li>
            <li data-role="team">Procurement Team Member</li>
            <li data-role="bu-lead">BU/Market Procurement Lead</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ============================== CLOSING ============================== -->
<section class="closing">
  <div class="container reveal">
    <h2 class="closing-text">One policy. <span class="em">Many hands.</span> Powerful results.</h2>
    <p class="closing-sub">Suntory Beverage and Food International — driving competitive advantage through winning supplier partnerships and effective management of all company spend.</p>
  </div>
</section>

<!-- ============================== FOOTER ============================== -->
<footer>
  <div class="container">
    <div class="footer-brand">SUNTORY · SBFI Procurement</div>
    <div style="margin-top:8px;">An interactive companion to the SBFI Procurement Policy.</div>
  </div>
</footer>

<script>
/* =====================================================================
   ROLE DATA
   ===================================================================== */
const ROLES = [
  {
    id: "cpo",
    group: "Leadership",
    title: "Chief Procurement Officer",
    tagline: "The strategic head of procurement across SBFI.",
    description: "Owns SBFI's procurement strategy, governance and overall performance — and serves as the final approver for high-value commitments.",
    workflow: [
      { t: "Set the strategy",      d: "Defines SBFI's procurement ambition, targets and priorities together with the Procurement Leadership Team." },
      { t: "Approve categories",    d: "Aligns and approves the annual list of categories that require a formal category strategy." },
      { t: "Approve sourcing awards", d: "Final approver for sourcing recommendations — mirrors the BU/Market CFO contract approval thresholds." },
      { t: "Approve bid waivers",   d: "Co-signs every non-competitive bidding waiver with the relevant BU/Market Procurement Lead." },
      { t: "Govern CPRM",           d: "Leads the Commodity Price Risk Management Governance Committee and steers price-risk strategy." },
    ],
    responsibilities: [
      "Set SBFI's procurement direction",
      "Approve high-value sourcing awards",
      "Mirror BU/Market CFO contract thresholds",
      "Chair the Procurement Leadership Team",
    ],
    collaborators: ["PLT", "BU/Market Procurement Leads", "COE Leads", "BU/Market CFOs"],
    tools: ["One Song Sheet", "BTMS", "Coupa"],
  },
  {
    id: "bu-lead",
    group: "Leadership",
    title: "BU/Market Procurement Lead",
    tagline: "Drives procurement execution within their market.",
    description: "Adapts and applies the SBFI policy locally — delivering market results while staying aligned to the global playbook.",
    workflow: [
      { t: "Localise the policy",   d: "Incorporates the SBFI Procurement Policy into the BU/Market policy and resolves local conflicts." },
      { t: "Run sourcing",          d: "Oversees competitive bids and tactical buys within the market." },
      { t: "Approve locally",       d: "Approves purchases within delegated authority — and bid waivers jointly with the SBFI CPO." },
      { t: "Engage stakeholders",   d: "Builds relationships across the BU/Market business and tracks engagement via NPS." },
      { t: "Report performance",    d: "Submits the One Song Sheet for the market on the cadence set by the COE." },
    ],
    responsibilities: [
      "Adapt SBFI policy for the local market",
      "Execute sourcing strategy locally",
      "Co-approve bid waivers with the CPO",
      "Drive local supplier performance",
    ],
    collaborators: ["CPO", "Local Stakeholders", "BU/Market Legal", "BU/Market CFO"],
    tools: ["Coupa", "SAP", "OSS Dashboard"],
  },
  {
    id: "coe-cap",
    group: "Center of Excellence",
    title: "Capability &amp; Intelligence Lead",
    tagline: "The engine of procurement excellence.",
    description: "Drives SBFI-wide procurement initiatives — from policy stewardship to capability building and the One Song Sheet.",
    workflow: [
      { t: "Maintain the policy",   d: "Owns, updates and disseminates the SBFI Procurement Policy across all functions." },
      { t: "Build capability",      d: "Designs training and capability programs for procurement teams across markets." },
      { t: "Run reporting",         d: "Sets the One Song Sheet cadence and consolidates submissions from every team." },
      { t: "Power analytics",       d: "Provides reporting &amp; analytics that inform leadership decisions and improvement." },
    ],
    responsibilities: [
      "Own and maintain the procurement policy",
      "Drive process excellence SBFI-wide",
      "Operate the One Song Sheet dashboard",
      "Develop procurement talent",
    ],
    collaborators: ["CPO", "PLT", "COE Team", "BU/Market Procurement"],
    tools: ["One Song Sheet", "BTMS", "Coupa"],
  },
  {
    id: "category",
    group: "Category Management",
    title: "Category Lead / Manager",
    tagline: "The architect of category strategies.",
    description: "Builds and runs forward-looking strategies for assigned categories — global or BU/Market — and leads end-to-end sourcing.",
    workflow: [
      { t: "Assess the category",   d: "Apply the Decision Framework: spend value, business criticality and supply risk." },
      { t: "Build the strategy",    d: "Use the Market Analysis &amp; Category Strategy Template — covers demand, supply markets, sourcing risks." },
      { t: "Plan sourcing",         d: "Define a Sourcing &amp; Negotiation Strategy with the 6 mandatory elements." },
      { t: "Award suppliers",       d: "Lead the Evaluation Team to score bids and select the supplier(s) maximising SBFI value." },
      { t: "Manage performance",    d: "Run supplier scorecards and drive continuous improvement quarter on quarter." },
    ],
    responsibilities: [
      "Build annual category strategies",
      "Run sourcing events end-to-end",
      "Plan the sourcing calendar",
      "Lead supplier scorecards and reviews",
    ],
    collaborators: ["Business Stakeholders", "Suppliers", "Evaluation Team", "CPRM Lead"],
    tools: ["Coupa Sourcing", "Strategy Template", "Sourcing Calendar"],
  },
  {
    id: "cprm",
    group: "Center of Excellence",
    title: "CPRM Lead",
    tagline: "Manages commodity price risk globally.",
    description: "Builds and governs SBFI's approach to managing price fluctuations in essential commodities, in close partnership with finance.",
    workflow: [
      { t: "Monitor markets",       d: "Track commodity markets and surface price-risk exposure across SBFI." },
      { t: "Convene the committee", d: "Coordinate the CPRM Governance Committee — CPO, Category Leads, regional Finance." },
      { t: "Agree strategies",      d: "Reach consensus on the best risk-management strategy for each commodity." },
      { t: "Cascade to markets",    d: "Pass the agreed strategies to BU/Market procurement teams for execution." },
      { t: "Track &amp; report",        d: "Monitor effectiveness and address concerns escalated by the markets." },
    ],
    responsibilities: [
      "Establish a unified CPRM approach",
      "Govern the CPRM Committee",
      "Mitigate commodity price volatility",
      "Coordinate with regional finance",
    ],
    collaborators: ["CPO", "Category Leads", "Regional Finance", "BU/Market Procurement"],
    tools: ["Hedging tools", "Market intelligence"],
  },
  {
    id: "esg",
    group: "Center of Excellence",
    title: "Sustainable Sourcing &amp; ESG Lead",
    tagline: "Energises Suntory 'Growing for Good' through procurement.",
    description: "Spearheads ESG and sustainable sourcing — building positive value chains across the supplier ecosystem.",
    workflow: [
      { t: "Risk-map suppliers",    d: "Map the supplier base for human-rights and ESG due diligence." },
      { t: "Build ESG strategy",    d: "Align the procurement sustainability strategy to SBFI's overall ESG goals." },
      { t: "Reduce footprint",      d: "Drive Scope 3 emissions reductions across the supply base." },
      { t: "Audit &amp; report",        d: "Build an auditable ESG procurement framework with clear, repeatable criteria." },
    ],
    responsibilities: [
      "Lead ESG strategy for procurement",
      "Reduce Scope 3 GHG emissions",
      "Drive human-rights due diligence",
      "Develop supplier sustainability scorecards",
    ],
    collaborators: ["BU/Market Sustainability", "Suppliers", "Category Leads", "CPO"],
    tools: ["SMETA", "Supplier ESG questionnaires"],
  },
  {
    id: "team",
    group: "Execution",
    title: "Procurement Team Member",
    tagline: "The hands-on practitioner.",
    description: "Runs the day-to-day work of sourcing, supplier management and stakeholder engagement.",
    workflow: [
      { t: "Engage early",          d: "Partner with stakeholders at budgeting, innovation and new-product-introduction stages." },
      { t: "Run tactical buys",     d: "Manage spot buys below threshold — obtain three written quotes when above the limit." },
      { t: "Onboard suppliers",     d: "Run NDA, anti-bribery checks, due diligence, and Coupa/SAP setup." },
      { t: "Deactivate inactive",   d: "Identify suppliers inactive 15+ months or non-compliant — recommend deactivation." },
      { t: "Submit OSS",            d: "Deliver One Song Sheet submissions on the cadence set by the COE." },
    ],
    responsibilities: [
      "Execute sourcing &amp; tactical buys",
      "Manage supplier onboarding &amp; deactivation",
      "Run NPS engagement surveys",
      "Submit One Song Sheet metrics",
    ],
    collaborators: ["Business Stakeholders", "Suppliers", "Category Leads", "Legal"],
    tools: ["Coupa", "SAP", "OSS Dashboard"],
  },
  {
    id: "stakeholder",
    group: "Cross-functional",
    title: "Business Stakeholder",
    tagline: "The voice of the business.",
    description: "Cross-functional partner from R&amp;D, Marketing, Supply Chain or Quality — shaping needs and choosing suppliers with procurement.",
    workflow: [
      { t: "Engage early",          d: "Initiate procurement conversations early — at budgeting and innovation stages." },
      { t: "Define needs",          d: "Co-create requirements and specifications with the procurement team." },
      { t: "Join the Evaluation Team", d: "Participate in supplier evaluation with the right level of seniority to decide." },
      { t: "Co-negotiate",          d: "Help discuss commercial terms with shortlisted suppliers." },
      { t: "Provide feedback",      d: "Complete the annual NPS survey on procurement engagement." },
    ],
    responsibilities: [
      "Define business requirements clearly",
      "Engage procurement early",
      "Participate in supplier evaluation",
      "Provide feedback through NPS",
    ],
    collaborators: ["Procurement Team", "Category Leads", "Suppliers"],
    tools: ["NPS Survey", "RF(x) documents"],
  },
  {
    id: "requestor",
    group: "Cross-functional",
    title: "Requestor / Employee",
    tagline: "Anyone making a purchase for SBFI.",
    description: "Identifies a need and follows the right buying channel — bound by the golden rule: 'No PO, No Payment.'",
    workflow: [
      { t: "Identify the need",     d: "Define what is needed and the quantity required." },
      { t: "Pick the channel",      d: "Choose the right buying channel: PO (Coupa/SAP), catalog, travel desk or P-Card." },
      { t: "Raise the request",     d: "For indirect: raise a Purchase Requisition. For direct: submit through SAP." },
      { t: "Get approval",          d: "Wait for approval from the relevant authority before placing any order." },
      { t: "Confirm the PO",        d: "Never accept goods or services without a confirmed Purchase Order." },
    ],
    responsibilities: [
      "Take ownership of every purchase initiated",
      "Use authorised buying channels only",
      "Confirm a PO exists before accepting deliveries",
      "Disclose any conflicts of interest",
    ],
    collaborators: ["Procurement Team", "Approving Manager", "Suppliers"],
    tools: ["Coupa", "SAP", "Catalogs", "Travel Desk", "P-Card"],
  },
];

/* =====================================================================
   GROUP HELPERS
   ===================================================================== */
const GROUP_ORDER = [
  "Leadership",
  "Center of Excellence",
  "Category Management",
  "Execution",
  "Cross-functional",
];

/* =====================================================================
   RENDER ROLE LIST
   ===================================================================== */
function renderRoleList() {
  const list = document.getElementById("roleList");
  let html = "";

  // Desktop: grouped lists with labels
  // Mobile (handled by CSS): horizontal scroll, labels hidden
  GROUP_ORDER.forEach(group => {
    const items = ROLES.filter(r => r.group === group);
    if (!items.length) return;
    html += `<div class="role-list-label">${group}</div>`;
    items.forEach(role => {
      html += `<button class="role-btn" data-id="${role.id}">${role.title}</button>`;
    });
  });
  list.innerHTML = html;

  list.querySelectorAll(".role-btn").forEach(btn => {
    btn.addEventListener("click", () => selectRole(btn.dataset.id));
  });
}

/* =====================================================================
   RENDER ROLE DETAIL (with smooth fade transition)
   ===================================================================== */
let currentRoleId = null;
function selectRole(id) {
  if (id === currentRoleId) return;
  currentRoleId = id;

  const role = ROLES.find(r => r.id === id);
  if (!role) return;

  // Toggle active state on buttons
  document.querySelectorAll(".role-btn").forEach(b => {
    b.classList.toggle("active", b.dataset.id === id);
  });

  const detail = document.getElementById("roleDetail");
  detail.classList.add("fading");

  setTimeout(() => {
    detail.innerHTML = `
      <span class="role-tag"><span class="dot"></span>${role.group}</span>
      <h3 class="role-title">${role.title}</h3>
      <p class="role-tagline">${role.tagline}</p>
      <p class="role-description">${role.description}</p>

      <div class="workflow">
        <div class="workflow-label">Workflow</div>
        <div class="workflow-steps">
          ${role.workflow.map((s, i) => `
            <div class="workflow-step" style="animation-delay:${i * 0.06}s">
              <div class="step-num">${i + 1}</div>
              <div class="step-content">
                <div class="step-title">${s.t}</div>
                <div class="step-detail">${s.d}</div>
              </div>
            </div>
          `).join("")}
        </div>
      </div>

      <div class="meta-grid">
        <div class="meta-block">
          <div class="meta-block-title">Key responsibilities</div>
          <ul class="meta-list">
            ${role.responsibilities.map(r => `<li>${r}</li>`).join("")}
          </ul>
        </div>
        <div class="meta-block">
          <div class="meta-block-title">Works with</div>
          <div class="chip-row" style="margin-bottom:24px;">
            ${role.collaborators.map(c => `<span class="chip">${c}</span>`).join("")}
          </div>
          <div class="meta-block-title">Tools</div>
          <div class="chip-row">
            ${role.tools.map(t => `<span class="chip">${t}</span>`).join("")}
          </div>
        </div>
      </div>
    `;
    detail.classList.remove("fading");
  }, 200);
}

/* =====================================================================
   SCROLL-TRIGGERED REVEALS
   ===================================================================== */
function setupReveals() {
  const els = document.querySelectorAll(".reveal");
  const obs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add("in");
        obs.unobserve(e.target);
      }
    });
  }, { threshold: 0.12, rootMargin: "0px 0px -60px 0px" });
  els.forEach(el => obs.observe(el));
}

/* =====================================================================
   NAV background switch (light over light sections, dark over hero/lifecycle)
   ===================================================================== */
function setupNavSwitch() {
  const nav = document.getElementById("nav");
  const darkSections = [document.querySelector(".hero"), document.querySelector(".lifecycle")];
  const obs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        nav.classList.add("dark");
      } else {
        // only remove if no dark section is intersecting
        const anyDark = darkSections.some(s => {
          const r = s.getBoundingClientRect();
          return r.top < 60 && r.bottom > 60;
        });
        if (!anyDark) nav.classList.remove("dark");
      }
    });
  }, { rootMargin: "-48px 0px 0px 0px", threshold: 0 });
  darkSections.forEach(s => obs.observe(s));
}

/* =====================================================================
   PHASE-LIST → JUMP TO ROLE
   ===================================================================== */
function setupPhaseJump() {
  document.querySelectorAll(".phase-roles-list li").forEach(li => {
    li.addEventListener("click", () => {
      const id = li.dataset.role;
      if (!id) return;
      // scroll to roles section, then activate role
      const roles = document.getElementById("roles");
      roles.scrollIntoView({ behavior: "smooth", block: "start" });
      setTimeout(() => selectRole(id), 700);
    });
  });
}

/* =====================================================================
   INIT
   ===================================================================== */
document.addEventListener("DOMContentLoaded", () => {
  renderRoleList();
  selectRole("cpo");
  setupReveals();
  setupNavSwitch();
  setupPhaseJump();
});
</script>

</body>
</html>