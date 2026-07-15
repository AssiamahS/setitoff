# Flash Deck — Echo Show flashcards

Quizlet-style voice flashcards for Echo Show (11/15). Alexa custom skill with:

- **Visual cards** (APL): big text + picture on the front, tap or say "flip" to reveal
- **Self-graded spaced repetition**: "got it" / "missed it" — missed cards get box 1
  (Leitner) and come up first next session; progress saved to S3 between sessions
- **Voice notes**: "note buy milk" → saved as a card in the **My Notes** deck
  (your mini post-it board), shown full-screen when created
- **Decks are plain JSON** in `lambda/decks/` — add a file, redeploy, done

## Voice commands

| Say | Does |
| --- | --- |
| "Alexa, open flash deck" | menu of decks |
| "study world capitals" | starts a deck (or tap it on screen) |
| "flip" (or tap card) | reveal answer |
| "got it" / "missed it" | grade + advance (missed = repeats sooner) |
| "next" | skip without grading |
| "note pick up eggs" | saves a note card to My Notes |
| "study my notes" | review your notes as flashcards |

## One-time setup (only you can do these)

1. **Amazon Developer account** — go to https://developer.amazon.com and sign in
   **with the SAME Amazon account your Echo Show is registered to** (check in the
   Alexa app → Settings). Same account = dev skills appear on your device
   automatically, no publishing needed. Free.
2. **Authorize the CLI** — in Claude Code type:
   `! ask configure`
   (browser opens, log in, done once).

Then tell Claude "configured" and it will create the Alexa-hosted skill (free —
Amazon hosts the Lambda + S3, no AWS account needed) and push this code into it.

## Deck format

```json
{
  "id": "capitals",
  "name": "World Capitals",
  "cards": [
    { "front": "France", "back": "Paris", "image": "https://flagcdn.com/w640/fr.png" },
    { "front": "Cell", "back": "Basic unit of life", "video": "https://.../clip.mp4" }
  ]
}
```

- `image`: any public HTTPS JPG/PNG URL
- `video`: public HTTPS MP4 — plays looping + muted on the card (use MP4 for
  animation; animated GIFs render as a static frame in APL's Image component)

## Layout

```
skill-package/
  skill.json                          # manifest (APL enabled)
  interactionModels/custom/en-US.json # invocation "flash deck" + intents
lambda/
  index.js                            # all skill logic
  apl/card.json, apl/menu.json        # Echo Show screens
  decks/*.json                        # your decks
```

## Roadmap ideas

- Echo Show 15 widget (persistent fridge notes board)
- Quizlet TSV import script (Quizlet → export set → paste TSV → deck JSON)
- AI-generated decks ("make me 20 cards on the amendments")
- Reminders API ("remind me" from inside the skill; native "Alexa, add a sticky
  note" and "Alexa, remind me..." already work on the Show today)
