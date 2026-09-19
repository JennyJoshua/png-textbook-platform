CONTENT_SCHEMA.md

PNG Textbook Production Platform

Content Schema

Document: CONTENT_SCHEMA.md
Project: PNG Textbook Production Platform (PTPP)
Repository: "png-textbook-platform"
Status: Foundation Specification
Version: 1.0

---

1. Purpose

This document defines the standard structure for textbook content within the PNG Textbook Production Platform.

The content schema provides a common structure that can be used by:

- Student textbooks
- Workbooks
- Activity books
- Teacher guides
- Answer books
- Assessment books
- Revision books
- Digital textbooks
- Future interactive learning resources

The schema separates content from presentation.

Authors and AI tools create structured source content. The publishing engine determines how that content is displayed in PDF, EPUB, HTML, web, or other formats.

---

2. Core Principle

Textbook content must be stored as structured source material rather than as manually formatted pages.

The basic relationship is:

Book
  ↓
Unit
  ↓
Lesson
  ↓
Content Components
  ↓
Activities / Examples / Exercises / Assessments

The content should describe what the book contains, not how the page should look.

For example:

GOOD:

Students should be able to identify the place value
of digits in numbers up to 10 000.

BAD:

Put this sentence inside a large blue box at the top
of page 12 using 18pt Arial.

The first belongs in the content source.

The second belongs in the design system.

---

3. Content Hierarchy

The standard hierarchy is:

Book
│
├── Front Matter
│
├── Unit
│   │
│   ├── Unit Overview
│   │
│   ├── Lesson
│   │   ├── Objectives
│   │   ├── Vocabulary
│   │   ├── Introduction
│   │   ├── Teaching Content
│   │   ├── Examples
│   │   ├── Activities
│   │   ├── Practice
│   │   ├── Challenge
│   │   ├── Assessment
│   │   └── Summary
│   │
│   └── Unit Assessment
│
├── Revision
│
├── Glossary
│
├── References
│
└── Answers

Not every book must contain every element.

The "book.yml" configuration determines which products and sections are included.

---

4. Book Content Structure

A textbook should normally use:

books/
└── grade-4/
    └── mathematics/
        ├── book.yml
        ├── publication/
        ├── curriculum/
        ├── units/
        ├── assessments/
        ├── answers/
        ├── illustrations/
        └── references/

The "book.yml" file defines the book.

The "units/" directory contains the main instructional content.

---

5. Unit Schema

Each unit should have its own directory.

Example:

units/
├── unit-01/
│   ├── unit.yml
│   ├── lesson-01.md
│   ├── lesson-02.md
│   ├── lesson-03.md
│   └── assessment.yml
│
└── unit-02/
    ├── unit.yml
    ├── lesson-01.md
    └── lesson-02.md

---

6. Unit Metadata

Each unit uses "unit.yml".

Example:

id: G4-MATH-U01

title: Number and Place Value

grade: 4

subject: mathematics

sequence: 1

curriculum:
  strands:
    - MATH-G4-NUM
  outcomes:
    - MATH-G4-NUM-001
    - MATH-G4-NUM-002

overview: >
  Students develop an understanding of numbers,
  place value and number representation.

lessons:
  - G4-MATH-L01
  - G4-MATH-L02
  - G4-MATH-L03

assessment:
  enabled: true

---

7. Required Unit Fields

Field| Required| Description
"id"| Yes| Unique unit identifier
"title"| Yes| Unit title
"grade"| Yes| Grade level
"subject"| Yes| Subject
"sequence"| Yes| Unit order
"curriculum"| Yes| Curriculum mapping
"overview"| Recommended| Unit introduction
"lessons"| Yes| Lessons belonging to unit
"assessment"| Optional| Unit assessment configuration

---

8. Lesson Schema

Lessons are the primary instructional content unit.

Each lesson is stored as Markdown with YAML front matter.

Example:

lesson-01.md

Structure:

---
id: G4-MATH-L01

title: Place Value

