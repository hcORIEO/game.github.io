<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Catch! — Simple Editable Game</title>
  <style>
    /*
    ==========================================
    CATCH! — A super simple editable canvas game
    ==========================================
    HOW TO HOST ON GITHUB PAGES
    1) Name this file index.html and put it at the root of your repo.
    2) Commit & push to GitHub.
    3) In your repo settings → Pages → Set source to "main" (or default) branch, /root.
    4) Wait a minute then open https://<your-username>.github.io/<repo-name>/

    HOW TO EDIT THE GAME QUICKLY
    • Change colors, speeds, sizes in the CONFIG section (below in <script>). 
    • Everything is vanilla HTML/CSS/JS in one file.
    • No build step, no libraries.

    OPTIONAL: README.md is for your project notes/instructions — not required for the game to run.
    */

    :root {
      /* UI color variables — tweak freely */
      --bg: #0f1226;
      --panel: #171a39;
      --accent: #8be9fd;
      --accent-2: #50fa7b;
      --text: #eaeaf2;
      --muted: #9aa0b0;
    }

    html, body {
      height: 100%;
      margin: 0;
    }

    body {
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Ubuntu, Cantarell, Noto Sans, Arial, "Apple Color Emoji", "Segoe UI Emoji";
      background: radial-gradient(1200px 800px at 20% -10%, #1b1f47 0%, var(--bg) 60%);
      color: var(--text);
      display: grid;
      grid-template-rows: auto 1fr auto;
      place-items: center;
      gap: 10px;
      padding: 12px;
    }

    header {
      width: min(880px, 100%);
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
    }

    .title {
      display: flex;
      align-items: baseline;
      gap: 10px;
    }

    h1 {
      margin: 0;
      font-size: clamp(20px, 3.2vw, 32px);
      letter-spacing: 0.5px;
    }

    .subtitle { color: var(--muted); font-size: 0.95rem; }

    .controls {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    button, .pill {
      background: var(--panel);
      border: 1px solid #2d325f;
      color: var(--text);
      border-radius: 999px;
      padding: 8px 12px;
      cursor: pointer;
      font-weight: 600;
      transition: transform 0.04s ease, background 0.2s ease, border 0.2s ease;
    }
    button:hover { transform: translateY(-1px); }
    button:active { transform: translateY(0); }

    .wrap {
      width: min(880px, 100%);
      background: linear-gradient(180deg, rgba(255,255,255,0.04), rgba(255,255,255,0));
      border: 1px solid #2d325f;
      border-radius: 16px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.25);
      overflow: hidden;
      position: relative;
    }

    #game {
      display: block;
      width: 100%;
      height: auto;
      background: radial-gradient(800px 500px at 50% -20%, #1a1f4f 0%, #0c0f25 60%);
    }

    .hud {
      position: absolute;
      left: 0; right: 0; top: 0;
      display: flex;
      justify-content: space-between;
      padding: 10px 14px;
      pointer-events: none;
      font-weight: 700;
      text-shadow: 0 2px 6px rgba(0,0,0,0.45);
    }

    .badge { background: rgba(0,0,0,0.35); padding: 6px 10px; border-radius: 999px; border: 1px solid rgba(255,255,255,0.1); }

    .mobile-controls {
      display: none;
      gap: 10px;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      bottom: 10px;
    }

    .touch-btn {
      width: 64px; height: 64px; border-radius: 50%;
      display
