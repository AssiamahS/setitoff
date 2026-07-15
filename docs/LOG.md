# Experiment log — what works / what doesn't

Running record so we can see what moved the needle. Newest first.
Format: date · tried · result · verdict.

## 2026-07-15 · v0.1.0

| Tried | Result | Verdict |
| --- | --- | --- |
| Animated GIFs on cards | APL's Image component renders GIFs as a static frame — confirmed limitation, not worth fighting | ❌ use MP4 in APL Video (looping, muted) instead |
| Research: existing Quizlet/Alexa skills | "Quizlet study flashcards" store skill (B06XYD5C3N) is voice-only, old, and forces awkward "study X" phrasing; SpartahackX (2025) pipes Quizlet sets in via PIN + grades answers with Gemini AI but has no screen support; Amazon's own course builds a quiz skill with APL + DynamoDB leaderboard | ✅ gap confirmed: nobody combines Show visuals + spaced repetition + cert content |
| Research: Duolingo on Alexa | No official Duolingo skill; closest is Glot, a 2017 one-lesson prototype | ✅ "Duolingo for Echo Show" lane is open |
| Reddit/X/Substack searches | Reddit returned a JS page shell (no content), X and Substack returned zero hits | ❌ web + GitHub searches were the only useful sources today |
| Leitner boxes over S3 persistence | Implemented, syntax-checked; not yet observed on device | ⏳ verify after first deploy |
| flagcdn.com flag images in capitals deck | URLs follow w640/{iso}.png pattern | ⏳ verify they render on the Show |

**Blocked on:** Amazon developer account sign-in (same account as the Echo
Show) + `ask configure`. Everything after that is automated.

**Next candidates (from research):**
- AI answer grading: say the answer out loud and have an LLM judge it
  (SpartahackX/QuizMe pattern) instead of self-grading — the single biggest
  UX upgrade toward Duolingo territory
- Quizlet set import (their export gives term/definition text)
- Streaks + daily goal (Duolingo mechanic; Reminders API for study nudges)
- Echo Show 15 widget for the fridge notes board