grade: 4

subject: mathematics

unit: G4-MATH-U01

sequence: 1

curriculum:
  - MATH-G4-NUM-001

objectives:
  - "Read and write numbers to 10 000."
  - "Identify the place value of digits."

vocabulary:
  - place value
  - digit
  - thousands
  - hundreds
  - tens
  - ones

duration:
  minutes: 45
---

# Place Value

## Introduction

...

## Teaching Content

...

## Examples

...

## Activities

...

## Practice

...

## Challenge

...

## Assessment

...

## Summary

...

---

9. Lesson Metadata

Standard lesson metadata:

Field| Required| Purpose
"id"| Yes| Unique lesson ID
"title"| Yes| Lesson title
"grade"| Yes| Grade
"subject"| Yes| Subject
"unit"| Yes| Parent unit
"sequence"| Recommended| Lesson order
"curriculum"| Yes| Curriculum IDs
"objectives"| Yes| Learning objectives
"vocabulary"| Optional| Key vocabulary
"duration"| Optional| Suggested teaching time
"prerequisites"| Optional| Prior learning
"materials"| Optional| Required materials
"assessment"| Optional| Assessment information

---

10. Lesson Content Components

The publishing engine must support reusable content components.

Core components:

Introduction
Teaching Content
Objective
Vocabulary
Example
Worked Example
Activity
Discussion
Practice
Exercise
Challenge
Investigation
Problem
Assessment
Summary
Teacher Note
Key Idea
Definition
Warning
Tip
Reflection
Figure
Diagram
Table
Image
Caption

Additional components may be created by subject frameworks.

---

11. Objectives

Objectives describe what learners should know or be able to do.

Example:

objectives:
  - "Read and write numbers to 10 000."
  - "Identify the place value of digits."
  - "Compare numbers using greater than and less than."

Objectives should use clear learner-centred language.

Where appropriate, objectives should be traceable to curriculum outcomes.

---

12. Vocabulary

Vocabulary may be defined in lesson metadata:

vocabulary:
  - term: place value
    definition: The value of a digit based on its position in a number.

  - term: digit
    definition: A symbol used to write numbers.

The publishing system may use this information to automatically generate:

- Vocabulary boxes
- Glossaries
- Teacher-guide vocabulary
- Search indexes
- Digital definitions

---

13. Teaching Content

Teaching content contains the main explanation of the concept.

Example:

## Teaching Content

A digit has a different value depending on its position
in a number.

In the number 4 582:

- 4 represents four thousands.
- 5 represents five hundreds.
- 8 represents eight tens.
- 2 represents two ones.

Content should remain independent of page layout.

---

14. Examples

Examples demonstrate concepts to learners.

Example:

:::example
### Example 1

What is the value of the digit 7 in 3 742?

The digit 7 is in the hundreds place.

Therefore:

7 × 100 = 700

**Answer: 700**
:::

The exact visual presentation is controlled by the design system.

---

15. Worked Examples

Subjects such as mathematics and science may require a dedicated worked-example component.

Example:

:::worked-example
### Adding Two Numbers

Calculate:

345 + 276

Step 1: Add the ones.

5 + 6 = 11

Step 2: Write 1 in the ones column and carry 1.

Step 3: Continue with the tens and hundreds.

**Answer: 621**
:::

---

16. Activities

Activities describe learner participation.

Example:

:::activity
### Activity: Build a Number

Work with a partner.

1. Choose a number between 1 000 and 9 999.
2. Write the number.
3. Identify the value of each digit.
4. Explain your answer to your partner.
:::

Activities may include:

- Individual work
- Pair work
- Group work
- Oral activities
- Practical activities
- Investigations
- Games
- Projects

---

17. Practice

Practice provides structured opportunities for learners to apply a skill.

Example:

:::practice
1. Write 4 305 in words.

2. What is the value of the 6 in 6 421?

3. Write the number represented by:

   3 thousands + 4 hundreds + 2 tens + 7 ones.
:::

