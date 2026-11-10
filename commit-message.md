Generate a short commit message. If different changes serve a cohesive purpose, tell that purpose.
Make sure the commit message clearly conveys what was changed and why it was changed (overarching purpose), and what was before. Do not repeat yourself; be terse and concise. Condense (compress) descriptiveness and information LOSSLESSLY; in other words, pack as much "story" into as few words as possible. Readers should be able to answer the question "**What** was changed, and **why** (for what **purpose?**)" at a glance. 
If the changes span a single file, start the commit message with the file name. If the changes span multiple files, start with a short commit message capturing the overarching purpose, then a bullet list where each item starts with a file name. Do not use Markdown formatting nor straight single quotes. No intros, no outros.

Examples for the right amount of specificity:

- aliases.sh: Removed unused aliases `pio`, and `pis`, and added `off` and `xhigh` thinking levels at dynamic alias definition.
- completions/_pi: Added tools-oriented completion options, and enhanced existing session management completion options.
- convert.sh: Updated `pdf2md` function invocation to inject `HF_TOKEN` at runtime and use `ocrmac` OCR mode.
- skills.sh: Update the directory resolution logic to detect a wider variety of cases for more intuitive behavior.
