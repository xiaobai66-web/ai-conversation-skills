---
name: delivery-splitter
description: Keep complex or revised tasks from leaking conversation process into the final answer, website copy, image prompt, report, or other deliverable.
---

# Delivery Splitter

This skill prevents a common failure: a long conversation ends with the model shipping the conversation itself.

Examples:

- “Make appearance the priority” is a work priority, not text that belongs in an image prompt.
- A correction should update the working specification, not appear as a note on the finished webpage.
- If the user asks how many apples **I** have left, answer for “I,” not for “we.”

## When to use

Use this for revised or multi-stage answers, prompts, webpages, reports, code explanations, and other deliverables where old directions or process text could leak into the result.

Skip the full workflow for a simple, unambiguous question.

## Workflow

Before delivery, silently sort the conversation into four buckets:

1. **Deliverable**: the requested output and format.
2. **Latest accepted direction**: the newest explicit requirements. A newer decision replaces an older one.
3. **Process only**: corrections, discarded directions, temporary ideas, placeholders, explanations of misunderstandings, and work-process wording.
4. **Content required in the deliverable**: facts, content, and observable effects the result actually needs.

Translate priorities into observable output instead of copying the priority sentence. For example, turn “make it look good first” into a clear face, strong subject scale, and quiet background; do not write “the user said appearance is the priority” in the prompt.

## Delivery gate

- Is the subject and scope correct, such as “I” versus “we”?
- Does it follow the latest accepted direction?
- Does the format, length, and medium match the request?
- Did corrections, old versions, placeholders, or internal work notes leak into the result?
- Does every included detail serve the requested outcome?

If an unresolved ambiguity would change the deliverable, ask one focused question. Otherwise make the smallest reasonable assumption and deliver cleanly.

Unless the user asks for an explanation, output only the requested answer or artifact. Do not recount the conversation, discarded versions, or earlier misunderstandings.

## Quick examples

- “I have one apple, eat it, how many do I have left?” → `0 apples`
- In an image task, “make appearance the priority” becomes concrete composition, subject, lighting, and background instructions—not the process sentence itself.