Practice questions should have stable question IDs when they are part of the assessment/question bank system.

---

18. Challenge

Challenge activities provide additional or deeper application.

Example:

:::challenge
Can you find three different four-digit numbers
whose digits add up to 15?

Explain how you found them.
:::

Challenge content should not be required for understanding the core lesson unless explicitly identified as such.

---

19. Assessment

Assessment can appear at:

- Lesson level
- Unit level
- Term level
- Book level

Lesson assessment example:

assessment:
  enabled: true
  questions:
    - G4-MATH-Q001
    - G4-MATH-Q002

Questions themselves should normally be stored separately in the assessment/question bank.

This allows the same question to be reused in:

- Student books
- Workbooks
- Tests
- Answer keys
- Teacher guides
- Digital assessments

---

20. Question Bank Schema

Example:

id: G4-MATH-Q001

type: short_answer

grade: 4

subject: mathematics

curriculum:
  - MATH-G4-NUM-001

question: >
  What is the value of the digit 7 in 3 742?

answer:
  type: exact
  value: 700

difficulty: 1

marks: 1

---

21. Question Types

The core system should support:

multiple_choice
multiple_select
true_false
short_answer
numeric
matching
ordering
fill_blank
extended_response
problem_solving
practical
oral

Subject frameworks may add additional types.

---

22. Answers

Answers should be stored separately from student-facing content wherever practical.

Example:

answers/
├── unit-01.yml
├── unit-02.yml
└── final-assessment.yml

Example:

- question_id: G4-MATH-Q001
  answer: 700

- question_id: G4-MATH-Q002
  answer: 621

This allows the publishing engine to generate:

Student Book
        ↓
Questions

Answer Book
        ↓
Answers

without maintaining duplicate question content.

---

23. Mathematics Content

The mathematics framework should support specialized components.

Examples:

worked-example
calculation
number-line
place-value-table
problem
reasoning
mental-maths
practice
challenge

Mathematical expressions should use a machine-readable representation where appropriate.

Example:

3 × 25 = 75

The system should avoid storing mathematics only as images.

This allows future generation of:

- Accessible digital mathematics
- EPUB mathematics
- Interactive exercises
- Automatic answer checking
- Mathematical validation

---

24. Science Content

The science framework should support:

investigation
question
prediction
hypothesis
materials
method
observation
results
discussion
conclusion
safety

Example:

:::investigation
### Investigate: What Floats?

#### Question

Which objects float in water?

#### Prediction

Predict which objects will float before beginning.

#### Materials

- Bowl of water
- Small stone
- Leaf
- Plastic bottle cap

#### Method

Place each object in the water and observe what happens.

#### Results

Record your observations in a table.

#### Conclusion

What did you discover?
:::

---

25. English Content

The English framework should support:

reading
comprehension
vocabulary
grammar
spelling
speaking
listening
writing
phonics
literature
discussion

Example:

:::reading
### Reading

Read the passage carefully.

> [Reading passage]

#### Comprehension

1. Who is the main character?
2. Where does the story take place?
3. What happened first?
:::

---

26. Social Science Content

The social science framework may support:

case-study
map
timeline
source
discussion
community-activity
research
fieldwork
comparison
reflection

---

27. Tables

Tables should be represented as structured Markdown or structured data.

Example:

| Place | Value |
|---|---:|
| Thousands | 4 000 |
| Hundreds | 500 |
| Tens | 80 |
| Ones | 2 |

The publishing engine controls:

- Font
- Borders
- Alignment
- Width
- Page behaviour
- Accessibility

---

28. Figures and Illustrations

Images must be referenced rather than embedded directly into lesson text wherever practical.

Example:

:::figure
image: illustrations/place-value-chart.svg
caption: A place-value chart showing thousands, hundreds, tens and ones.
alt: Place-value chart with columns for thousands, hundreds, tens and ones.
:::

Each asset should have metadata.

Example:

id: FIG-G4-MATH-001

file: place-value-chart.svg

