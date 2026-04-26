# B.Tech Second Year Notes

This repository contains curated notes for the second year of the B.Tech curriculum, organized by semester.

## Navigation

- [Semester 3 Notes](./Semester3/README.md)
- [Semester 4 Notes](./Semester4/README.md)

---

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>ZenYukti — Notes Footer</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Mono:ital,wght@0,400;0,500;1,400&family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,400&display=swap" rel="stylesheet"/>

<style>
  /* ── Reset & Base ─────────────────────────────────────────────────── */
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --zy-ink:        #1A1740;
    --zy-deep:       #26215C;
    --zy-mid:        #3C3489;
    --zy-core:       #534AB7;
    --zy-soft:       #7F77DD;
    --zy-mist:       #AFA9EC;
    --zy-pale:       #EEEDFE;
    --zy-white:      #FFFFFF;
    --zy-ghost:      #F5F4FC;

    --social-li:     #0A66C2;
    --social-x:      #0F0F0F;
    --social-ig:     #E1306C;
    --social-wa:     #25D366;
    --social-gh:     #24292F;
    --social-yt:     #FF0000;
    --social-dc:     #5865F2;

    --radius-card:   18px;
    --radius-sm:     10px;
    --radius-pill:   100px;

    --shadow-card:   0 8px 40px rgba(26,23,64,.13), 0 1px 4px rgba(26,23,64,.08);
    --shadow-icon:   0 4px 14px rgba(0,0,0,.22);
  }

  body {
    font-family: 'DM Sans', sans-serif;
    background: #F0EFF9;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 48px 20px;
  }

  /* ── Wrapper ──────────────────────────────────────────────────────── */
  .zy-wrap {
    width: 100%;
    max-width: 760px;
  }

  /* ── Divider ──────────────────────────────────────────────────────── */
  .zy-divider {
    display: flex;
    align-items: center;
    gap: 14px;
    margin-bottom: 32px;
  }
  .zy-divider-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, transparent, var(--zy-mist), transparent);
  }
  .zy-divider-badge {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    font-weight: 500;
    letter-spacing: .18em;
    text-transform: uppercase;
    color: var(--zy-white);
    background: var(--zy-core);
    padding: 5px 16px;
    border-radius: var(--radius-pill);
    white-space: nowrap;
    box-shadow: 0 2px 12px rgba(83,74,183,.35);
  }

  /* ── Card ─────────────────────────────────────────────────────────── */
  .zy-card {
    border-radius: var(--radius-card);
    overflow: hidden;
    box-shadow: var(--shadow-card);
    border: 1px solid rgba(83,74,183,.12);
  }

  /* ── Header ───────────────────────────────────────────────────────── */
  .zy-header {
    background: linear-gradient(130deg, var(--zy-ink) 0%, var(--zy-deep) 35%, var(--zy-core) 75%, var(--zy-soft) 100%);
    padding: 28px 30px 26px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 20px;
    flex-wrap: wrap;
    position: relative;
    overflow: hidden;
  }

  /* subtle grid texture on header */
  .zy-header::before {
    content: '';
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(255,255,255,.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,255,255,.04) 1px, transparent 1px);
    background-size: 32px 32px;
    pointer-events: none;
  }

  /* decorative circle blur */
  .zy-header::after {
    content: '';
    position: absolute;
    width: 220px;
    height: 220px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(127,119,221,.25) 0%, transparent 70%);
    top: -60px;
    right: -40px;
    pointer-events: none;
  }

  .zy-brand {
    display: flex;
    align-items: center;
    gap: 16px;
    position: relative;
    z-index: 1;
  }

  /* ── Logo placeholder (replace src with real logo) ─────────────────── */
  .zy-logo {
    width: 50px;
    height: 50px;
    border-radius: 13px;
    border: 1.5px solid rgba(255,255,255,.28);
    background: rgba(255,255,255,.12);
    overflow: hidden;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  /* When you have a real logo, replace the <img> src below */
  .zy-logo img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }
  /* Fallback monogram shown when image fails / placeholder used */
  .zy-logo-fallback {
    font-family: 'DM Mono', monospace;
    font-size: 17px;
    font-weight: 500;
    color: #fff;
    letter-spacing: -1px;
    line-height: 1;
  }

  .zy-brand-text .name {
    font-family: 'Syne', sans-serif;
    font-size: 22px;
    font-weight: 800;
    color: var(--zy-white);
    letter-spacing: -.3px;
    line-height: 1.1;
  }
  .zy-brand-text .sub {
    font-size: 12.5px;
    color: rgba(255,255,255,.6);
    font-weight: 400;
    margin-top: 3px;
    font-family: 'DM Sans', sans-serif;
  }

  .zy-website-pill {
    position: relative;
    z-index: 1;
    display: inline-flex;
    align-items: center;
    gap: 7px;
    background: rgba(255,255,255,.1);
    border: 1px solid rgba(255,255,255,.22);
    border-radius: var(--radius-sm);
    padding: 8px 16px;
    font-family: 'DM Mono', monospace;
    font-size: 12.5px;
    color: rgba(255,255,255,.9);
    text-decoration: none;
    transition: background .18s, border-color .18s;
    backdrop-filter: blur(6px);
  }
  .zy-website-pill:hover {
    background: rgba(255,255,255,.18);
    border-color: rgba(255,255,255,.4);
    color: #fff;
  }
  .zy-website-pill svg { opacity: .75; flex-shrink: 0; }

  /* ── Two link cards ───────────────────────────────────────────────── */
  .zy-links-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    background: var(--zy-white);
    border-top: 1px solid var(--zy-pale);
  }

  .zy-link-card {
    display: flex;
    align-items: flex-start;
    gap: 15px;
    padding: 22px 26px;
    text-decoration: none;
    transition: background .16s;
  }
  .zy-link-card:first-child { border-right: 1px solid var(--zy-pale); }
  .zy-link-card:hover { background: var(--zy-ghost); }

  .zy-link-icon {
    width: 42px;
    height: 42px;
    border-radius: 11px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }
  .zy-link-icon.gh  { background: var(--zy-pale); }
  .zy-link-icon.dc  { background: #D5F0C0; }

  .zy-link-title {
    font-family: 'Syne', sans-serif;
    font-size: 13.5px;
    font-weight: 700;
    color: var(--zy-ink);
    margin-bottom: 4px;
  }
  .zy-link-desc {
    font-size: 12px;
    color: #6B6894;
    line-height: 1.5;
    margin-bottom: 7px;
  }
  .zy-link-url {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--zy-core);
    text-decoration: none;
    display: inline-block;
  }
  .zy-link-url:hover { text-decoration: underline; }

  /* ── Socials bar ──────────────────────────────────────────────────── */
  .zy-socials {
    background: var(--zy-ghost);
    border-top: 1px solid var(--zy-pale);
    padding: 16px 26px;
    display: flex;
    align-items: center;
    gap: 10px;
    flex-wrap: wrap;
  }

  .zy-socials-label {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: .14em;
    text-transform: uppercase;
    color: var(--zy-mist);
    margin-right: 4px;
    flex-shrink: 0;
  }

  .zy-social-icon {
    width: 36px;
    height: 36px;
    border-radius: 9px;
    display: flex;
    align-items: center;
    justify-content: center;
    text-decoration: none;
    transition: transform .16s cubic-bezier(.34,1.56,.64,1), box-shadow .16s;
    flex-shrink: 0;
  }
  .zy-social-icon:hover {
    transform: translateY(-3px);
    box-shadow: var(--shadow-icon);
  }
  .zy-social-icon svg { display: block; }

  .si-li  { background: var(--social-li); }
  .si-x   { background: var(--social-x);  }
  .si-ig  { background: linear-gradient(135deg, #f09433 0%, #e6683c 25%, #dc2743 50%, #cc2366 75%, #bc1888 100%); }
  .si-wa  { background: var(--social-wa); }
  .si-gh  { background: var(--social-gh); }
  .si-yt  { background: var(--social-yt); }
  .si-dc  { background: var(--social-dc); }

  .zy-socials-sep {
    width: 1px;
    height: 22px;
    background: var(--zy-pale);
    flex-shrink: 0;
    margin: 0 2px;
  }

  /* ── Footer base ──────────────────────────────────────────────────── */
  .zy-base {
    background: var(--zy-white);
    border-top: 1px solid var(--zy-pale);
    padding: 14px 26px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 10px;
  }
  .zy-base-text {
    font-size: 11.5px;
    color: #9896BE;
  }
  .zy-base-text strong { color: var(--zy-mid); font-weight: 600; }

  .zy-tags {
    display: flex;
    gap: 6px;
    flex-wrap: wrap;
  }
  .zy-tag {
    font-size: 10.5px;
    font-weight: 500;
    padding: 3px 10px;
    border-radius: var(--radius-pill);
    background: var(--zy-pale);
    color: var(--zy-mid);
    letter-spacing: .02em;
    font-family: 'DM Sans', sans-serif;
  }

  /* ── Responsive ───────────────────────────────────────────────────── */
  @media (max-width: 520px) {
    .zy-links-row  { grid-template-columns: 1fr; }
    .zy-link-card:first-child { border-right: none; border-bottom: 1px solid var(--zy-pale); }
    .zy-header     { flex-direction: column; align-items: flex-start; }
    .zy-base       { flex-direction: column; align-items: flex-start; }
  }
</style>
</head>
<body>

<div class="zy-wrap">

  <!-- ── Divider ── -->
  <div class="zy-divider">
    <div class="zy-divider-line"></div>
    <div class="zy-divider-badge">End of Notes</div>
    <div class="zy-divider-line"></div>
  </div>

  <div class="zy-card">

    <!-- ── Header ── -->
    <div class="zy-header">
      <div class="zy-brand">

        <!-- LOGO: replace the src below with your actual logo file path/URL -->
        <!-- If no image, the fallback monogram "ZY" is shown automatically -->
        <div class="zy-logo">
          <img
            src="https://zenyukti.in/assets/logo.png"
            alt="ZenYukti Logo"
            onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';"
          />
          <span class="zy-logo-fallback" style="display:none;">ZY</span>
        </div>

        <div class="zy-brand-text">
          <div class="name">ZenYukti</div>
          <div class="sub">Quick Exam Notes</div>
        </div>
      </div>

      <a href="https://zenyukti.in" class="zy-website-pill" target="_blank" rel="noopener">
        <svg width="13" height="13" viewBox="0 0 16 16" fill="none">
          <circle cx="8" cy="8" r="6.5" stroke="currentColor" stroke-width="1.3"/>
          <ellipse cx="8" cy="8" rx="2.8" ry="6.5" stroke="currentColor" stroke-width="1.3"/>
          <path d="M1.5 8h13" stroke="currentColor" stroke-width="1.3"/>
        </svg>
        zenyukti.in
      </a>
    </div>

    <!-- ── Two link cards ── -->
    <div class="zy-links-row">

      <a href="https://github.com/ZenYukti/MyNotes" class="zy-link-card" target="_blank" rel="noopener">
        <div class="zy-link-icon gh">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="none">
            <path d="M12 2C6.477 2 2 6.484 2 12.021c0 4.427 2.865 8.184 6.839 9.504.5.09.682-.217.682-.482 0-.237-.009-.868-.013-1.703-2.782.605-3.369-1.342-3.369-1.342-.454-1.156-1.11-1.462-1.11-1.462-.908-.62.069-.608.069-.608 1.003.071 1.531 1.031 1.531 1.031.892 1.529 2.341 1.089 2.912.833.091-.647.35-1.089.636-1.339-2.22-.252-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.578 9.578 0 0112 6.836a9.59 9.59 0 012.504.338c1.909-1.296 2.747-1.026 2.747-1.026.546 1.378.202 2.397.1 2.65.64.7 1.027 1.595 1.027 2.688 0 3.848-2.339 4.695-4.566 4.942.359.309.678.92.678 1.855 0 1.339-.012 2.419-.012 2.749 0 .268.18.577.688.48C19.138 20.2 22 16.447 22 12.021 22 6.484 17.523 2 12 2z" fill="#3C3489"/>
          </svg>
        </div>
        <div>
          <div class="zy-link-title">Other Unit Notes</div>
          <div class="zy-link-desc">All subject notes on GitHub — free to access &amp; star</div>
          <span class="zy-link-url">github.com/ZenYukti/MyNotes</span>
        </div>
      </a>

      <a href="https://go.zenyukti.in/discord" class="zy-link-card" target="_blank" rel="noopener">
        <div class="zy-link-icon dc">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="none">
            <path d="M20.317 4.37a19.791 19.791 0 00-4.885-1.515.074.074 0 00-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 00-5.487 0 12.64 12.64 0 00-.617-1.25.077.077 0 00-.079-.037A19.736 19.736 0 003.677 4.37a.07.07 0 00-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 00.031.057 19.9 19.9 0 005.993 3.03.078.078 0 00.084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 00-.041-.106 13.107 13.107 0 01-1.872-.892.077.077 0 01-.008-.128 10.2 10.2 0 00.372-.292a.074.074 0 01.077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 01.078.01c.12.098.246.198.373.292a.077.077 0 01-.006.127 12.299 12.299 0 01-1.873.892.077.077 0 00-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 00.084.028 19.839 19.839 0 006.002-3.03.077.077 0 00.032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 00-.031-.03z" fill="#3B6D11"/>
          </svg>
        </div>
        <div>
          <div class="zy-link-title">Join ZenYukti Discord</div>
          <div class="zy-link-desc">Free workspace — internship &amp; hackathon updates, tech discussions</div>
          <span class="zy-link-url">go.zenyukti.in/discord</span>
        </div>
      </a>

    </div>

    <!-- ── Socials bar ── -->
    <div class="zy-socials">
      <span class="zy-socials-label">Find us on</span>

      <!-- LinkedIn -->
      <a href="https://linkedin.com/company/zenyukti" class="zy-social-icon si-li" target="_blank" rel="noopener" title="LinkedIn">
        <svg width="17" height="17" viewBox="0 0 24 24" fill="#fff">
          <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
        </svg>
      </a>

      <!-- Twitter / X -->
      <a href="https://twitter.com/zenyukti" class="zy-social-icon si-x" target="_blank" rel="noopener" title="Twitter / X">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="#fff">
          <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-4.714-6.231-5.401 6.231H2.746l7.73-8.835L1.254 2.25H8.08l4.258 5.63 5.906-5.63zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
        </svg>
      </a>

      <!-- Instagram -->
      <a href="https://instagram.com/zenyukti" class="zy-social-icon si-ig" target="_blank" rel="noopener" title="Instagram">
        <svg width="17" height="17" viewBox="0 0 24 24" fill="#fff">
          <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/>
        </svg>
      </a>

      <!-- WhatsApp -->
      <a href="https://whatsapp.com/channel/zenyukti" class="zy-social-icon si-wa" target="_blank" rel="noopener" title="WhatsApp">
        <svg width="17" height="17" viewBox="0 0 24 24" fill="#fff">
          <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
        </svg>
      </a>

      <!-- GitHub -->
      <a href="https://github.com/ZenYukti" class="zy-social-icon si-gh" target="_blank" rel="noopener" title="GitHub">
        <svg width="17" height="17" viewBox="0 0 24 24" fill="#fff">
          <path d="M12 2C6.477 2 2 6.484 2 12.021c0 4.427 2.865 8.184 6.839 9.504.5.09.682-.217.682-.482 0-.237-.009-.868-.013-1.703-2.782.605-3.369-1.342-3.369-1.342-.454-1.156-1.11-1.462-1.11-1.462-.908-.62.069-.608.069-.608 1.003.071 1.531 1.031 1.531 1.031.892 1.529 2.341 1.089 2.912.833.091-.647.35-1.089.636-1.339-2.22-.252-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.578 9.578 0 0112 6.836a9.59 9.59 0 012.504.338c1.909-1.296 2.747-1.026 2.747-1.026.546 1.378.202 2.397.1 2.65.64.7 1.027 1.595 1.027 2.688 0 3.848-2.339 4.695-4.566 4.942.359.309.678.92.678 1.855 0 1.339-.012 2.419-.012 2.749 0 .268.18.577.688.48C19.138 20.2 22 16.447 22 12.021 22 6.484 17.523 2 12 2z"/>
        </svg>
      </a>

      <!-- YouTube -->
      <a href="https://youtube.com/@zenyukti" class="zy-social-icon si-yt" target="_blank" rel="noopener" title="YouTube">
        <svg width="17" height="17" viewBox="0 0 24 24" fill="#fff">
          <path d="M23.498 6.186a3.016 3.016 0 00-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 00.502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 002.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 002.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
        </svg>
      </a>

      <!-- Discord -->
      <a href="https://go.zenyukti.in/discord" class="zy-social-icon si-dc" target="_blank" rel="noopener" title="Discord">
        <svg width="17" height="17" viewBox="0 0 24 24" fill="#fff">
          <path d="M20.317 4.37a19.791 19.791 0 00-4.885-1.515.074.074 0 00-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 00-5.487 0 12.64 12.64 0 00-.617-1.25.077.077 0 00-.079-.037A19.736 19.736 0 003.677 4.37a.07.07 0 00-.032.027C.533 9.046-.32 13.58.099 18.057a.082.082 0 00.031.057 19.9 19.9 0 005.993 3.03.078.078 0 00.084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 00-.041-.106 13.107 13.107 0 01-1.872-.892.077.077 0 01-.008-.128 10.2 10.2 0 00.372-.292a.074.074 0 01.077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 01.078.01c.12.098.246.198.373.292a.077.077 0 01-.006.127 12.299 12.299 0 01-1.873.892.077.077 0 00-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 00.084.028 19.839 19.839 0 006.002-3.03.077.077 0 00.032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 00-.031-.03z"/>
        </svg>
      </a>

    </div>

    <!-- ── Footer base ── -->
    <div class="zy-base">
      <p class="zy-base-text">Made with care by <strong>ZenYukti</strong> &nbsp;·&nbsp; Share freely, learn together</p>
      <div class="zy-tags">
        <span class="zy-tag">Quick Exam Notes</span>
        <span class="zy-tag">Exam Ready</span>
        <span class="zy-tag">Free Resource</span>
      </div>
    </div>

  </div>
</div>

</body>
</html>
