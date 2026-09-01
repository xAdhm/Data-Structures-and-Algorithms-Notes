# Interview Process - Stages of an Interview

Most algorithmic interview rounds run **45–60 minutes**, broken into distinct stages. Advice for maximizing success at each.

## 1. Introductions
Interviewer briefly introduces themselves and their role, then asks you to introduce yourself.
- Prepare and rehearse a **30–60 second** self-introduction covering education, work experience, and interests. Smile, speak confidently.
- **Pay attention** to what the interviewer says about their work — useful for questions later (see [[Interview Process - Stages of an Interview#7. Outro|Outro]]).
- If they mention something you're also interested in (their work, a hobby), mention the connection.

## 2. Problem Statement
Interviewer presents the problem (often pasted into a shared editor along with a test case, then read aloud).
- **Confirm understanding** by paraphrasing the problem back to them.
- **Ask clarifying questions** about the input:
  - Only integers, or other types too?
  - Sorted or unsorted?
  - Guaranteed non-empty, or could it be empty?
  - What to do with invalid input?
- **Ask about expected input size** — even a vague answer is a useful clue:
  - Very small `n` → likely [[Backtracking - Overview|backtracking]]
  - `n` around 100–1000 → an O(n²) solution might be optimal
  - Very large `n` → probably need better than O(n)
- **Walk through the example test case(s)** quickly to confirm understanding.

Clarifying questions aren't just for your own understanding — they demonstrate attention to detail and edge-case awareness to the interviewer.

## 3. Brainstorming DS&A
- Break the problem down, look for familiar patterns, and figure out what data structure/algorithm accomplishes the goal with good time complexity.
- **Think out loud.** Demonstrates you're weighing tradeoffs — e.g. explicitly say "since this involves subarrays, I'm considering a sliding window, since every window represents a subarray." Even being wrong out loud is valuable; the interviewer appreciates visible reasoning. The best way to build this skill is simply practicing problems.
- Thinking out loud also lets the interviewer **give hints** and redirect you.
- Before coding: outline rough algorithm steps, explain them, and get the interviewer's buy-in that the approach is reasonable. A subtle hint from them is often a signal you're off track.
- **Be receptive to interviewer input** at this stage — they already know the optimal solution, and hints exist to help you succeed. Don't be stubborn; be ready to explore their suggested direction.

## 4. Implementation
- If planning to use a library/module (e.g. Python's `collections`), **confirm it's allowed** before using it.
- **Narrate your decisions** as you write — e.g. explaining that a `seen` set on a graph problem prevents revisiting nodes and thus prevents cycles.
- **Write clean code** — follow standard language conventions (case, indentation, spacing, globals). Know your language's basics.
- **Avoid duplicated code** — e.g. loop over a `directions` array instead of writing near-identical logic 4 times for 4 directions (see [[Graphs - Number of Islands Example]] for this exact pattern). Similar code repeated in multiple places is a signal to extract a function or loop.
- **Use helper functions freely** — improves modularity (mirrors real software engineering practice) and can make follow-ups easier to handle.
- **Don't panic if stuck.** Communicate concerns openly — struggling in silence makes it much harder for the interviewer to help.
- **Useful strategy:** implement a brute force solution first (acknowledging it's suboptimal), then analyze which parts are "slow" and discuss how to speed them up — with the interviewer, not alone.

## 5. Testing & Debugging
Testing environment varies by company:

**Built-in test cases, code is run** (LeetCode-style) — widest variety of test cases (small, huge, edge cases) automatically applied; puts the most pressure on solution correctness but least on writing your own tests.

**Write your own test cases, code is run** (shared editor with execution) — call your function with self-written tests and print results in the outermost scope. Include a variety: edge cases, intuitive inputs, and (if relevant) invalid inputs.

**Write your own test cases, code is not run** (plain shared editor) — manually walk through test cases by hand. Condense trivial parts verbally (e.g. "after this loop, the prefix sum array looks like..." rather than tracing every iteration). Track variable values by writing them out and updating them as you narrate.

**If a bug turns up:**
- If code execution is available: add print statements at relevant points to isolate the issue.
- Otherwise: manually trace a small test case, narrating expected vs. actual variable values at each step.
- Staying vocal throughout makes it easier for the interviewer to help you find it.

## 6. Explanations and Follow-ups
Expect these questions after coding:
- **"What's the time and space complexity?"** — answer in terms of worst case, but also mention average case if it's meaningfully better and the worst case is rare.
- **"Why did you choose to do ___?"** — be ready to explain data structure choices, algorithm choices, loop configurations, etc.
- **"Could this be improved?"** — if the problem inherently requires examining every element (e.g. finding max in an unsorted array), O(n) is likely already optimal; otherwise O(log n) may be the ceiling. If asked this question, the answer is *usually* yes — be careful not to over-assert optimality. Being wrong is fine; being **confidently** wrong is not.

If time remains: either an entirely new problem (restart from stage 2) or follow-ups on the current one — new constraints, tighter space complexity requirements, etc. This is exactly why genuinely **understanding** a solution (not just memorizing it) matters.

## 7. Outro
The interviewer typically reserves a few minutes for your questions about them/the company.
- This is unlikely to *improve* your outcome at this point, but can definitely *worsen* it.
- Interviews are two-way — use this time to genuinely evaluate whether you'd want to work there.
- **Prepare questions in advance**, e.g.:
  - What does an average day look like?
  - Why did you join this company over others?
  - What's your favorite/least favorite part of the job?
  - What kind of work can I expect?
- Reading the company's tech blog beforehand and preparing specific questions about their engineering decisions is a strong way to show genuine interest.
- **Stay engaged:** smile, listen actively, ask follow-ups based on their answers.
- Lacking good questions or appearing bored/uninterested sends a bad signal — technical performance alone doesn't guarantee a good outcome if the interviewer doesn't enjoy the conversation.

#interview-prep #soft-skills

Related: [[Backtracking - Overview]]
