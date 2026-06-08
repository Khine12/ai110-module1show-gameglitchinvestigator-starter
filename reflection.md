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

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
