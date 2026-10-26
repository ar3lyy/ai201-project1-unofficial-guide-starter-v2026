
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

**Question:**

How are housing lottery numbers assigned to rising sophomores?

**Answer:**

Rising sophomores get a number drawn at random for the housing lottery.

Source: admin_housing_lottery.txt

Sources retrieved: admin_dining_dollars.txt, admin_housing_lottery.txt, admin_meal_plan_changes.txt, advising_registration.txt, housing_tamsin_court.txt

**My relevance cutoff:** 0.6

I decided to keep the relevance cutoff at 0.6 after comparing five questions that my campus_life documents cover with five unrelated questions. The in-corpus questions had distances ranging from 0.186 to 0.551, while the out-of-scope questions ranged from 0.825 to 0.934.

There was a clear gap between the two groups. Keeping the cutoff at 0.6 allows all five of my campus-related questions to be answered while rejecting all five unrelated questions. I also noticed that the registration question had a higher distance of 0.551, so setting the cutoff too low could incorrectly reject a question the documents can answer.

| Question | In corpus? | Best distance |
|---|---|---|
| How are housing lottery numbers assigned to rising sophomores? | Yes | 0.202 |
| How are juniors and seniors prioritized in the housing lottery? | Yes | 0.205 |
| How quickly do student parking permits for the west lots sell out? | Yes | 0.193 |
| How much does it cost to wash clothes at Morrow House? | Yes | 0.186 |
| What must students have lifted before registering for classes? | Yes | 0.551 |
| What is the capital of Mongolia? | No | 0.825 |
| How do I change the oil in a diesel engine? | No | 0.934 |
| Who won the 1994 World Cup? | No | 0.886 |
| What is the recommended dosage of ibuprofen for a headache? | No | 0.844 |
| How do I write a for loop in Rust? | No | 0.891 |

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

**1. Creating my chunking strategy**

I used ChatGPT to help me understand how to improve the starter's chunking function. I explained that my campus_life corpus had 88 documents with an average length of 317 characters. ChatGPT suggested using paragraph-based chunking with a target of 400 characters and no overlap. I added the suggested function to chunker.py and tested it. The new strategy produced 100 chunks instead of 88, and I checked five sample chunks to make sure the information was readable.

**2. Testing retrieval and choosing a relevance cutoff**

I used ChatGPT to help me understand the retrieval distances from my test questions. After running five campus-related questions and five unrelated questions, I shared the results. ChatGPT helped me compare the distances and suggested keeping the cutoff at 0.6. I decided to keep that value because all five campus questions were answered correctly, while all five unrelated questions were rejected.

---

# Unit 2

<!-- Complete the following sections during Unit 2.
Keep your Unit 1 documentation unchanged. -->

## Run Log — Before


| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. Chunks contain complete information | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 5. Answers include expected information | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |

### Evidence from the Before Evaluation

**Criterion 1 — Retrieved chunks contain the answer**

Question: How quickly do student parking permits for the west lots sell out?

Best distance: 0.1928

Sources retrieved: admin_parking_permits.txt, advising_registration.txt, dining_halden_hall.txt, transit_shuttle.txt, transit_walking.txt

The retrieved document admin_parking_permits.txt contains the information that west lot permits sell out in about three days.

Produced by: `store.py::search`

**Criterion 2 — Every answer names a source**

Question: How are juniors and seniors prioritized in the housing lottery?

Actual output:

    Juniors and seniors are ordered first by accumulated credit hours, with any ties broken randomly.

    Source: admin_housing_lottery.txt

Produced by: `run_eval.py::main`

**Criterion 3 — Relevance gate stops unrelated questions**

Actual output from the evaluation:

    Out-of-scope questions (the gate should refuse these):
    refused (best distance 0.825) What is the capital of Mongolia?
    refused (best distance 0.934) How do I change the oil in a diesel engine?
    refused (best distance 0.886) Who won the 1994 World Cup?
    refused (best distance 0.844) What is the recommended dosage of ibuprofen for a headache?
    refused (best distance 0.891) How do I write a for loop in Rust?
    gate refused 5 of 5

Produced by: `run_eval.py::check_out_of_scope`

**Criterion 4 — Chunks contain complete information**

Sample from the chunk inspection:

    On the add/drop deadline

    You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.

Source: `admin_add_drop_deadline.txt#0`

Produced by: `chunker.py::split_documents`

**Criterion 5 — Answers include expected information**

Question: How much does it cost to wash clothes at Morrow House?

Expected phrase: $1.50

Actual output:

    It costs $1.50 to wash clothes at Morrow House (housing_morrow_house.txt and housing_morrow_house_laundry.txt).

Produced by: `run_eval.py::main`


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
