---
name: conversation-summarizer
description: Summarizes the current conversation into a single portable Markdown file that the user can paste or upload into a new conversation to carry context forward. Use whenever the user asks to "summarize this conversation", "save this chat", "make a handoff file", "continue this later", "export context", or wants a file capturing what's been discussed so far. Produces a structured recap covering context/background, decisions made, code/technical details discussed, and open/pending tasks.
---
 
# Conversation Summarizer
 
Generates a single `.md` file summarizing the current conversation for reuse as context in a new conversation.
 
## Workflow
 
1. Review the full conversation history in context (do not ask the user to repeat anything already said).
2. Extract and organize into these sections (omit a section if genuinely empty):
   - **Context** — what the user is working on, project/background, relevant prior state.
   - **Decisions Made** — choices, conclusions, or directions the user confirmed or settled on.
   - **Technical Details** — code snippets, file paths, architecture notes, script/system names, key configs discussed. Preserve code blocks verbatim with language tags.
   - **Open / Pending Tasks** — anything unfinished, unresolved questions, next steps explicitly mentioned or implied.
   - **Other Notes** — anything relevant that doesn't fit above (preferences stated mid-conversation, constraints, etc).
3. Be specific: use real names (scripts, functions, features, systems) mentioned in the conversation, not vague paraphrases.
4. Do not editorialize or add information not present in the conversation.
5. Write the file using `create_file` to `/mnt/user-data/outputs/conversation-summary-<short-topic-slug>.md`.
6. Call `present_files` on it.
7. Tell the user, in one line, that it's ready to paste/upload into a new conversation as context.
## Format template
 
```markdown
# Conversation Summary: <topic>
 
## Context
...
 
## Decisions Made
...
 
## Technical Details
...
 
## Open / Pending Tasks
...
 
## Other Notes
...
```
 
## Rules
 
- No comments explaining the skill's own process inside the output file — just the content.
- Keep prose tight; prefer bullet points over paragraphs.
- Include code blocks exactly as discussed, not paraphrased, when technical accuracy matters.
- If the conversation is very long, prioritize the most recent/relevant thread of work over stale tangents, but don't silently drop major topics.
