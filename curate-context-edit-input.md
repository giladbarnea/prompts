Run `context_outline` with a `minTokens` value that fits within your context window and leaves enough headroom for the rest of this task. Ideally, use `minTokens=0`. You can use your entire context window for this task; you don't need to reserve space for work beyond it.

Then prepare a `context_edit` call that removes everything unambiguously irrelevant to our mission and summarizes material with some indirect relevance. Preserve a deep understanding of the domain while reducing noise.

Write a JSON file that holds only the arguments of your curated `edit_context` call: `{"operations": [...]}`. It must apply without any preliminary reading or research, with this CodeMode block and nothing more:

```js
const args = JSON.parse(await tools.read({ path: "<your file>", outputSizeLimitKb: "unlimited" }));
text(await tools.edit_context(args));
```

If you've just been forked for this task, your result will be relayed to the main session. A fork gets new entry IDs, so the IDs in your outline do not exist in the main session. The first line of your session file names the main session's file in `parentSession`. Match each entry you reference to the same entry in that file, by identical content, and write the main session's IDs in the JSON file and in your notes.

This script translates them: `node <script> $PI_SESSION_ID <entry ID>...`

```js
import { open } from '/Users/giladbarnea/.agents/skills/jsonl-toolkit/lib/pi.mjs';

const fork = open(process.argv[2]);
const main = open(fork.header.parentSession);
const key = entry => JSON.stringify(entry.message ?? entry.content ?? entry);
const mainIds = Map.groupBy(main.entries, key);
for (const prefix of process.argv.slice(3)) {
  const entry = fork.entries.find(candidate => candidate.id.startsWith(prefix));
  const matches = mainIds.get(key(entry)) ?? [];
  console.log(prefix, '→', matches.length === 1 ? matches[0].id : `${matches.length} matches`);
}
```

