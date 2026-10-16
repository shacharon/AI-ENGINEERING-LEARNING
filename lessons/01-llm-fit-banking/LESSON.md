# Lesson 01 — When an LLM is the right tool: task fit and failure modes (Tier A: guided)

**Type:** discussion lesson. No code. Scenario is fictional.

## Vocabulary you must be able to define
LLM · probabilistic vs deterministic · hallucination · grounding (answering from supplied evidence) · retrieval · context · error cost (what a wrong answer costs) · fallback · human in the loop · auditability.

## What / why / when
- An LLM produces plausible text. It is strong at language: summarising, rewriting, explaining, extracting meaning from messy text. It is not a calculator, a database or a rules engine, and it can state wrong things fluently.
- **Why task fit matters:** the same model is excellent for one banking task and dangerous for another. Choosing the right tool per task is the first senior decision in any AI feature.
- **Four ways to handle a task:** (1) LLM alone, (2) LLM grounded in supplied evidence, (3) deterministic code or rules, (4) a human. Real systems mix them.
- **When it matters:** at the start of every AI feature discussion and in every senior interview. Skipping it leads to using an LLM where a lookup or a rule is cheaper, faster and exactly right.

## Trade-offs
| Approach | Strength | Risk |
|---|---|---|
| LLM alone | Flexible language, fast to build | Can invent facts; varies between runs; hard to audit |
| LLM grounded in evidence | Answers can be tied to a source | Wrong or stale evidence gives a wrong answer; more moving parts |
| Deterministic code / rules | Exact, testable, cheap, auditable | Rigid; poor with free-form language |
| Human | Judgment and accountability | Slow and costly; does not scale |

## Answer structure (Tier A guide)
For **each** task, use these headings:
1. **Task:** what exactly is asked.
2. **Handling:** LLM alone / grounded LLM / deterministic / human (a mix is allowed).
3. **Error cost:** what a wrong answer costs the customer and the bank.
4. **Evidence:** what the answer must be based on.
5. **Fallback:** what happens when it is unsure or fails.

## Worked mini-example of the *method* (a different problem)
*Company HR assistant, task: "How many vacation days do I have left?"*
- **Task:** report a number from an employee record.
- **Handling:** deterministic lookup; an LLM may only phrase the sentence around the number.
- **Error cost:** moderate; a wrong balance causes disputes.
- **Evidence:** the HR record, never the model's memory.
- **Fallback:** show "balance unavailable" and offer a human contact.
Notice that the model is not trusted with the fact; it is used only where language is the hard part.

## Common mistakes
- Giving every task to the LLM because it can "answer anything".
- Naming a handling without naming its error cost.
- Forgetting the fallback: what the customer sees when the system is unsure.
- Treating "grounded" as "always correct".
