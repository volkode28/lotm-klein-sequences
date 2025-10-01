<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>LoTM – Klein’s Sequences (9→8)</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <style>
    :root { --fg:#0f172a; --muted:#475569; --bg:#f8fafc; --card:#ffffff; --ring:#e2e8f0; }
    body { font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial; margin:0; color:var(--fg); background:var(--bg); }
    header { padding:2rem 1rem; text-align:center; }
    h1 { margin:0 0 .5rem; font-size:clamp(1.6rem, 4vw, 2.2rem); }
    .sub { color:var(--muted); }
    main { max-width:1000px; margin:0 auto; padding:0 1rem 3rem; }
    .grid { display:grid; gap:1rem; grid-template-columns: 1fr; }
    @media (min-width: 900px) { .grid { grid-template-columns: 1fr 1fr; } }
    .card { background:var(--card); border:1px solid var(--ring); border-radius:18px; padding:1rem 1.2rem; box-shadow:0 1px 3px rgba(0,0,0,.04); }
    .tag { display:inline-block; padding:.2rem .5rem; border-radius:999px; background:#eef2ff; color:#3730a3; font-size:.8rem; margin-right:.4rem; }
    ul { margin:.4rem 0 .6rem 1.1rem; }
    .muted { color:var(--muted); }
    .mermaid { background: #fff; border:1px solid var(--ring); border-radius:18px; padding:1rem; }
    footer { text-align:center; padding:2rem 1rem; color:var(--muted); }
    code { background:#f1f5f9; padding:.1rem .3rem; border-radius:6px; }
  </style>
  <script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
  <script>mermaid.initialize({ startOnLoad: true, theme: 'default' });</script>
</head>
<body>
  <header>
    <h1>Lord of the Mysteries — Klein’s Sequences <span class="muted">(9 → 8)</span></h1>
    <div class="sub">Seer Pathway around <em>Episode 9: “Party”</em></div>
  </header>

  <main>
    <section class="card">
      <h2 style="margin-top:0">Progression</h2>
      <div class="mermaid">
      flowchart TD
        A[Sequence 9 — Seer] -->|Potion Advancement + Acting Method| B[Sequence 8 — Clown]
        A --> A1[Divination & Perception]
        A1 --> A2[Spirit Vision, Intuition, Dream/Meditation]
        B --> B1[Dexterity & Psyche Control]
        B1 --> B2[Balance/Agility, Pain Suppression, Emotion Masking]
      </div>
    </section>

    <section class="grid" id="cards"><!-- populated by JS --></section>

    <section class="card">
      <h2 style="margin-top:0">Mindmap (At-a-glance)</h2>
      <div class="mermaid">
      mindmap
        root((Seer Pathway))
          Sequence 9: Seer
            Divination
            Spirit Vision
            Ritual Basics
            Support/Utility
          Sequence 8: Clown
            Acrobatics
            Pain Control
            Emotion Masking
            Trickster Combat
      </div>
      <p class="muted" style="margin:.6rem 0 0">
        Spoiler policy: restricted to Sequences 9 & 8 to match where you’re at in the story.
      </p>
    </section>
  </main>

  <footer>
    Built for GitHub README + Pages. Edit <code>data/klein_sequences.json</code> to extend.
  </footer>

  <script>
  async function loadData() {
    try {
      const res = await fetch('../data/klein_sequences.json');
      const data = await res.json();
      const wrap = document.getElementById('cards');

      data.sequences.sort((a,b)=>a.number-b.number).forEach(seq => {
        const card = document.createElement('section');
        card.className = 'card';

        card.innerHTML = `
          <h2 style="margin:.2rem 0 0">${seq.number} — ${seq.name}</h2>
          <div class="muted" style="margin-bottom:.6rem">${seq.concept}</div>

          <div style="margin-bottom:.5rem"><span class="tag">Abilities</span></div>
          <ul>
            ${seq.abilities.map(a=>`<li><strong>${a.label}</strong> — ${a.desc}</li>`).join('')}
          </ul>

          <div style="margin:.8rem 0 .5rem"><span class="tag">Trade-offs / Risks</span></div>
          <ul>
            ${seq.tradeoffs.map(t=>`<li>${t}</li>`).join('')}
          </ul>
        `;
        wrap.appendChild(card);
      });
    } catch (e) {
      console.error(e);
    }
  }
  loadData();
  </script>
</body>
</html>