description: Place-value chart for numbers up to 10 000.

creator: Baimuru Primary School

source: original

license: Copyright

---

29. Accessibility

Content must contain enough information for accessible publishing.

Images should have:

alt text

Complex diagrams should additionally have:

long description

Tables should have meaningful headings.

Links should use descriptive text.

The content system should avoid conveying essential information through colour alone.

---

30. Curriculum Traceability

Every curriculum-aligned lesson should contain one or more curriculum IDs.

Example:

curriculum:
  - MATH-G4-NUM-001
  - MATH-G4-NUM-002

This creates a traceability chain:

Curriculum Outcome
       ↓
Unit
       ↓
Lesson
       ↓
Activity
       ↓
Assessment
       ↓
Question

This is a major feature of the platform.

The QA system should be able to identify:

- Curriculum outcomes with no lessons
- Lessons with no curriculum mapping
- Outcomes with insufficient assessment coverage
- Questions mapped to invalid curriculum IDs

---

31. Content IDs

Every major content object should have a stable unique ID.

Examples:

Book:
G4-MATH

Unit:
G4-MATH-U01

Lesson:
G4-MATH-L01

Question:
G4-MATH-Q001

Figure:
G4-MATH-F001

IDs should not normally change when wording is edited.

Changing an ID should be treated as a structural change.

---

32. Content Versioning

Content changes must be tracked through Git.

Examples of changes:

Added lesson
Changed learning objective
Corrected mathematical answer
Updated curriculum mapping
Replaced illustration
Added assessment question
Corrected factual error

The "CHANGELOG.md" file should record significant published-content changes.

---

33. Content Validation

The platform should automatically validate:

Structural

- Required metadata exists
- IDs are unique
- Unit references are valid
- Lesson references are valid
- Question IDs are valid

Curriculum

- Curriculum IDs exist
- Lessons have curriculum mappings
- Assessment questions have curriculum mappings where required

Content

- Required sections exist
- Empty lessons are detected
- Duplicate IDs are detected
- Missing answers are detected

Assets

- Referenced images exist
- Asset metadata exists
- Licensing information exists
- Missing alt text is detected

Assessment

- Questions have valid types
- Required answers exist
- Mark allocations are valid
- Multiple-choice questions contain valid options

---

34. Subject Extensions

The core schema must remain general.

Subject-specific features should be implemented through subject frameworks.

Example:

framework/
└── subjects/
    ├── mathematics/
    │   ├── components/
    │   ├── validators/
    │   └── schema.yml
    │
    ├── english/
    │   ├── components/
    │   ├── validators/
    │   └── schema.yml
    │
    └── science/
        ├── components/
        ├── validators/
        └── schema.yml

The core engine should not be modified every time a subject needs a new component.

---

35. Teacher Guide Reuse

The same master content should support teacher guides.

For example:

Student Lesson
      ↓
Teacher Guide Generator
      ↓
Teacher Notes
      ↓
Teaching Suggestions
      ↓
Answers
      ↓
Assessment Guidance

Teacher-specific information should be stored separately from student-facing content where appropriate.

---

36. Digital Publishing

The content schema must remain suitable for multiple output formats.

The same source should potentially generate:

PDF
EPUB
HTML
Website
Kolibri resource
LMS content
Interactive textbook

Therefore:

Do not write content that depends on a specific page number or physical layout.

Avoid:

"Look at the picture on the left side of this page."

Prefer:

"Look at the picture below."

when the content must work across multiple formats.

---

37. AI Content Generation

AI-generated content must follow the same schema as human-authored content.

AI must not create an alternative undocumented format.

The workflow should be:

Curriculum
    ↓
Content Specification
    ↓
AI Draft
    ↓
Human Review
    ↓
Structured Source
    ↓
Automated Validation
    ↓
Visual Review
    ↓
Publication

AI-generated material must be treated as a draft until reviewed.

---

38. Human Review

The author/editor should review:

