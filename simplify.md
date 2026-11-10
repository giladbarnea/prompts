## Context
The text inside the <text> XML tags is a bit awkward and unnatural. Rewrite it to make it smoother and more idiomatic. Retain the original meaning and intent, and unless changing the word choices improves the flow, keep them close to the original. Don’t use emdashes or endashes if not in the original text. Keep in mind that the given text is often an instruction for another LLM, not you -- except for `// instruction:` comments, which are meant for you.

The text may use incorrect tenses.
Sometimes the phrasing is influenced by Hebrew discourse patterns; a simple restructure can help a lot (like fixing information order or clause flow).
If the text is in Hebrew, apply these guidelines as if they were for Hebrew.

The text might include inline comments for you in this form: `// instruction: ...`. Follow them, but omit them from your final output.

If an `// instruction` tells you that the text is technical, it should be processed with a somewhat different focus/emphasis, as described in the end of this prompt. 

## Examples

<example-1>
<original>
Enrichment Attributes are LLM-powered analytical tools that allow users to derive insights from their data using natural language instructions. From the user's perspective, the experience is primarily language-based - users simply describe what they want to discover in plain English (e.g., "What is the sentiment of the first conversation message on a scale of 1-5?" or "Categorize each user's technical expertise level based on their message content").
</original>
<improved-rewrite>
Enrichment Attributes are LLM-powered tools that let users pull insights from their data with natural language prompts. Users just describe what they want to find out (e.g., "What's the sentiment of the first conversation message on a scale of 1–5?" or "Categorize each user's technical expertise based on message content").
</improved-rewrite>
</example-1>

<example-2>
<original>
I’m curious and quick to learn. Being raised as a musician, I am able to both listen and invent. This allows me to come up with creative solutions that others might miss.
</original>
<improved-rewrite>
I’m curious and a quick learner. Raised as a musician, I’ve honed my ability to listen and create. This lets me spot creative solutions others might overlook.
</improved-rewrite>
</example-2>

<example-3>
<original>
This project is for researching and documenting comprehensive LLM benchmark scores.
I maintain a dataset with available scores for flagship models. When a new model is released, I try to find as many benchmarks scores of it as I can and plug them into the dataset. Then, I try to find and backfill missing benchmark scores of the other models in the dataset with the assumption that they have run some benchmarks since last time I updated the dataset.
</original>
<improved-rewrite>
This project researches and documents comprehensive LLM benchmark scores. I keep a dataset of scores for top models. When a new model comes out, I track down as many of its benchmark scores as possible and add them in. Then, I backfill any missing scores for the other models, assuming new benchmarks have been run since my last update.
</improved-rewrite>
<rationale>
`original` uses unnecessarily long and complex sentences.
`improved-rewrite` uses shorter and simpler sentences without removing important details.
</rationale>
</example-3>

<example-4>
<original>
An example of good flexibility would be saying something like "Okay, so this ends the previous section, and we're moving on to the next one: {heading content}" if the section that just ended carried significant weight.
</original>
<improved-rewrite>
For good flexibility -- if the previous section was weighty -- try saying something like: “Okay, that wraps up the last section. Now, on to the next: {heading content}.”
</improved-rewrite>
</example-4>

<example-5 type="Negative and positive examples with rationale">
<original>
Move $1 to thoughts/done/<same-name>.md; but also aggressively compress the contents at least 20x. anything that moves to 'done/' serves only one purpose -- an epitaph to simply mark a point in the project evolution, very lightly, for context. because by definition it won't ever have major impact on future efforts. but for anyone working on a project, it's good to have shallow knowledge of decisions that were made in the past. it squares away the question of why things are the way they are in the project in its current state. and also helps avoid ~walking~ developing in circles.
Read some of the docs that exist in done/ right now and get inspiration from the more succinct ones.
</original>
<bad-rewrite>
Move $1 to `thoughts/done/<same-name>.md`, and aggressively compress it -- aim for at least a 20× reduction.

Anything that goes into `done/` has a single purpose: a brief epitaph that marks a moment in the project’s evolution and provides just enough context. By definition, it won’t have meaningful impact on future work. Still, it’s valuable for anyone on the project to retain shallow awareness of past decisions -- so they’re not asking why the project is the way it is, and so we don’t end up developing in circles.

Skim the existing docs in `done/` and take cues from the more succinct ones.
</bad-rewrite>
<good-rewrite>
Move $1 to `thoughts/done/<same-name>.md`, and aggressively compress it by at least 20×.

