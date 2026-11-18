<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#ffe6ee">
  <title>A Love Letter for KENNY</title>
  <style>
    :root {
      --pink: #ffe6ee;
      --rose: #f5a8bd;
      --deep: #b8325b;
      --ink: #713247;
      --paper: #fffaf7;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      min-height: 100vh;
      overflow-x: hidden;
      display: grid;
      place-items: center;
      padding: 28px 16px;
      color: var(--ink);
      font-family: Georgia, "Times New Roman", serif;
      background:
        radial-gradient(circle at 15% 20%, #fff 0 2px, transparent 3px),
        radial-gradient(circle at 85% 75%, #fff 0 2px, transparent 3px),
        linear-gradient(135deg, #fff2f5, var(--pink) 55%, #ffd3df);
    }

    .scene {
      width: min(100%, 560px);
      text-align: center;
      position: relative;
      z-index: 1;
    }

    .eyebrow {
      margin: 0 0 10px;
      color: var(--deep);
      font: 700 0.78rem/1.4 Arial, sans-serif;
      letter-spacing: 0.22em;
      text-transform: uppercase;
    }

    h1 {
      margin: 0 0 12px;
      font-size: clamp(2rem, 8vw, 3.2rem);
      font-weight: 500;
      color: #9f3155;
    }

    .intro {
      margin: 0 auto 34px;
      max-width: 360px;
      font: 1rem/1.6 Arial, sans-serif;
      color: #885368;
    }

    .envelope-button {
      appearance: none;
      border: 0;
      background: transparent;
      padding: 12px;
      cursor: pointer;
      width: min(100%, 390px);
      -webkit-tap-highlight-color: transparent;
    }

    .envelope-button:focus-visible {
      outline: 3px solid var(--deep);
      outline-offset: 8px;
      border-radius: 18px;
    }

    .envelope {
      position: relative;
      height: 230px;
      width: 100%;
      margin: auto;
      filter: drop-shadow(0 18px 20px rgba(137, 48, 79, .18));
      perspective: 900px;
    }

    .envelope-back {
      position: absolute;
      inset: 0;
      border-radius: 12px;
      background: #e98eaa;
    }

    .letter-preview {
      position: absolute;
      left: 8%;
      right: 8%;
      bottom: 10px;
      height: 88%;
      padding: 22px 14px;
      border-radius: 8px;
      background: var(--paper);
      color: #9f3155;
      font-size: 1.15rem;
      transition: transform .8s ease, bottom .8s ease;
      box-shadow: 0 2px 8px rgba(80, 20, 40, .1);
    }

    .envelope-front {
      position: absolute;
      inset: 0;
      overflow: hidden;
      border-radius: 12px;
      background: #f6b1c5;
      clip-path: polygon(0 0, 50% 57%, 100% 0, 100% 100%, 0 100%);
    }

    .envelope-front::before,
    .envelope-front::after {
      content: "";
      position: absolute;
      inset: 0;
      background: #ed9db5;
    }

    .envelope-front::before {
      clip-path: polygon(0 0, 50% 57%, 0 100%);
    }

    .envelope-front::after {
      background: #f2a8bd;
      clip-path: polygon(100% 0, 50% 57%, 100% 100%);
    }

    .flap {
      position: absolute;
      inset: 0;
      z-index: 3;
      background: #f8c1d0;
      clip-path: polygon(0 0, 100% 0, 50% 62%);
      transform-origin: top center;
      transition: transform .75s ease;
      backface-visibility: hidden;
    }

    .seal {
      position: absolute;
      z-index: 4;
      left: 50%;
      top: 53%;
      transform: translate(-50%, -50%);
      width: 48px;
      height: 48px;
      display: grid;
      place-items: center;
      border-radius: 50%;
      color: white;
      background: #c83f69;
      font-size: 1.45rem;
      box-shadow: 0 4px 12px rgba(120, 25, 60, .2);
      transition: opacity .3s ease;
    }

    .envelope-button.opened .flap {
      transform: rotateX(180deg);
      z-index: 0;
    }

    .envelope-button.opened .letter-preview {
      transform: translateY(-105px);
      bottom: 0;
    }

    .envelope-button.opened .seal { opacity: 0; }

    .tap-hint {
      margin: 12px 0 0;
      font: 700 .9rem Arial, sans-serif;
      color: #a64a68;
    }

    .letter {
      display: none;
      margin: 30px auto 0;
      padding: clamp(24px, 6vw, 38px);
      max-width: 500px;
      text-align: left;
      border: 1px solid #f3d3dc;
      border-radius: 16px;
      background: var(--paper);
      box-shadow: 0 14px 35px rgba(137, 48, 79, .12);
      animation: appear .7s ease both;
    }

    .letter.visible { display: block; }

    .letter h2 {
      margin: 0 0 18px;
      text-align: center;
      color: #a83259;
      font-size: 1.8rem;
      font-weight: 500;
    }

    .letter p {
      white-space: pre-line;
      font-size: 1.08rem;
      line-height: 1.85;
      margin: 0 0 16px;
    }

    .signature {
      margin-top: 24px !important;
      text-align: right;
      color: #a83259;
      font-style: italic;
    }

    .heart {
      position: fixed;
      bottom: -30px;
      color: #e45c85;
      pointer-events: none;
      z-index: 0;
      animation: floatUp linear forwards;
      opacity: .75;
    }

    @keyframes floatUp {
      to { transform: translateY(-110vh) rotate(25deg); opacity: 0; }
    }

    @keyframes appear {
      from { opacity: 0; transform: translateY(18px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @media (max-width: 420px) {
      .envelope { height: 195px; }
      .letter-preview { font-size: 1rem; }
    }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: .01ms !important;
        transition-duration: .01ms !important;
      }
    }
  </style>
</head>
<body>
  <main class="scene">
    <p class="eyebrow">A little something from the heart</p>
    <h1>For KENNY</h1>
    <p class="intro">There is a message waiting inside this envelope. Tap to open it. 💗</p>

    <button class="envelope-button" id="envelopeButton"
      type="button" aria-expanded="false" aria-controls="loveLetter">
      <div class="envelope" aria-hidden="true">
        <div class="envelope-back"></div>
        <div class="letter-preview">A letter, written with love…</div>
        <div class="envelope-front"></div>
        <div class="flap"></div>
        <div class="seal">♥</div>
      </div>
      <div class="tap-hint" id="tapHint">Tap the envelope to open ❤️</div>
    </button>

    <article class="letter" id="loveLetter" aria-live="polite">
      <h2>My Dearest KENNY,</h2>
      <p id="letterMessage">Your personal love letter will go here.

For now, this is just a placeholder. MY DEAREST KENNY ❤️

My Sweetheart,

Three years… and yet, whenever I think about you, my heart still feels the same beautiful excitement I felt when our journey began.

KENNY, I want you to know that having you in my life is one of the most beautiful blessings I could ever ask for. These three years have given me beautiful memories, laughter, lessons, unforgettable moments, and reasons to love you even more.

I know we haven't always had perfect days. We've had our ups and downs, misunderstandings, and moments when things weren't easy. But through it all, one thing remains true: YOU ARE STILL THE WOMAN MY HEART CHOOSES.

I don't just love you because of your beauty. I love your presence, your personality, your smile, and the special way you make my world feel different.

If I had the opportunity to go back in time and choose someone to begin this journey with, I would still choose you, KENNY. Not once, not twice, but over and over again.

I may not have everything figured out, and I may not be able to give you the whole world today, but I promise to keep giving you something genuine: my love, my honesty, my care, and my effort.

Three years have passed, but I don't want our love story to end here. I want more memories, more laughter, more adventures, more anniversaries, and countless beautiful chapters with you.

Thank you for being my girl, my happiness, and my special person.

I LOVE YOU, KENNY. ❤️

Forever yours,

THE ONE WHO STILL CHOOSE ME. 💍❤️.</p>
      <p class="signature" id="letterSignature">With love, ❤️</p>
    </article>
  </main>

  <script>
    const envelopeButton = document.getElementById("envelopeButton");
    const loveLetter = document.getElementById("loveLetter");
    const tapHint = document.getElementById("tapHint");

    envelopeButton.addEventListener("click", () => {
      const isOpen = envelopeButton.classList.toggle("opened");
      envelopeButton.setAttribute("aria-expanded", String(isOpen));
      loveLetter.classList.toggle("visible", isOpen);
      tapHint.textContent = isOpen
        ? "Your letter is open 💕"
        : "Tap the envelope to open ❤️";

      if (isOpen) {
        setTimeout(() => loveLetter.scrollIntoView({
          behavior: "smooth", block: "nearest"
        }), 350);
      }
    });

    function makeHeart() {
      const heart = document.createElement("span");
      heart.className = "heart";
      heart.textContent = Math.random() > 0.5 ? "♥" : "♡";
      heart.style.left = Math.random() * 100 + "vw";
      heart.style.fontSize = (14 + Math.random() * 22) + "px";
      heart.style.animationDuration = (5 + Math.random() * 5) + "s";
      document.body.appendChild(heart);
      heart.addEventListener("animationend", () => heart.remove());
    }

    if (!window.matchMedia("(prefers-reduced-motion: reduce)").matches) {
      setInterval(makeHeart, 650);
    }
  </script>
</body>
</html>
