<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Confetti & Cake: Birthday Card Genie</title>

  <!-- Fun fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Montserrat:wght@300;600&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg1: #FBF7FF;
      --accent: #6E3BB8;     /* primary purple */
      --accent2: #B890FF;    /* lighter purple */
      --card-bg: #FCF9FF;
      --shadow: rgba(60,20,80,0.10);
      --muted: #5B3B66;
      --copy: #5A3BD6;
      --highlight: rgba(184,134,255,0.12);
    }

    html,body{
      height:100%;
      margin:0;
      font-family: "Montserrat", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background: linear-gradient(135deg, #fbf8ff 0%, #f6f2ff 40%, #f1eeff 100%);
      color:#1b2030;
    }

    /* Fancier header / title */
    header{
      text-align:center;
      padding:24px 12px 18px;
      background: linear-gradient(90deg, rgba(110,59,184,0.04), rgba(184,134,255,0.02));
      border-bottom: 1px solid rgba(60,20,80,0.03);
      position: relative;
      overflow: visible;
    }

    h1.fancyTitle{
      margin:6px 0 6px;
      font-family: "Playfair Display", "Pacifico", serif;
      font-weight:700;
      font-size:40px;
      line-height:1;
      letter-spacing:-0.5px;
      background: linear-gradient(90deg,var(--accent),var(--accent2),#e7d4ff);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      text-shadow: 0 6px 18px rgba(110,59,184,0.04);
    }

    p.subtitle{
      margin:0;
      margin-top:6px;
      font-family: "Montserrat", system-ui, sans-serif;
      color:var(--muted);
      font-size:15px;
      letter-spacing:0.2px;
    }

    .flourish{
      width:120px;
      height:6px;
      background: linear-gradient(90deg, var(--accent2), var(--accent));
      margin:12px auto 0;
      border-radius:6px;
      box-shadow: 0 6px 18px rgba(110,59,184,0.06);
    }

    .container{
      display:flex;
      gap:20px;
      max-width:1100px;
      margin:28px auto;
      padding:0 18px;
    }

    .controls{
      flex:0 0 360px;
      background: linear-gradient(180deg, rgba(255,255,255,0.96), rgba(250,245,255,0.94));
      border-radius:12px;
      padding:18px;
      box-shadow: 0 8px 24px var(--shadow);
      border: 1px solid rgba(60,20,80,0.04);
    }
    .controls h2{
      margin:0 0 12px;
      color:#2d1b3a;
      font-size:20px;
      font-family: "Pacifico", cursive;
    }
    .controls label{
      display:block;
      margin-top:10px;
      font-size:13px;
      color:#3a2a45;
    }
    .controls input[type="text"],
    .controls input[type="number"]{
      width:100%;
      padding:10px 12px;
      margin-top:6px;
      border-radius:8px;
      border:1px solid rgba(60,20,80,0.06);
      background: #fff;
      font-size:15px;
      box-sizing:border-box;
      transition: background-color 220ms ease, box-shadow 220ms ease;
    }
    .controls input.highlight {
      background: var(--highlight);
      box-shadow: 0 6px 18px rgba(80,40,140,0.06) inset;
    }

    .controls .row{
      display:flex;
      gap:8px;
    }
    .controls .hint{
      font-size:12px;
      color:#6b5576;
      margin-top:6px;
    }
    .controls button{
      margin-top:14px;
      background: linear-gradient(90deg, var(--accent), var(--accent2));
      border:none;
      color:white;
      padding:10px 14px;
      font-size:15px;
      border-radius:10px;
      cursor:pointer;
      box-shadow: 0 6px 18px rgba(110,59,184,0.14);
    }
    .controls button.secondary{
      background:#f6f2ff;color:#3a203f;border-radius:10px;padding:10px 12px;border:1px solid rgba(60,20,80,0.04);box-shadow:none;margin-left:8px;
    }
    .controls button.lucky{
      background: linear-gradient(90deg,#b890ff,#9b63ff);
      color: #2a0b3a;
      font-weight:600;
      margin-left:8px;
      padding:10px 12px;
      border-radius:10px;
      box-shadow: 0 6px 18px rgba(140,90,255,0.10);
    }

    .cards-wrapper{
      flex:1;
      display:flex;
      flex-direction:column;
      align-items:flex-end;
      gap:12px;
      min-height:200px;
    }

    .card{
      width:420px;
      background: linear-gradient(180deg, #fcf9ff, #f5f0ff);
      border-radius:12px;
      padding:18px;
      box-shadow: 0 12px 34px rgba(60,20,80,0.06);
      border: 1px solid rgba(60,20,80,0.05);
      position:relative;
      overflow:visible;
      transform-origin: top right;
      animation: pop 280ms ease;
    }

    .card::before{
      content:"";
      position:absolute;
      left:16px;
      right:16px;
      top:-8px;
      height:8px;
      border-radius:6px;
      background: linear-gradient(90deg, var(--accent2), var(--accent));
      box-shadow: 0 4px 8px rgba(110,59,184,0.06);
    }

    .card .greeting{
      display:flex;
      align-items:center;
      gap:10px;
    }
    .card h3{
      margin:0;
      font-family: "Pacifico", cursive;
      color: var(--accent);
      font-size:22px;
    }
    .card .ageTag{
      margin-left:auto;
      background: linear-gradient(180deg, #fff, #e8ddff);
      color:#3a1f57;
      font-weight:600;
      padding:6px 8px;
      border-radius:8px;
      border:1px solid rgba(60,20,80,0.04);
      font-size:13px;
      box-shadow: 0 4px 12px rgba(60,20,80,0.04);
    }

    .card .message{
      margin-top:10px;
      font-size:15px;
      color:#2b2b44;
      line-height:1.38;
    }

    .card .funny{
      margin-top:12px;
      font-style:italic;
      color:#452a66;
      background: linear-gradient(180deg, rgba(245,240,255,0.9), rgba(250,245,255,0.6));
      padding:10px;
      border-radius:8px;
      border:1px dashed rgba(60,20,80,0.03);
      font-weight:600;
    }

    .card .signature{
      margin-top:12px;
      text-align:right;
      color:#6b5576;
      font-size:13px;
    }

    /* copy button inside card */
    .card .copyBtn{
      position:absolute;
      top:12px;
      right:12px;
      background: rgba(255,255,255,0.96);
      border:1px solid rgba(60,20,80,0.06);
      color:var(--copy);
      padding:6px 8px;
      border-radius:8px;
      font-size:13px;
      cursor:pointer;
      box-shadow: 0 6px 14px rgba(90,30,180,0.06);
      transition: transform 120ms ease, background 160ms ease;
    }
    .card .copyBtn:hover{ transform: translateY(-2px); background: #fbf7ff; }
    .card .copyBtn.copied{
      background: linear-gradient(90deg,#e7d4ff,#f0e8ff);
      color:#3a1f57;
      border-color: rgba(60,20,80,0.04);
    }

    .card + .card{
      margin-top:-8px;
      transform: scale(0.995);
      opacity:0.97;
    }

    @keyframes pop {
      from { transform: translateY(-8px) scale(.995); opacity:0;}
      to   { transform: translateY(0) scale(1); opacity:1;}
    }

    @media (max-width:900px){
      .container{ flex-direction:column; align-items:center; padding-bottom:40px; }
      .cards-wrapper{ align-items:center; width:100%; }
      .controls{ width:100%; max-width:520px; }
      .card{ width:92%; max-width:520px; }
    }

    .confetti{
      position:absolute;
      left:10px;
      top:8px;
      pointer-events:none;
      display:flex;
      gap:4px;
      transform:scale(.9);
    }
    .confetti span{
      width:8px;height:8px;border-radius:2px;display:inline-block;
    }
    .conf1{ background:#e7d4ff; transform: rotate(12deg); }
    .conf2{ background:#b890ff; transform: rotate(-10deg); }
    .conf3{ background:#d6befc; transform: rotate(6deg); }
    .conf4{ background:#6e3bb8; transform: rotate(-6deg); }

    .note{
      margin-top:10px;
      font-size:13px;
      color:#6b5576;
    }
  </style>
</head>
<body>
  <header>
    <div style="position:relative; display:inline-block;">
      <div class="confetti" aria-hidden="true">
        <span class="conf1"></span>
        <span class="conf2"></span>
        <span class="conf3"></span>
        <span class="conf4"></span>
      </div>

      <h1 class="fancyTitle">Confetti & Cake</h1>
      <p class="subtitle">Birthday Card Genie — witty wishes made easy 🎂✨</p>
      <div class="flourish" aria-hidden="true"></div>
    </div>
  </header>

  <main class="container" role="main" aria-labelledby="pageTitle">
    <section class="controls" aria-label="Card inputs">
      <h2>Write a card</h2>

      <form id="cardForm">
        <label for="name">Name</label>
        <input id="name" name="name" type="text" placeholder="e.g. Jamie" required>

        <label for="age">Age</label>
        <input id="age" name="age" type="number" min="1" max="150" placeholder="e.g. 30" required>

        <label for="hobby">Hobby</label>
        <input id="hobby" name="hobby" type="text" placeholder="e.g. gardening, chess, gaming" required>

        <label for="adjective">Adjective</label>
        <input id="adjective" name="adjective" type="text" placeholder="e.g. brilliant, wacky, sparkly" required>

        <label for="plural">Plural Noun</label>
        <input id="plural" name="plural" type="text" placeholder="e.g. cookies, balloons, adventures" required>

        <div style="display:flex; gap:8px; flex-wrap:wrap; margin-top:6px;">
          <button type="submit">Make Card 🎈</button>

          <!-- I'm feeling lucky button (type=button so it doesn't submit the form) -->
          <button type="button" id="luckyBtn" class="lucky" title="Auto-fill with funny choices">I'm feeling lucky ✨</button>

          <button type="button" id="clearAll" class="secondary">Clear All</button>
        </div>
        <div class="note">Click "I'm feeling lucky" to auto-fill. After creating cards, use the copy button on each card to copy its text to your clipboard.</div>
      </form>
    </section>

    <section class="cards-wrapper" aria-label="Birthday cards area" id="cardsArea">
      <!-- Cards will be inserted here -->
    </section>
  </main>

  <script>
    // Elements
    const form = document.getElementById('cardForm');
    const cardsArea = document.getElementById('cardsArea');
    const clearBtn = document.getElementById('clearAll');
    const luckyBtn = document.getElementById('luckyBtn');

    // Funny predefined choices
    const luckyChoices = {
      names: [
        "Captain Sparkles", "Noodle", "Poppy", "Gizmo", "Zelda", "Cheddar", "Luna", "Mojo"
      ],
      ages: [
        "7","13","18","21","30","42","69","101"
      ],
      hobbies: [
        "juggling", "space-walking", "yo-yo tricks", "extreme knitting", "taco sculpting",
        "binge gardening", "competitive napping", "guerilla baking"
      ],
      adjectives: [
        "sparkly", "wacky", "glorious", "mystical", "dashing", "slime-tastic", "magnificent", "snoozy"
      ],
      plurals: [
        "balloons", "donuts", "unicorns", "kazoos", "pancakes", "confetti", "socks", "treasures"
      ]
    };

    // Message templates
    const templates = [
      "{name}, you're {adjective} and {age} years young — time to celebrate with extra {plural} and zero regrets about dessert!",
      "Happy {age}th, {name}! May your {hobby} be tireless, your day {adjective}, and your supply of {plural} never run out.",
      "At {age}, you're officially a {adjective} legend in the world of {hobby}. Also, you now qualify for honorary {plural}.",
      "Wishing you a {adjective} birthday, {name}. May your {hobby} bring joy and your {plural} be plentiful!",
      "Congratulations on turning {age}! You're like a fine {hobby}-player: {adjective}, admired, and always ready with more {plural}.",
      "{name}, keep being {adjective} — age {age} looks great on you. Now go celebrate with {plural} and maybe a little {hobby}.",
      "Happy birthday! At {age}, you're not getting older — you're getting more {adjective} and collecting epic {plural}.",
      "Another year, another {adjective} chapter! May your {hobby} sessions be long and your {plural} be legendary."
    ];

    const emojis = ["🎉","🎂","🥳","🍰","🎈","😜","🍩","🪅"];

    function randomChoice(arr){ return arr[Math.floor(Math.random() * arr.length)]; }

    function generateMessage(inputs){
      const t = randomChoice(templates);
      const emoji = randomChoice(emojis);
      return t
        .replace(/{name}/g, inputs.name)
        .replace(/{age}/g, inputs.age)
        .replace(/{hobby}/g, inputs.hobby)
        .replace(/{adjective}/g, inputs.adjective)
        .replace(/{plural}/g, inputs.plural)
        + " " + emoji;
    }

    // Build a card element. We store a plain-text version for copying in dataset.copy
    function buildCard(inputs, message){
      const card = document.createElement('article');
      card.className = 'card';
      card.setAttribute('role','article');

      // Plain text to copy
      const copyText = `Happy Birthday, ${inputs.name} (${inputs.age})

Dear ${inputs.name},

${message}

— With love from your friendly Card Genie`;

      card.dataset.copy = copyText;

      // Rendered card HTML (visible)
      card.innerHTML = `
        <button class="copyBtn" aria-label="Copy card to clipboard">📋 Copy</button>
        <div class="greeting">
          <h3>Happy Birthday, ${escapeHtml(inputs.name)}!</h3>
          <div class="ageTag">${escapeHtml(inputs.age)}</div>
        </div>
        <div class="message">Dear ${escapeHtml(inputs.name)},</div>
        <div class="funny">${escapeHtml(message)}</div>
        <div class="signature">— With love from your friendly Card Genie</div>
      `;
      return card;
    }

    // Basic escaping for safe insertion
    function escapeHtml(str){
      return String(str)
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;')
        .replace(/'/g, '&#039;');
    }

    // Copy helper with fallback for older browsers
    function copyToClipboard(text){
      if (navigator.clipboard && navigator.clipboard.writeText) {
        return navigator.clipboard.writeText(text);
      }
      // fallback: create textarea and execCommand
      return new Promise((resolve, reject) => {
        const ta = document.createElement('textarea');
        ta.value = text;
        ta.style.position = 'fixed';
        ta.style.left = '-9999px';
        document.body.appendChild(ta);
        ta.focus();
        ta.select();
        try {
          const ok = document.execCommand('copy');
          document.body.removeChild(ta);
          if (ok) resolve();
          else reject(new Error('execCommand copy failed'));
        } catch (err) {
          document.body.removeChild(ta);
          reject(err);
        }
      });
    }

    // Form submit -> create card and prepend
    form.addEventListener('submit', function(e){
      e.preventDefault();
      const name = form.name.value.trim();
      const age = form.age.value.trim();
      const hobby = form.hobby.value.trim();
      const adjective = form.adjective.value.trim();
      const plural = form.plural.value.trim();

      if (!name || !age || !hobby || !adjective || !plural) {
        alert('Please fill in all five fields: Name, Age, Hobby, Adjective, and Plural Noun.');
        return;
      }

      const inputs = { name, age, hobby, adjective, plural };
      const msg = generateMessage(inputs);
      const card = buildCard(inputs, msg);

      // Prepend newest at the top
      if (cardsArea.firstChild) cardsArea.insertBefore(card, cardsArea.firstChild);
      else cardsArea.appendChild(card);

      // Smooth scroll to show it
      card.scrollIntoView({ behavior: 'smooth', block: 'start' });

      // Reset and focus name
      form.reset();
      form.name.focus();
    });

    // Clear all
    clearBtn.addEventListener('click', function(){
      if (!cardsArea.hasChildNodes()) return;
      if (!confirm("Clear all created cards? This can't be undone in this session.")) return;
      cardsArea.innerHTML = '';
    });

    // Lucky fill
    luckyBtn.addEventListener('click', function(){
      const chosen = {
        name: randomChoice(luckyChoices.names),
        age: randomChoice(luckyChoices.ages),
        hobby: randomChoice(luckyChoices.hobbies),
        adjective: randomChoice(luckyChoices.adjectives),
        plural: randomChoice(luckyChoices.plurals)
      };

      form.name.value = chosen.name;
      form.age.value = chosen.age;
      form.hobby.value = chosen.hobby;
      form.adjective.value = chosen.adjective;
      form.plural.value = chosen.plural;

      // highlight briefly
      const inputs = [form.name, form.age, form.hobby, form.adjective, form.plural];
      inputs.forEach(i => i.classList.add('highlight'));
      setTimeout(() => inputs.forEach(i => i.classList.remove('highlight')), 900);
    });

    // Event delegation for copy button clicks inside cards area
    cardsArea.addEventListener('click', function(e){
      const btn = e.target.closest('.copyBtn');
      if (!btn) return;

      const card = btn.closest('.card');
      if (!card) return;

      const textToCopy = card.dataset.copy || card.innerText || '';

      // Temporarily change button to indicate progress
      const originalText = btn.textContent;
      btn.textContent = 'Copying...';
      btn.disabled = true;

      copyToClipboard(textToCopy).then(() => {
        btn.textContent = '✅ Copied!';
        btn.classList.add('copied');
        // restore after a short delay
        setTimeout(() => {
          btn.textContent = originalText;
          btn.classList.remove('copied');
          btn.disabled = false;
        }, 1400);
      }).catch(() => {
        btn.textContent = 'Failed to copy';
        btn.disabled = false;
        setTimeout(() => {
          btn.textContent = originalText;
        }, 1400);
      });
    });

    // Add a friendly sample card on load
    window.addEventListener('load', function(){
      const sampleInputs = { name: "Sam", age: "29", hobby: "biking", adjective: "sparkly", plural: "balloons" };
      const sample = buildCard(sampleInputs, generateMessage(sampleInputs));
      cardsArea.appendChild(sample);
    });
  </script>
</body>
</html>