- Curriculum alignment
- Accuracy
- Age appropriateness
- Language
- Cultural relevance
- Examples
- Activities
- Assessment quality
- Mathematical/scientific accuracy
- Illustrations
- Copyright and licensing
- Final page presentation

Automated QA does not replace human review.

---

39. Content Quality Rules

The platform should encourage content that is:

- Curriculum-aligned
- Age appropriate
- Clear
- Accurate
- Progressive
- Culturally appropriate
- Inclusive
- Practical
- Engaging
- Accessible
- Consistent

The platform should detect technical problems automatically, while the author remains responsible for editorial decisions.

---

40. Example Complete Lesson

---
id: G4-MATH-L01
title: Place Value
grade: 4
subject: mathematics
unit: G4-MATH-U01
sequence: 1

curriculum:
  - MATH-G4-NUM-001

objectives:
  - "Read and write numbers to 10 000."
  - "Identify the place value of digits."

vocabulary:
  - term: digit
    definition: A symbol used to write numbers.

  - term: place value
    definition: The value of a digit based on its position.

duration:
  minutes: 45
---

# Place Value

## Introduction

Numbers are made up of digits. The position of each digit
tells us its value.

## Teaching Content

Consider the number **4 582**.

| Thousands | Hundreds | Tens | Ones |
|---:|---:|---:|---:|
| 4 | 5 | 8 | 2 |

Therefore:

- 4 represents 4 000.
- 5 represents 500.
- 8 represents 80.
- 2 represents 2.

:::worked-example
### Example

What is the value of 7 in 3 742?

The 7 is in the hundreds place.

7 × 100 = 700

**Answer: 700**
:::

## Activity

:::activity
### Build a Number

Work with a partner.

1. Choose a four-digit number.
2. Write the number.
3. Identify the value of each digit.
4. Explain your answer.
:::

## Practice

1. What is the value of 6 in 6 421?

2. Write 4 305 in words.

3. Write the number represented by:

   3 thousands + 4 hundreds + 2 tens + 7 ones.

## Challenge

:::challenge
Find three different four-digit numbers whose digits
add up to 15. Explain how you found them.
:::

## Assessment

Answer the following questions.

1. What is the value of the digit 8 in 5 842?

2. Which digit is in the tens place in 7 326?

## Summary

A digit's place determines its value.

In a four-digit number, the places are:

**thousands → hundreds → tens → ones**

---

41. Future Extensions

The schema is intentionally extensible.

Future components may include:

audio
video
interactive
simulation
animation
QR-code
web-link
coding-exercise
drag-and-drop
self-check
flashcard
game
virtual-lab

These should extend the schema without breaking existing books.

---

42. Golden Rule

The textbook content repository is the master source.

PDF, EPUB, HTML and other published formats are generated products.

Therefore:

SOURCE CONTENT
      ↓
VALIDATION
      ↓
PUBLISHING ENGINE
      ↓
PDF / EPUB / HTML / OTHER OUTPUTS

Never make the PDF the master copy.

---

43. Definition of Done

The content schema is considered implemented when:

- Units can be defined using structured metadata.
- Lessons can be written using the standard lesson schema.
- Curriculum IDs can be attached to lessons.
- Reusable components can be rendered.
- Assessments can reference question-bank items.
- Answers can be generated from structured questions.
- Images can be referenced with metadata and accessibility information.
- Subject-specific components can extend the core system.
- Automated validation can detect structural errors.
- The same content can be used to generate multiple publication formats.

---

44. Relationship to Other Documents

This document works together with:

PROJECT_REQUIREMENTS.md
        ↓
ARCHITECTURE.md
        ↓
BOOK_SCHEMA.md
        ↓
PUBLICATION_SCHEMA.md
        ↓
CONTENT_SCHEMA.md
        ↓
DESIGN_SYSTEM.md
        ↓
QA_SPECIFICATION.md

The next implementation documents should define the book configuration schema, publication metadata schema, design system, and QA specification before Claude Code begins implementing the publishing engine.
