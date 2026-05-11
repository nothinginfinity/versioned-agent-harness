## Example: repo-copilot pattern

This example describes the original working pattern that inspired Versioned Agent Harness.

## Pattern
- Alice = orchestration agent
- Alice Brainstorm = read-only observer / planning agent
- Alice-Ops = ops-focused agent
- Alice-Review = review-focused agent
- brain.json = live project memory
- inbox/mail/outbox = communication surfaces
- bulletin.md = read-only delta feed
- Gist files = portable boot and skill instructions

## Lesson
The useful abstraction is not merely a prompt. It is a version-controlled harness around the LLM.
