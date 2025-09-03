Perfect, this is shaping into a fantastic first lesson. I’ll organize your list into a clear **teaching flow** so that the session feels like a journey: start light and fun, slowly build conceptual depth, and end with a big-picture takeaway. Each activity is expanded so you know exactly what to do, what prompts to run, and what the students will discover.

---

# Lesson 1: Prompt Engineering (Expanded Flow)

---

## 1. Icebreaker: The Cookie Recipe Game

**Goal:** Show that tiny changes in wording lead to big changes in output.
**How to run:**

* Start with a basic prompt: *“Give me a recipe for cookies.”*
* Then tweak step by step:

  * *“…with chocolate.”*
  * *“…with chocolate, but gluten-free.”*
  * *“…in the style of a medieval knight’s instructions.”*
* Keep escalating the weirdness. Students suggest constraints live, you type them in, and everyone sees how the model bends to fit.

**Takeaway:** Prompts are like levers—add constraints, and the machine’s behavior shifts.

---

## 2. Prompt Tuning Competition: Banana Challenge

**Goal:** Teach iteration and experimentation.
**How to run:**

* Task: *“Get ChatGPT to produce the funniest possible description of a banana in exactly 2 sentences.”*
* **Round 1:** Each group writes their best prompt and runs it.
* **Round 2:** They iterate—add constraints (“use Shakespearean insults,” “make it a haiku”), retry, compare.
* Groups share their funniest results. Everyone votes on the winner.

**Variation:** Afterward, ask ChatGPT: *“Write a better prompt for the banana challenge.”* → Show that AI can help generate its own prompts.

---

## 3. Ambiguity vs Clarity

**Goal:** Highlight how vague prompts produce vague answers.
**How to run:**

* Start with *“Write a report on climate change.”* → Boring, generic.
* Refine step by step:

  * *“Write a 200-word report on climate change.”*
  * *“Include 3 causes and 3 solutions.”*
  * *“End with a call to action.”*
* Then run a student activity: give each student a vague base prompt like *“Tell me about cats.”*

  * Round 1: they run it.
  * Round 2: they refine with your help (length, details, structure).
  * Round 3: polish further (style, tone, output format).

**Takeaway:** More clarity = more control.

---

## 4. Prompt Anatomy: Building the Sandwich

**Goal:** Give them a framework for thinking about prompts.
**Mini-lesson:**
Explain the 5 parts of a strong prompt:

* **Context** (who/what/where)
* **Task** (what to do)
* **Constraints** (rules: tone, word count, style)
* **Output format** (paragraph, table, poem, list)
* **Examples** (optional, but powerful)

**Demo:**

* Prompt: *“You are a Spartan general speaking to your troops. Write a 3-sentence pep talk before battle. Use simple words, no more than 8 words per sentence.”*
* Point out exactly how each “part” of the sandwich was applied.

**Activity:**

* Hand out slips of paper with “Write about a cat.”
* **Round 1:** Add context (*“You are a pirate talking about a cat”*).
* **Round 2:** Add constraints (*word count, tone*).
* **Round 3:** Add format (*make it a limerick, a shopping list, etc.*).
* Share results—compare how wildly different they get.

---

## 5. Iteration Demo: The Dragon Story

**Goal:** Show how step-by-step refinement matters.
**How to run:**

* Start with *“Write a bedtime story about a dragon.”*
* Refine together:

  * *“Make it suitable for a 5-year-old.”*
  * *“Add a moral about sharing.”*
  * *“Write it in the style of Dr. Seuss.”*

**Takeaway:** Prompt engineering is iterative—layer changes, don’t expect perfection first try.

---

## 6. System/User Roles (Playground)

**Goal:** Show how “system” instructions change behavior.
**Demo:**

* System = *“You are a sarcastic pirate.”*
* User = *“Explain photosynthesis.”*
* See how tone overrides.
* Let students invent their own system roles (robot, wizard, grumpy teacher) and try them.

---

## 7. Conflicts & Randomness

**Goal:** Explore model limits.
**Examples:**

* *“Write a summary of Hamlet in one paragraph. Make it exactly two words long.”*
* Or: *“List 10 animals but only give me 3.”*
  Students see how the model “chooses” which instruction to follow, often inconsistently.

---

## 8. Birthday Song Challenge (Quickfire)

**Goal:** End on a playful, high-energy activity.
**How to run:**

* 2-minute challenge: *“Write the best possible prompt to get ChatGPT to write a birthday song for a turtle.”*
* Students test theirs, share results, funniest one wins.

**Takeaway:** Prompt engineering = programming in English. They’re just learning the “spells.”




# Extension Activities for Prompt Engineering



## 1. **Spelling & Noise Tolerance**

**Goal:** Show AI’s robustness but also limits.
**Demo:**

* Prompt: *“Explane the solar sistum in detale.”*
* Compare to: *“Explain the solar system in detail.”*
* Try: *“Explain teh solr systm in exstreem detale pls!!!”*

**Activity:**

* Each student intentionally makes a “messy” prompt (typos, slang, ALL CAPS, emoji spam).
* Compare outputs. Did the AI still understand? Where did it break?

**Takeaway:** AI is forgiving, but clarity = power. Garbage in → sometimes garbage out.

---

