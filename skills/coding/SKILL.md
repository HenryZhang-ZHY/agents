---
name: coding
description: "Guide LLM Agents to code using the user's preferred workflow: clarify the problem, define the goal, use TDD with small iterations, and commit atomic units of work."
---

# Coding

Use this skill whenever an LLM Agent is asked to implement, fix, refactor, or otherwise change code.

## Principles

1. **Define the problem clearly.** A problem that can be described clearly in language is already mostly solved. Start by making the current problem explicit before coding.
2. **Define the target from the problem.** State the final goal for the current coding round so the agent knows what outcome it is optimizing for.
3. **Use TDD.** Drive coding with tests. Work in small, fast iterations: write or adjust a focused test, make the smallest implementation change that passes it, then refine.
4. **Make atomic git commits.** After completing each atomic unit of the coding task, create one commit for that unit before moving on.

## Workflow

1. Clarify the problem in concrete language.
2. Derive the goal for the current coding round from that problem definition.
3. Break the work into atomic units that can be tested and committed independently.
4. For each unit:
   1. Write or update a focused test that captures the intended behavior.
   2. Implement the smallest correct change.
   3. Run the relevant test.
   4. Commit the completed unit with an atomic git commit.
5. Continue with the next unit until the coding goal is complete.
