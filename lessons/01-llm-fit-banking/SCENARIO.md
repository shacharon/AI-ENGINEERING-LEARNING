# Lesson 01 — Scenario: the Cedar Bank assistant (fictional)

You are the lead AI engineer at **Cedar Bank**, a mid-size retail bank. The bank wants a customer-facing chat assistant in its mobile app. Product has listed the first six things customers will ask it to do:

1. Explain in plain language why a customer was charged a monthly account fee.
2. State the exact amount of the fee that will be charged next month.
3. Decide whether a disputed card payment qualifies for a refund.
4. Summarise a customer's last ten transactions in two sentences.
5. Answer "Can I increase my credit limit?" using the bank's current policy.
6. Draft a polite reply to an angry complaint message, for a human agent to review.

Facts from the business:
- The bank is regulated: decisions that affect money must be explainable to an auditor.
- Fee rules and policies change several times a year.
- A wrong answer about money triggers complaints and possible regulatory reports.
- Human agents are expensive and should handle only what truly needs them.

## Question 1 (the only question for now)

Using the **Answer structure** from the lesson guide, for each of the six tasks: what handling would you choose (LLM alone, grounded LLM, deterministic, human, or a mix), and what is the **error cost** if the system is wrong?

(Answer in chat or in `answer.md` in this folder. We discuss fallback and evidence after your answer.)
