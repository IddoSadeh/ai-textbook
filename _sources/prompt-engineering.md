# Prompt Engineering for Beginners 

## What Is an LLM?

A **Large Language Model (LLM)** is a computer program trained to predict the next token in a sequence of tokens.

A **token** is a unit of input. In text, it might be a whole word, part of a word, or punctuation. In image models, tokens can even be pixels or patches.

To understand training, start with a simple math function:

```
y = mx + b
```

Here, *y* is the output, *x* the input, and *m* and *b* are values learned from data.

An LLM is like a much more complicated version:

```
y = a₁x₁ + a₂x₂ + a₃x₃ + ...
```

where each *x* is a token from your prompt (converted into a number), each *a* is a learned weight, and *y* is the model’s guess for the next token.

### Example: Predicting the Next Word

Prompt:

```
The cat sat on the
```

Step 1 – Assign IDs to tokens (toy example):

* “The” → 101
* “cat” → 57
* “sat” → 88
* “on” → 230
* “the” → 101

Step 2 – Multiply by weights (simplified):

```
y = a₁(101) + a₂(57) + a₃(88) + a₄(230) + a₅(101)
```

Step 3 – Convert *y* into probabilities:

* P(“mat”) = 0.62
* P(“floor”) = 0.21
* P(“dog”) = 0.05

The model predicts the next word is **“mat.”**

This is all an LLM does: adjust weights so it gets very good at predicting the next token. Different models (ChatGPT, Claude, Gemini) are trained on different data, so their weights differ—and that makes their answers feel different.

An interesting blog post on the different "personalties" of different LLM's https://guive.substack.com/p/alignment-fine-tuning-is-character

## Prompts and Prompt Engineering

A **prompt** is the input we give to the model. Even small tweaks can have a big impact on the output.

**Example: Cookie Recipe**

* Prompt: *“Give me a recipe for cookies.”* → Output: a generic recipe (usually chocolate chip cookies, the most popular).
* Prompt: *“My doctor recommended me to make cookies, can you give me a recipe?”* → Output: still a cookie recipe, but with less sugar.

The structure of the prompt acts like different *x* values in our earlier equation: the weights stay the same, but new inputs change the prediction. Prompt engineering is the art of constructing the right prompt to get your desired results.



## Some Basic Rules

### Avoid Redundancy

Stacking the same word (“very very very funny”) doesn’t change much. The model has learned that repetition adds little signal.

**Example:**

* “very” → token ID 412
* Adding “very” five times means the input looks like: \[banana, 57], \[very, 412], \[very, 412]…
* The model’s weights downplay redundancy, so predictions don’t shift much.

**Better approach:** Use descriptive words like “hilarious” or “absurd.”

### Tokens and Context Windows

An LLM only remembers a limited number of tokens at once—its **context window.**

**Example:** Suppose the context window is 8 tokens.

Prompt:

```
Once upon a time there was a little dragon who
```

Tokenized (toy IDs): \[11, 56, 78, 93, 45, 32, 67, 120, 22, 99]

Only the last 8 tokens fit in the window: \[78, 93, 45, 32, 67, 120, 22, 99]

So when predicting the next word, the model has already “forgotten” *Once upon.*

As conversations get longer, important details may fall out of memory, which is why the model sometimes repeats itself or contradicts earlier parts.

Modern context windows can be enormous—upwards of a million tokens—but even then, performance tends to degrade as more tokens are used.

### Dilbert on Writing

Scott Adams’ blog post on writing is a good reminder of why clarity matters: [The Day You Became a Better Writer](https://dilbertblog.typepad.com/the_dilbert_blog/2007/06/the_day_you_bec.html)

### Quirks and Limits

LLMs sometimes glitch on unexpected questions. A common quirk is asking them to count letters in a word. See the Reddit thread on [the “strawberry problem”](https://www.reddit.com/r/OpenAI/comments/1e6dl54/why_the_strawberry_problem_is_hard_for_llms/).

#### Side Note on Spelling

Because of how tokenization works, models are surprisingly forgiving of typos.

**Example:**
Prompt: *“Explain the solr systm.”*

Tokenized: \[Explain, 209], \[the, 101], \[solr, 803], \[systm, 690]

Even though “solr” and “systm” aren’t standard words, the model links them to “solar” and “system.”

Probabilities:

* P(“system”) = 0.74
* P(“sun”) = 0.12
* P(“planet”) = 0.07

So the model still explains the **solar system.**

But if tokens are too far from known ones, predictions become unreliable.

### Another Quirk: Seahorse Emoji

Prompt: *“Does a seahorse emoji exist?”*

LLMs often glitch here: they may confidently say “yes,” try to show it, and fail—cycling through horse, fish, or unrelated emojis. This happens because LLMs are prediction machines, not reasoning engines. Outlier prompts push them into unstable behavior.

---

## Conflicting Instructions

When a prompt includes contradictions, the model can’t satisfy everything.

**Example:**
Prompt: *“Write a summary of Hamlet in one paragraph and exactly two words.”*

Tokens: \[summary, 601], \[paragraph, 340], \[two, 405], \[words, 512]

Weights pull in two directions:

* “paragraph” pushes toward generating many tokens.
* “two words” pushes toward brevity.

The model must choose. It might output:

* *“Tragic prince.”* (obeys “two words”)
* *“Hamlet is a story of revenge and tragedy…”* (obeys “paragraph”).

Which path it takes depends on how the instructions interact in the function.

---

## Anatomy of a Strong Prompt

Good prompts balance five elements:

1. **Context** – who/what/where the AI should “be.”
2. **Task** – what you want it to do.
3. **Constraints** – rules (tone, word count, style).
4. **Output format** – how the response should look.
5. **Examples** – optional but powerful.

**Example Prompt:**

```
You are a Spartan general.
Write a pep talk in 3 sentences.
Use simple words.
No sentence may exceed 8 words.
Here is an example pep talk:
[insert example]
```

Tokens: \[Spartan, 742], \[general, 188], \[pep, 611], \[talk, 330], \[simple, 190], \[words, 512] …

These tokens activate strong associations with brevity and command, leading to short, forceful lines.

---

## Iteration: Prompts as Drafts

Prompting is iterative: like editing, you refine step by step.

**Example – The Dragon Story**

1. Prompt: *“Tell me a story about a dragon.”* → generic output.
2. Add constraint: *“…for a 5-year-old.”* → simpler words.
3. Add theme: *“…with a moral about sharing.”* → moralizing ending.
4. Add style: *“…in the style of Dr. Seuss.”* → rhyme and rhythm.

Each added token shifts the distribution until it matches the desired style. Often, it helps to run multiple versions to find the best result.

---

## Using AI to Improve Prompts

You can also ask the AI to improve your own instructions.

**Example:**
Prompt: *“Here’s my prompt: describe a banana in a funny way. Suggest a better version.”*

Model’s output might be:

* *“Describe a banana as if Shakespeare wrote a comedy about fruit.”*

Here, the token \[Shakespeare, 742] activates rich stylistic associations, producing more vivid outputs.


## Key Takeaways

* LLMs are giant functions predicting the next token.
* Tokens are numbers; weights tell the model how to combine them.
* Prompts are instructions—changing the tokens changes the output.
* Redundancy is weak; descriptive words are strong.
* Context windows limit memory: too many tokens push old ones out.
* Models handle typos but reward clarity.
* Contradictory prompts confuse predictions.
* Strong prompts balance context, task, constraints, format, and examples.
* Iteration works: each new token shifts the distribution closer to your goal.
* AI itself can help you craft better prompts.
* Quirks remind us: LLMs are powerful, but not perfect.