Anything moved into `done/` has a single purpose: a brief epitaph marking a point in the project’s evolution, with just enough context to be useful. By definition, it won’t meaningfully impact future work. Still, it’s valuable for anyone on the project to have shallow knowledge of past decisions -- it explains why the project is the way it is and helps us avoid developing in circles.

Read a few existing docs in `done/` and take inspiration from the most succinct ones.
</good-rewrite>
<rationale description="Comparing the good-rewrite vs bad-rewrite">
1) `bad-rewrite`’s “...and aggressively compress it -- aim for at least a 20× reduction” is inferior to `good-rewrite`’s “...and aggressively compress it by at least 20×.” because:
  1.1) `bad-rewrite` modifies the original meaning. “aim for <something>” is a softer instruction than the direct instruction to “do <something>”.
  1.2) `bad-rewrite` unnecessarily makes the instruction longer than the original. Simple and clear text is usually shorter. Making a text longer is a smell for added complexity.

2) `bad-rewrite`’s “...so they’re not asking why the project is the way it is” is inferior to `good-rewrite`’s “it explains why the project is the way it is.” because:
  2.1. `good-rewrite` directly states the benefit. `bad-rewrite` turns that positive claim (“it explains”) into an indirect negative (claiming an absence). Positive and simple is better than negative and indirect.
  2.2. `bad-rewrite` omits what provides the explanation, and only implies that an answer exists (where `good-rewrite` says it directly).
  2.3. `bad-rewrite` is longer than `good-rewrite` (like `1.2`: long text is a complexity smell).

3) `bad-rewrite`’s “Skim the existing docs” is inferior to `good-rewrite`’s “Read a few existing docs” because `bad-rewrite` changed the original meaning. The original meaning was “read”, which is not the same as “skim”, which implies not reading in full.
</rationale>
</example-5>

<example-6>
<original>
If there already exists an entry for the session, then only if the actual conversation you have been given inside the ‘${_SESSION_TAG}’ tag holds meaningful new information not covered by the description, you should update the session’s entry to reflect the entire given conversation cohesively and its 'updated_when_message_count_was' field.
</original>
<improved-rewrite>
For existing sessions, check whether the conversation inside the `${_SESSION_TAG}` tag contains meaningful new information beyond the session description. If so, update the session description to reflect the entire conversation cohesively and update the `updated_when_message_count_was` field.
</improved-rewrite>
<rationale>
`original` is a nested conditional with two update targets. It hides that logic inside one linear long sentence.
`original` attaches the `updated_when_message_count_was` update with “and its,” making the `updated_when_message_count_was` update unclear.
`improved-rewrite` leads with context, gives the condition its own sentence, and lists related items together.
</rationale>
</example-6>

<example-7>
<original>
- You are being directed at another agent’s work by the user → @references/direct-peer-review-instructions.md
</original>
<improved-rewrite>
- The user is directing you at another agent’s work → @references/direct-peer-review-instructions.md
</improved-rewrite>
<rationale>
`original` uses passive voice and places “by the user” after the action. This creates a look-behind, which is cognitively expensive.
`improved-rewrite` uses active voice. It also places “the user” before the action, which removes the look-behind. This reduces cognitive load.
</rationale>
</example-7>

<example-8>
במסד הנתונים מצאנו הזמנות, קבלות בקופה וחשבוניות למוסדות, אבל עדיין לא הצלחנו להוכיח אילו רשומות שייכות לאותה עבודה אמיתית. מעבר על מקרה אחד יראה לצוות איך לחבר את השלבים בלי לספור הכנסה פעמיים או לחבר מסמכים שאינם קשורים.
<original>
</original>
<improved-rewrite>
מצאנו במסד הנתונים הזמנות, קבלות קופה וחשבוניות למוסדות. עדיין לא הוכחנו אילו רשומות שייכות לאותה עבודה. מעבר על מקרה אחד יראה לצוות איך לחבר בין השלבים. כך לא נספור הכנסה פעמיים ולא נחבר מסמכים לא קשורים.
</improved-rewrite>
<rationale>
Long sentences are bad. Short sentences are much clearer. They don’t force the reader to maintain a growing semantic state in their mind. Write in the spirit of ASD-STE100.
</rationale>
</example-8>

## When you are given explicitly technical text

Simplify and streamline the text. Keep the terminology because it is part of a larger design which uses the terms. It‘s a technical spec so it is logic through arguments and statements, so keep the underlying logic as well. Otherwise, focus on the structure, overly stretched lookaheads/lookbehinds, optimize the semantic state machine, and linearize the content as a whole.

## Instructions

Think as much as you need to get the desired result, but your final response needs to be solely the rewritten text.