## 2. **Knowledge vs Conversation Engines**

**Goal:** Differentiate between LLMs and factual tools.
**Demo:**

* Ask ChatGPT: *“What’s the exact population of Canada today?”* (It may hedge or give an outdated number.)
* Then use Wolfram Alpha or Google.
* Contrast: conversational “best guess” vs factual retrieval.

**Activity:**

* Give groups a list of questions (e.g., *“Who won the last World Cup?”* vs *“Explain why soccer is popular in Brazil.”*).
* They decide: Which is better for ChatGPT, which for Google/Wolfram?

**Takeaway:** LLMs are storytellers first, encyclopedias second.

---

## 3. **AI for AI: Meta-Prompting**

**Goal:** Show recursive thinking with prompts.
**Demo:**

* Ask: *“Give me 5 better prompts to ask you about dinosaurs.”*
* Then run one of its own suggested prompts.

**Activity:**

* Each student writes a vague base prompt (*“Tell me about space”*).
* They then ask AI: *“Make this prompt better.”*
* Compare the “before” and “after” outputs.

**Takeaway:** You can use AI itself as your co-pilot in prompt engineering.

---

## 4. **Tone & Voice Olympics**

**Goal:** Explore tonality and style control.
**Demo:**

* Same task, different tones: *“Explain how a toaster works as…”*

  * a Shakespearean actor,
  * a YouTube influencer,
  * a kindergarten teacher,
  * a cat.

**Activity:**

* Students draw random “tone cards” (pirate, drill sergeant, grandma, alien, news reporter, etc.).
* They must prompt ChatGPT to explain the same topic (*how rainbows form*) in that style.
* Share funniest results.

**Takeaway:** Tonality = part of prompt anatomy. Control style, not just content.

---

## 5. **Prompt Telephone**

**Goal:** Show how iteration warps meaning.
**How to run:**

* Round 1: One student writes a base prompt (*“Write a limerick about a robot.”*).
* Round 2: Another student must *rewrite* the prompt slightly (add or remove constraints).
* Round 3: Another student iterates again.
* After 4–5 rounds, compare the final output to the original.

**Takeaway:** Small changes ripple—iteration is powerful but must be guided.

---

## 6. **Conflicting Instructions Deep Dive**

**Goal:** Explore inconsistency and model decision-making.
**Examples:**

* *“Write a 1000-word essay in exactly 5 words.”*
* *“List 10 animals but give me only 2.”*
* *“Write a happy poem that is also tragic.”*

**Activity:**

* Students invent their own contradictory prompts.
* Everyone runs one and shares how ChatGPT “resolved” the conflict.

**Takeaway:** The AI often chooses one instruction arbitrarily—precision avoids surprises.

---

## 7. **Hidden Constraints Challenge**

**Goal:** Teach subtle prompt control.
**Demo:**

* Ask: *“Write a story about a detective.”* (Generic.)
* Then add hidden rules: *“…but every sentence must start with the letter ‘S’.”*
* Or: *“…only use words of one syllable.”*

**Activity:**

* Students design quirky “hidden rules” for their classmates’ prompts.
* They then test them and see how well ChatGPT adapts.

**Takeaway:** The more unusual the constraint, the more you see model flexibility.

---

## 8. **Prompt Debugging**

**Goal:** Treat prompts like code with bugs.
**How to run:**

* Give students a “broken” prompt that doesn’t deliver the intended output.
  Example: *“Write a list of planets in order.”* (It may include Pluto or miss formatting.)
* Students must rewrite the prompt until the output is perfect.

**Takeaway:** Debugging prompts is just like debugging programs.

---

## 9. **Prompt Remix (Collaborative Writing)**

**Goal:** Creativity and iteration.
**How to run:**

* Student A gives base prompt: *“Write a horror story about a toaster.”*
* Student B refines: *“…but make it funny.”*
* Student C: *“…and only 4 sentences.”*
* Student D: *“…told from the toaster’s perspective.”*
* Run final version.

**Takeaway:** Prompts are modular—you can remix constraints endlessly.

---

## 10. **Chain of Prompts (Multi-step Workflow)**

**Goal:** Show how prompts can build on each other.
**Example:**

1. Prompt 1: *“Give me 10 random animals.”*
2. Prompt 2: *“Pick one and invent a superpower for it.”*
3. Prompt 3: *“Now write a comic book backstory for this superhero animal.”*

**Activity:**

* Groups design a “3-step chain” of prompts where each builds on the last.
* Compare wild final outputs.

**Takeaway:** Prompting isn’t always one-shot—it’s often sequential.

---

## 11. **Prompt Speedrun**

**Goal:** Add time pressure, keep energy high.
**How to run:**

* Give students a challenge like: *“Make the AI write a haiku about pizza in under 1 minute.”*
* First one to succeed “wins.”
* Play multiple rounds with escalating difficulty.

---

## 12. **Role Reversal: Students as the AI**

**Goal:** Reinforce that prompts are instructions.
**How to run:**

* One student is “the AI.” Others give prompts like:
  *“Explain gravity in 5 words.”*
  *“Write a rap about homework in the style of Eminem.”*
* The “AI” student has to respond as literally as possible.

**Takeaway:** Students *feel* what it’s like to be “programmed” by prompts.


