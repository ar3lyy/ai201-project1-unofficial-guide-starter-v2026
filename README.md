
# The Unofficial Guide

**Name:** [Arely Morales]  
**Corpus:** campus_life

This project is part of CodePath AI201. It uses a document retrieval system to answer questions about student experiences on campus.

---

# Unit 1

## What This Does

The Unofficial Guide is a system that answers questions about student experiences using information from campus documents. I chose the campus_life corpus, which contains 88 documents covering topics like housing, parking, dining, classes, and registration. The system searches these documents for information related to a user's question and uses the retrieved information to generate an answer. It also provides the source documents so users can see where the information came from.

## Chunking Strategy

**Chunk size:** 400 characters (target)  
**Overlap:** 0 characters

I chose a target chunk size of 400 characters because most of the documents in the campus_life corpus are relatively short. When I first indexed the documents using the starter chunker, it created 88 chunks from 88 documents, with an average length of 317 characters. This meant that documents covering multiple topics were still being kept together.

I decided to use paragraph-based chunking instead of splitting the text at fixed character positions. My new function keeps shorter documents together and splits longer documents at paragraph boundaries. I chose no overlap because I wanted to avoid repeating information while keeping complete sentences and related ideas together.

After making this change, my system created 100 chunks from the 88 documents. The average chunk length decreased to 278 characters, with the shortest chunk being 94 characters and the longest being 400 characters. I think this strategy fits my corpus better because it separates information by paragraphs without cutting sentences in half.

## Sample Chunks

The following five chunks were generated using my custom chunking function.

**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::split_documents`

    On the add/drop deadline

    You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.

**Chunk 2** — source: `course_cs_210.txt#0` — produced by: `chunker.py::split_documents`

    CS 210 Data Structures

    I'm a junior and I've done this twice now. Format is lecture with weekly labs; slides go up after class, not before. Assessment: two midterms and a final, all drawn from lecture material rather than the textbook. Midterms are curved, the final is not.

    Expect 8 to 10 hours a week outside class.

**Chunk 3** — source: `course_math_220_workload.txt#0` — produced by: `chunker.py::split_documents`

    Workload for MATH 220 Linear Algebra

    People keep asking so: 6 to 8 hours a week, almost all of it on problem sets. That's real time, not optimistic time.

    It's front-loaded — the first month is heavier than the rest, partly because you're learning the format.

**Chunk 4** — source: `dining_the_ridgeway_cafe_followup.txt#0` — produced by: `chunker.py::split_documents`

    Re: The Ridgeway Café

    Adding to what people have said about The Ridgeway Café. The wait figure of 10 to 15 minutes at 12:30 matches what I've seen. If you're trying to eat between classes, go before 11:45 and it's a different building entirely.

    Also worth saying: seating is tight; about 40 seats for a building of 900. Nobody tells you this at orientation.

**Chunk 5** — source: `housing_morrow_house.txt#0` — produced by: `chunker.py::split_documents`

    Morrow House — what it's actually like

    Just finished a year in this building. Built 1954, partially renovated 2008. Rooms are singles and doubles, hall bathrooms.

    The good: cheapest housing tier by about $900 a year, and the singles are real singles.

    The bad: known damp problem on the ground floor; two rooms were taken offline in 2024.

## Sample Answer

<!-- Complete this section in Milestone 4.
Paste one complete question and answer from your current system,
including the source line. -->

**Question:**

**Answer:**

**My relevance cutoff:**

<!-- Record your selected cutoff and explain how you chose it
using five in-corpus and five out-of-scope retrieval distances. -->

| Question | In corpus? | Best distance |
|---|---|---|
| Question 1 | Yes | |
| Question 2 | Yes | |
| Question 3 | Yes | |
| Question 4 | Yes | |
| Question 5 | Yes | |
| Out-of-scope 1 | No | |
| Out-of-scope 2 | No | |
| Out-of-scope 3 | No | |
| Out-of-scope 4 | No | |
| Out-of-scope 5 | No | |

## How I Used AI

<!-- Complete this section in Milestone 5.
Describe two specific examples of how you used AI,
what it suggested, and what you changed or decided. -->

**1.**

**2.**

---

# Unit 2

<!-- Complete the following sections during Unit 2.
Keep your Unit 1 documentation unchanged. -->

## Run Log — Before

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | | | | |
| 2. Every answer names a source | 5 of 5 | | | | |
| 3. Gate stops out-of-corpus questions | 4 of 5 | | | | |
| 4. Chunks contain complete information | 4 of 5 | | | | |
| 5. Answers include expected information | 4 of 5 | | | | |

<!-- Paste real evaluation outputs here during Unit 2.
Include the file and function that produced them. -->

## Verdicts

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

## Diagnoses

<!-- For each missed criterion, explain which stage caused
the problem and why.

Stages: loading, chunking, embedding, retrieval, generation.

If no criteria were missed, explain whether your
targets were too easy and what you would tighten. -->

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect your change to one of the problems
you identified in the Diagnoses section. -->

### Run Log — After

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | | | | |
| 2. Every answer names a source | 5 of 5 | | | | |
| 3. Gate stops out-of-corpus questions | 4 of 5 | | | | |
| 4. Chunks contain complete information | 4 of 5 | | | | |
| 5. Answers include expected information | 4 of 5 | | | | |

**Did it help?**

<!-- Explain whether your improvement worked
using the results from your evaluation. -->

## What's Still Broken

<!-- Explain any criteria that are still unmet
and what you would do to improve them. -->

## What I'd Do Differently

<!-- Explain which acceptance criterion you would
write differently based on what you learned. -->
