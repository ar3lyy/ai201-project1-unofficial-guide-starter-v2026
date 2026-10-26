
# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1 **before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something a person could plainly observe.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that contains the answer.

**Why this target:**

I chose this target because my campus_life corpus contains 88 documents covering different topics about student life. Some questions might be harder to match with the right document than others. I think getting at least 4 out of 5 correct retrievals is a good goal because it shows the system can find useful information most of the time without expecting it to be perfect.

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**

I chose this target because I want students to know where the information in each answer comes from. Since the documents already have filenames, the system should be able to include a source every time it gives an answer. I chose all 5 answers instead of 4 because I think providing sources is important for making the system trustworthy.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate stops it and the system returns "I don't have enough information about that" — in at least 4 of 5 tries.

**Why this target:**

I chose this target because the system should only answer questions using the information in the campus_life documents. If someone asks something unrelated, I want the system to recognize that it doesn't have enough information instead of making up an answer. I chose 4 out of 5 because I want most unrelated questions to be rejected, while recognizing that the relevance cutoff might not work perfectly for every question.

---

## 4. Chunks contain complete information

At least 4 out of 5 sampled chunks should contain a complete thought without cutting off a sentence at the beginning or end.

**Why this target:**

I chose this target because the campus_life corpus contains relatively short documents. When I first indexed the corpus, the system created 88 chunks from 88 documents, with an average length of 317 characters. Since most documents are already short, I want the chunks to keep related information together instead of splitting sentences in the wrong places. I chose 4 out of 5 because I want nearly all the chunks I inspect to make sense on their own.

---

## 5. Answers include the expected information

For at least 4 of my 5 test questions, the system's answer should contain the expected information listed in the "expects" field in questions.py.

**Why this target:**

I chose this target because finding the right document is not enough if the system gives an incomplete or incorrect answer. I want students to receive information that actually answers their questions. The "expects" field gives me a specific word or phrase to check for each question. I chose 4 out of 5 because I want the system to provide accurate information for most questions, even if it occasionally misses an important detail.

---

<!-- UNIT 2

Keep these original criteria unchanged when evaluating the system in Unit 2.

If a criterion cannot be measured consistently, add a revision underneath the original criterion and explain why it needed to change.

Do not lower a target just because the system failed to meet it.

-->

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
