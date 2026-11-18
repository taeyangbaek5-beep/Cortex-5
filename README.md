```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#f7f4ed">
  <title>Parts of the Human Brain</title>
  <style>
    :root {
      --bg: #f7f4ed;
      --paper: #fffefa;
      --ink: #222729;
      --muted: #626b6b;
      --green: #3f6659;
      --green-light: #e9f0ed;
      --line: #e2ddd1;
      --shadow: 0 8px 26px rgba(45, 40, 30, 0.08);
      --font-main: 'Calibri', 'Carlito', sans-serif;
    }

    * {
      box-sizing: border-box;
      font-family: var(--font-main);
    }

    body {
      margin: 0;
      background: var(--bg);
      color: var(--ink);
      font-family: var(--font-main);
      -webkit-font-smoothing: antialiased;
    }

    header {
      max-width: 1160px;
      margin: 0 auto;
      padding: 32px 24px 16px;
    }

    .kicker {
      font-size: 0.78rem;
      letter-spacing: 0.16em;
      text-transform: uppercase;
      font-weight: 700;
      color: var(--green);
    }

    h1 {
      font-family: var(--font-main);
      font-size: clamp(2.1rem, 4.5vw, 3rem);
      font-weight: 700;
      letter-spacing: -0.02em;
      margin: 8px 0 10px;
      line-height: 1.12;
    }

    header p {
      color: var(--muted);
      line-height: 1.6;
      max-width: 680px;
      margin: 0;
      font-size: 1.05rem;
    }

    main {
      max-width: 1160px;
      margin: 14px auto 44px;
      padding: 0 24px;
      display: grid;
      grid-template-columns: minmax(0, 1.35fr) minmax(300px, 0.65fr);
      gap: 22px;
      align-items: start;
    }

    .panel {
      background: var(--paper);
      border: 1px solid var(--line);
      border-radius: 14px;
      padding: 22px;
      box-shadow: var(--shadow);
    }

    .panel-header {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 6px;
    }

    .panel h2 {
      font-size: 1.12rem;
      font-weight: 700;
      margin: 0;
    }

    .hint {
      font-size: 0.94rem;
      color: var(--muted);
      margin: 0 0 10px;
    }

    .diagram-wrap {
      background: #ffffff;
      border: 1px solid #ede8dd;
      border-radius: 12px;
      padding: 10px 6px 14px;
      margin-top: 6px;
    }

    svg#brainDiagram {
      width: 100%;
      height: auto;
      display: block;
      user-select: none;
    }

    /* Interactive brain region styling */
    .brain-region {
      cursor: pointer;
      transition: filter 0.2s ease, transform 0.2s ease, opacity 0.2s ease;
    }

    .brain-region:hover {
      filter: brightness(1.06) contrast(1.03);
    }

    .brain-region:focus {
      outline: none;
    }

    .brain-region:focus-visible .lobe-outline,
    .brain-region.active .lobe-outline {
      stroke: #1c2422;
      stroke-width: 3.4;
      filter: drop-shadow(0 0 6px rgba(28, 36, 34, 0.35));
    }

    .brain-region.dimmed {
      opacity: 0.72;
    }

    /* Leader lines & labels matching reference illustration */
    .leader-line {
      stroke: #181a1b;
      stroke-width: 2.1;
      stroke-linecap: round;
      fill: none;
      transition: stroke 0.2s ease, stroke-width 0.2s ease;
    }

    .leader-label {
      font-family: var(--font-main);
      font-size: 17.5px;
      font-weight: 500;
      fill: #181a1b;
      cursor: pointer;
      transition: font-weight 0.15s ease, fill 0.15s ease;
    }

    .leader-label:hover,
    .leader-label.active {
      font-weight: 700;
      fill: var(--green);
    }

    /* Quick select pills */
    .buttons {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-top: 16px;
    }

    .part-btn {
      display: inline-flex;
      align-items: center;
      gap: 7px;
      background: #f5f1e8;
      border: 1px solid #dcd5c7;
      border-radius: 8px;
      padding: 9px 13px;
      font-family: var(--font-main);
      font-size: 0.94rem;
      font-weight: 600;
      color: #2c3331;
      cursor: pointer;
      transition: all 0.16s ease;
    }

    .part-btn:hover {
      background: #ece6d9;
      border-color: #c7beae;
    }

    .part-btn.active {
      background: var(--green);
      color: #ffffff;
      border-color: var(--green);
      box-shadow: 0 3px 10px rgba(63, 102, 89, 0.24);
    }

    .part-btn:focus-visible {
      outline: 2px solid var(--green);
      outline-offset: 2px;
    }

    .swatch {
      width: 11px;
      height: 11px;
      border-radius: 50%;
      border: 1px solid rgba(0, 0, 0, 0.22);
      flex-shrink: 0;
    }

    /* Right side details panel */
    .details {
      display: flex;
      flex-direction: column;
      min-height: 460px;
      position: sticky;
      top: 20px;
    }

    .details .eyebrow {
      color: var(--green);
      font-size: 0.78rem;
      font-weight: 700;
      letter-spacing: 0.14em;
      text-transform: uppercase;
    }

    #partName {
      font-family: var(--font-main);
      font-size: 2.15rem;
      font-weight: 700;
      margin: 10px 0 14px;
      line-height: 1.15;
    }

    .details h3 {
      font-size: 0.85rem;
      letter-spacing: 0.09em;
      text-transform: uppercase;
      color: var(--green);
      margin: 18px 0 6px;
    }

    .details p {
      font-size: 1.02rem;
      line-height: 1.65;
      color: #454f4d;
      margin: 0;
    }

    .note {
      margin-top: auto;
      padding-top: 24px;
      border-top: 1px solid #eee9de;
      font-size: 0.88rem;
      line-height: 1.55;
      color: #7d8681;
    }

    @media (max-width: 860px) {
      main {
        grid-template-columns: 1fr;
        padding: 0 16px;
      }
      .details {
        position: static;
        min-height: auto;
      }
      header {
        padding: 24px 16px 12px;
      }
      .panel {
        padding: 16px;
      }
    }

    @media (max-width: 480px) {
      .leader-label {
        font-size: 15px;
      }
      .part-btn {
        flex: 1 1 calc(50% - 8px);
        justify-content: center;
      }
    }
  </style>
</head>
<body>
  <header>
    <div class="kicker">Interactive Neuroanatomy Guide</div>
    <h1>Parts of the Human Brain</h1>
    <p>Select any sculpted region of the brain or use the buttons below to inspect its anatomical definition and primary functions.</p>
  </header>

  <main>
    <!-- Interactive Brain Illustration Card -->
    <section class="panel" aria-label="Brain Diagram Explorer">
      <div class="panel-header">
        <h2>Explore the brain</h2>
      </div>
      <p class="hint">Click or tap on a colored lobe, the cerebellum, or the spinal cord.</p>

      <div class="diagram-wrap">
        <svg id="brainDiagram" viewBox="0 0 800 500" role="group" aria-label="Sculpted lateral illustration of the human brain">
          <defs>
            <!-- Drop shadow beneath entire brain -->
            <filter id="brainDropShadow" x="-10%" y="-10%" width="125%" height="130%">
              <feDropShadow dx="0" dy="8" stdDeviation="7" flood-color="#1f1a18" flood-opacity="0.16"/>
            </filter>

            <!-- FRONTAL LOBE: Rich Crimson & Glossy Red -->
            <radialGradient id="frontalGrad" cx="35%" cy="32%" r="72%">
              <stop offset="0%" stop-color="#ff6961"/>
              <stop offset="32%" stop-color="#eb2629"/>
              <stop offset="72%" stop-color="#c4121b"/>
              <stop offset="100%" stop-color="#7c070f"/>
            </radialGradient>
            <linearGradient id="frontalPrecentral" x1="0" y1="0" x2="1" y2="0.8">
              <stop offset="0%" stop-color="#ff4d4d"/>
              <stop offset="48%" stop-color="#dc1d22"/>
              <stop offset="100%" stop-color="#8a0911"/>
            </linearGradient>

            <!-- PARIETAL LOBE: Bright Golden Yellow -->
            <radialGradient id="parietalGrad" cx="45%" cy="30%" r="70%">
              <stop offset="0%" stop-color="#fff99e"/>
              <stop offset="35%" stop-color="#ffe135"/>
              <stop offset="75%" stop-color="#f5b800"/>
              <stop offset="100%" stop-color="#b87800"/>
            </radialGradient>

            <!-- OCCIPITAL LOBE: Sky / Ice Blue -->
            <radialGradient id="occipitalGrad" cx="42%" cy="35%" r="70%">
              <stop offset="0%" stop-color="#e3f7ff"/>
              <stop offset="38%" stop-color="#9bd8f5"/>
              <stop offset="78%" stop-color="#5da9d6"/>
              <stop offset="100%" stop-color="#2c668f"/>
            </radialGradient>

            <!-- TEMPORAL LOBE: Vibrant Orchid / Magenta-Purple -->
            <radialGradient id="temporalGrad" cx="42%" cy="35%" r="72%">
              <stop offset="0%" stop-color="#f2b8ed"/>
              <stop offset="38%" stop-color="#c96ec2"/>
              <stop offset="78%" stop-color="#994294"/>
              <stop offset="100%" stop-color="#5b1f59"/>
            </radialGradient>

            <!-- CEREBELLUM: Warm Golden-Brown / Ochre -->
            <radialGradient id="cerebellumGrad" cx="42%" cy="30%" r="72%">
              <stop offset="0%" stop-color="#f5c982"/>
              <stop offset="45%" stop-color="#cc8739"/>
              <stop offset="85%" stop-color="#965619"/>
              <stop offset="100%" stop-color="#5e3109"/>
            </radialGradient>

            <!-- SPINAL CORD / BRAINSTEM: Muted Mauve / Purple-Pink -->
            <linearGradient id="spinalGrad" x1="0" y1="0" x2="1" y2="0.4">
              <stop offset="0%" stop-color="#d89bc8"/>
              <stop offset="45%" stop-color="#a66498"/>
              <stop offset="85%" stop-color="#753d6a"/>
              <stop offset="100%" stop-color="#4d2246"/>
            </linearGradient>

            <!-- Clip paths so internal sulci & specular highlights stay crisp inside each lobe -->
            <clipPath id="clipFrontal">
              <path d="M166 266 C152 246 151 224 162 206 C149 188 153 163 169 149 C166 125 182 99 207 90 C219 67 247 54 274 58 C293 43 324 41 346 53 C368 41 399 42 419 52 C416 69 401 81 393 97 C382 119 384 142 372 162 C360 183 361 206 347 224 C324 233 295 244 268 258 C240 272 213 287 188 282 C176 280 170 274 166 266 Z"/>
            </clipPath>

            <clipPath id="clipParietal">
              <path d="M419 52 C444 48 471 57 487 74 C514 75 538 93 546 117 C567 128 578 153 571 176 C552 179 535 190 526 206 C512 204 498 212 492 224 C472 225 455 215 446 199 C431 190 411 193 398 205 C382 213 363 219 347 224 C361 206 360 183 372 162 C384 142 382 119 393 97 C401 81 416 69 419 52 Z"/>
            </clipPath>

            <clipPath id="clipOccipital">
              <path d="M571 176 C590 185 601 208 594 229 C606 247 604 274 587 289 C588 308 571 324 551 322 C535 327 517 319 509 305 C503 288 506 269 499 253 C491 242 490 232 492 224 C498 212 512 204 526 206 C535 190 552 179 571 176 Z"/>
            </clipPath>

            <clipPath id="clipTemporal">
              <path d="M276 312 C281 286 306 268 332 269 C349 247 375 231 401 221 C416 202 440 198 459 211 C475 215 488 221 495 234 C505 251 504 274 509 294 C512 311 499 327 482 329 C463 343 437 346 416 336 C395 352 365 356 341 344 C317 355 288 345 278 322 C276 319 275 315 276 312 Z"/>
            </clipPath>

            <clipPath id="clipCerebellum">
              <path d="M412 342 C433 324 467 317 498 323 C528 328 552 345 552 369 C552 395 524 419 485 424 C448 429 415 415 404 391 C397 374 400 354 412 342 Z"/>
            </clipPath>

            <clipPath id="clipSpinal">
              <path d="M359 346 C377 351 395 350 407 344 C401 364 401 384 411 401 C422 414 435 422 445 438 L421 444 C411 427 397 413 383 398 C370 383 360 366 359 346 Z"/>
            </clipPath>
          </defs>

          <!-- Main Sculpted Brain Group -->
          <g filter="url(#brainDropShadow)">

            <!-- ==================== 1. SPINAL CORD / BRAINSTEM ==================== -->
            <g class="brain-region" data-part="spinal" tabindex="0" role="button" aria-label="Spinal cord">
              <path class="lobe-outline" fill="url(#spinalGrad)" stroke="#3d1936" stroke-width="2" stroke-linejoin="round"
                d="M359 346 C377 351 395 350 407 344 C401 364 401 384 411 401 C422 414 435 422 445 438 L421 444 C411 427 397 413 383 398 C370 383 360 366 359 346 Z"/>
              <g clip-path="url(#clipSpinal)" pointer-events="none">
                <!-- Deep striated nerve fibers & vertical ridges -->
                <path d="M369 349 C375 375 394 405 425 443" fill="none" stroke="#421a3b" stroke-width="2.4"/>
                <path d="M378 350 C385 376 403 406 431 441" fill="none" stroke="#421a3b" stroke-width="2.2"/>
                <path d="M388 349 C394 375 412 405 437 440" fill="none" stroke="#421a3b" stroke-width="2.2"/>
                <path d="M397 347 C402 373 419 403 442 438" fill="none" stroke="#421a3b" stroke-width="2"/>
                <!-- Glossy specular ridge highlights -->
                <path d="M373 351 C380 376 398 405 427 441" fill="none" stroke="#f0c7e6" stroke-width="1.8" stroke-linecap="round" opacity="0.85"/>
                <path d="M383 351 C390 376 407 405 433 440" fill="none" stroke="#f0c7e6" stroke-width="1.6" stroke-linecap="round" opacity="0.75"/>
                <!-- Shadow under temporal lobe -->
                <path d="M356 347 C376 355 396 354 410 347" fill="none" stroke="#2d1028" stroke-width="6" opacity="0.65"/>
              </g>
            </g>

            <!-- ==================== 2. CEREBELLUM ==================== -->
            <g class="brain-region" data-part="cerebellum" tabindex="0" role="button" aria-label="Cerebellum">
              <path class="lobe-outline" fill="url(#cerebellumGrad)" stroke="#4f2706" stroke-width="2.2" stroke-linejoin="round"
                d="M412 342 C433 324 467 317 498 323 C528 328 552 345 552 369 C552 395 524 419 485 424 C448 429 415 415 404 391 C397 374 400 354 412 342 Z"/>
              <g clip-path="url(#clipCerebellum)" pointer-events="none">
                <!-- Deep folia grooves (dark brown curved striations) -->
                <g fill="none" stroke="#592c08" stroke-width="2.2" stroke-linecap="round" opacity="0.85">
                  <path d="M406 346 C446 327 502 326 546 347"/>
                  <path d="M401 355 C445 335 505 335 552 357"/>
                  <path d="M399 364 C445 344 507 345 554 367"/>
                  <path d="M399 374 C446 354 507 355 553 377"/>
                  <path d="M401 384 C447 365 505 366 549 387"/>
                  <path d="M406 394 C449 376 502 377 542 397"/>
                  <path d="M414 404 C453 388 498 389 532 406"/>
                  <path d="M426 413 C459 400 493 401 519 415"/>
                </g>
                <!-- Bright cream/ochre folia ridge highlights -->
                <g fill="none" stroke="#ffe5b4" stroke-width="1.9" stroke-linecap="round" opacity="0.85">
                  <path d="M409 343 C447 324 501 323 543 344"/>
                  <path d="M404 352 C446 332 504 332 549 354"/>
                  <path d="M402 361 C446 341 506 342 551 364"/>
                  <path d="M402 371 C447 351 506 352 550 374"/>
                  <path d="M404 381 C448 362 504 363 546 384"/>
                  <path d="M409 391 C450 373 501 374 539 394"/>
                  <path d="M417 401 C454 385 497 386 529 403"/>
                </g>
                <!-- Top shadow cast by occipital & temporal lobes -->
                <path d="M405 339 C445 322 505 321 548 340" fill="none" stroke="#361802" stroke-width="7" opacity="0.5"/>
              </g>
            </g>

            <!-- ==================== 3. OCCIPITAL LOBE ==================== -->
            <g class="brain-region" data-part="occipital" tabindex="0" role="button" aria-label="Occipital lobe">
              <path class="lobe-outline" fill="url(#occipitalGrad)" stroke="#1d4666" stroke-width="2.2" stroke-linejoin="round"
                d="M571 176 C590 185 601 208 594 229 C606 247 604 274 587 289 C588 308 571 324 551 322 C535 327 517 319 509 305 C503 288 506 269 499 253 C491 242 490 232 492 224 C498 212 512 204 526 206 C535 190 552 179 571 176 Z"/>
              <g clip-path="url(#clipOccipital)" pointer-events="none">
                <!-- Deep navy/slate sulci crevices -->
                <g fill="none" stroke="#183b57" stroke-width="4.2" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M532 203 C545 215 542 234 527 244 C514 252 516 268 531 273"/>
                  <path d="M565 184 C558 202 567 219 586 225"/>
                  <path d="M551 228 C568 232 576 248 566 263 C556 277 567 294 584 292"/>
                  <path d="M514 278 C531 281 544 295 541 314"/>
                  <path d="M552 296 C558 306 555 316 547 322"/>
                </g>
                <!-- Soft secondary sulci shadows -->
                <g fill="none" stroke="#2d6691" stroke-width="7" stroke-linecap="round" opacity="0.45">
                  <path d="M532 205 C545 217 542 236 527 246"/>
                  <path d="M551 230 C568 234 576 250 566 265"/>
                </g>
                <!-- Glossy ice-white highlights on gyri -->
                <g fill="none" stroke="#ffffff" stroke-width="3.6" stroke-linecap="round" opacity="0.88">
                  <path d="M549 191 C561 187 574 192 579 203"/>
                  <path d="M518 221 C526 214 535 218 534 228"/>
                  <path d="M573 237 C584 239 591 251 587 263"/>
                  <path d="M534 257 C546 252 557 259 554 271"/>
                  <path d="M517 292 C525 289 533 296 531 305"/>
                  <path d="M563 301 C572 301 577 308 572 315"/>
                </g>
              </g>
            </g>

            <!-- ==================== 4. PARIETAL LOBE ==================== -->
            <g class="brain-region" data-part="parietal" tabindex="0" role="button" aria-label="Parietal lobe">
              <path class="lobe-outline" fill="url(#parietalGrad)" stroke="#7a4c00" stroke-width="2.2" stroke-linejoin="round"
                d="M419 52 C444 48 471 57 487 74 C514 75 538 93 546 117 C567 128 578 153 571 176 C552 179 535 190 526 206 C512 204 498 212 492 224 C472 225 455 215 446 199 C431 190 411 193 398 205 C382 213 363 219 347 224 C361 206 360 183 372 162 C384 142 382 119 393 97 C401 81 416 69 419 52 Z"/>
              <g clip-path="url(#clipParietal)" pointer-events="none">
                <!-- Deep amber/brown sulci crevices -->
                <g fill="none" stroke="#7d4a00" stroke-width="4.5" stroke-linecap="round" stroke-linejoin="round">
                  <!-- Postcentral sulcus running parallel to central sulcus -->
                  <path d="M443 56 C436 82 419 101 415 128 C411 154 394 174 388 202"/>
                  <!-- Intraparietal & upper folds -->
                  <path d="M484 74 C474 96 485 118 507 123 C526 127 535 145 524 162"/>
                  <path d="M436 122 C456 121 471 136 465 156 C459 175 474 191 494 187"/>
                  <path d="M542 121 C534 138 543 156 561 161"/>
                  <path d="M414 168 C432 166 446 179 445 196"/>
                  <path d="M498 158 C514 164 522 182 514 199"/>
                </g>
                <!-- Warm golden shading beside sulci -->
                <g fill="none" stroke="#c97d00" stroke-width="8" stroke-linecap="round" opacity="0.38">
                  <path d="M445 58 C438 84 421 103 417 130 C413 156 396 176 390 204"/>
                  <path d="M486 76 C476 98 487 120 509 125"/>
                  <path d="M438 124 C458 123 473 138 467 158"/>
                </g>
                <!-- Creamy white specular highlights along puffy yellow gyri -->
                <g fill="none" stroke="#fffff2" stroke-width="4.6" stroke-linecap="round" opacity="0.92">
                  <!-- Postcentral gyrus ridge highlight -->
                  <path d="M423 64 C415 84 402 99 398 121"/>
                  <path d="M393 138 C389 159 376 177 371 198"/>
                  <!-- Superior & inferior parietal gyri highlights -->
                  <path d="M454 63 C4
