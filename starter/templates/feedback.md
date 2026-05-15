---
type: feedback
date: YYYY-MM-DD
driving-judgments:
  - "[[link to judgment node 1]]"
  - "[[link to judgment node 2]]"
methodology-to-update: "[[link to 07_methodology/relevant-file]]"
action-taken: [brief description]
result: [right | wrong | mixed | too-early-to-tell]
status: [draft | processed]
---

# Feedback · [one-line description of the action and outcome]

> File this in `01_drafts/feedback/` to trigger the Feedback Reverse-Update operation.

---

## 1. What action was taken

[Describe specifically what you did. Be concrete: which decision, when, based on what.]

---

## 2. Which judgment drove it

This action was driven by:
- **[[Driving judgment 1]]** — at that time, confidence 🟡 0.65
- **[[Driving judgment 2]]** — at that time, evolution-stage 加速 A

[Briefly explain how the judgment translated to action — what protocol or framework you applied.]

---

## 3. What was the result

[Describe the outcome. Be specific. Avoid "it worked" / "it didn't work" without details.]

[If too-early-to-tell: state what observation would close the loop. Schedule a follow-up.]

---

## 4. What I learned

> This is the most important section. The agent will use this to update methodology.

### The judgment itself

- [Did the judgment hold up? If yes, with what nuance? If no, what was wrong?]
- [Was confidence appropriate, too high, or too low at decision time?]
- [Did any falsifier come close to triggering between action and result?]

### The methodology (procedure / protocol)

- [What in the methodology did NOT account for this situation?]
- [What rule, condition, or step should be added?]
- [Be specific. Vague lessons don't propagate. Named ones do.]

### Generalizable insight

- [What's the underlying principle? What other domains does it apply to?]
- [This is the seed for a possible new methodology file or schema update.]

---

## 5. Specific methodology changes proposed

Concrete edits to suggest to the agent:

1. In `07_methodology/<file>.md`, section §X, change wording from "..." to "..."
2. Add new trigger condition: "..."
3. Add new exception clause: "..."

---

## 6. Judgments to revisit after methodology update

When the methodology is updated, these judgments will get an automatic evidence entry. Pre-flag any that may also need confidence review:

- [[Judgment A]] — may need confidence downgrade after this lesson
- [[Judgment B]] — actually strengthened by this; might warrant confidence upgrade

---

## 7. Next steps

- [ ] Agent updates methodology file
- [ ] Agent reverse-propagates evidence to related judgments
- [ ] User reviews confidence implications
- [ ] Mark this feedback file `status: processed`
- [ ] (Optional) If insight is broader than current domain, propose a new Meta layer judgment node

---

*The whole point of feedback is to make sure the same lesson isn't learned twice. Specific > vague. Named > intuitive.*
