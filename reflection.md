# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

| Input Used | Expected Behavior | Actual Behavior | Console Error / Output |
|---|---|---|---|
| Guess 88, secret is 50 | "Go Lower" hint | "Go HIGHER" shown | none |
| Click "New Game" button | Fresh game starts | Nothing happens, must refresh browser | none |
| Uncheck "Show Hint" box | Hint disappears | Hint stays on screen, persists after refresh | none |
| Change difficulty to Easy | Range changes to 1-20, 6 attempts | Range stays 1-100, settings ignored | none |
| Mid-game score in debug panel | Score shows 0 or positive | Score shows -5 (negative) | none |
---

## 2. How did you use AI as a teammate?

I used Claude (Claude Code) to investigate the broken game with me. Before changing anything, I had it walk through `app.py` and `logic_utils.py` and show me each bug as the exact current code next to a suggested fix, so I could understand *why* each line was wrong instead of just accepting a rewrite.

**A correct suggestion:** The AI pointed out that the "secret number keeps changing" feeling came from two places — the secret was only generated once and never refreshed when I switched difficulty, and on every even attempt the code did `secret = str(st.session_state.secret)`, which turned the secret into a string so `guess == secret` (int vs. str) could never be true. It suggested deleting the `str()` line and regenerating the secret whenever the difficulty changes. I verified this by opening the Developer Debug Info panel and confirming the secret now stays put across submits and lands inside the correct range after I change difficulty.

**A suggestion I had to modify:** The AI's first draft of `logic_utils.py` had `check_guess` return a tuple `(outcome, message)` like the original code did. That broke `tests/test_game_logic.py`, which asserts `check_guess(50, 50) == "Win"` — a plain string. I had it change `check_guess` to return only the outcome string and move the hint text into a separate `hint_for()` helper. I caught the mismatch by reading the test file's assertions before running anything, and confirmed the fix with `pytest`.

---

## 3. Debugging and testing your fixes

I decided a bug was really fixed only when I could reproduce the original broken behavior, apply the change, and see the correct behavior in the same scenario — not just when the code "looked right." For the hint bug, I tested with a known secret of 50 (visible in the debug panel): guessing 88 now correctly shows "Go LOWER" and guessing 12 shows "Go HIGHER", which were reversed before. I ran `python -m pytest tests/ -q` and all three tests in `test_game_logic.py` passed, which confirmed `check_guess` returns the right outcome string for win, too-high, and too-low cases. I also manually checked the state bugs: "New Game" now actually restarts after a loss (before, the game stayed in the "lost" state and `st.stop()` blocked it), and an invalid input like "abc" no longer burns an attempt. AI helped me understand the tests by explaining that the assertions expected a single string return value, which is what told me the tuple-returning version would fail before I even ran it.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
