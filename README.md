# Grandmaster Insanity

A chess bot in a single web page (`index.html`), with a board styled after chess.com's green theme.

- **Engine:** Stockfish 18 (lite NNUE, WebAssembly) in a Web Worker, files in `engine/`.
- **Opponent model:** learns which kinds of moves you choose (captures, checks, development, risk, engine-like moves…) and seals a prediction of your next move before you play it.
- **Pondering:** keeps searching on the predicted move while you think, so a correct prediction gives it extra search time.
- **Practical move choice:** when Stockfish rates several moves within a few centipawns, it plays the one whose likely replies (per your model) lose the most. When losing, it widens that window to look for swindles.
- **Opening book:** 38 grandmaster main lines (Ruy Lopez, Najdorf, Sveshnikov, Nimzo-Indian, Grünfeld, Catalan…).
- **Backup engine:** a built-in alpha-beta search (perft-verified move generator) if Stockfish can't load.

Run it from any static server (Workers don't load from `file://`):

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000.

Credits: Stockfish (GPL-3.0, see `engine/COPYING-stockfish.txt`), cburnett pieces via lichess chessground (GPL-3.0).
