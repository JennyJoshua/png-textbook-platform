Handover — PNG Textbook Production Platform

Project

PNG Textbook Production Platform (PTPP)

Repository: "png-textbook-platform"

---

1. Purpose of This Handover

This document instructs the implementation agent to begin building the platform described in the project specifications.

The platform is intended to become a reusable system for producing primary-school textbooks and related educational publications.

The implementation must follow the existing project architecture and decisions.

Do not redesign the project from scratch.

---

2. Read These Documents First

Before modifying or creating implementation files, read:

README.md
PROJECT_REQUIREMENTS.md
ARCHITECTURE.md
DECISIONS.md
CONTENT_SCHEMA.md
BOOK_SCHEMA.md
PUBLICATION_SCHEMA.md
DESIGN_SYSTEM.md
QA_SPECIFICATION.md

These documents define the current project requirements and architectural decisions.

If there is a conflict between an implementation idea and an established decision, identify the conflict rather than silently changing the architecture.

---

3. Implementation Philosophy

Build the platform incrementally.

Do NOT attempt to implement:

- every subject
- every output format
- advanced AI functionality
- advanced visual QA
- LMS integration
- Kolibri integration
- interactive textbooks

during the first implementation stage.

The first objective is to prove the fundamental pipeline:

Book Configuration
        ↓
Structured Content
        ↓
Validation
        ↓
Rendering
        ↓
PDF
        ↓
QA Report

Once this works reliably, expand the system.

---

4. Initial Prototype

Create a small but complete demonstration textbook.

Recommended prototype:

Grade 4 Mathematics

The prototype does not need to be a complete year's textbook.

It should contain enough content to exercise the platform.

Recommended structure:

Grade 4 Mathematics
│
├── Unit 1
│   ├── Lesson 1
│   ├── Lesson 2
│   ├── Lesson 3
│   └── Unit Assessment
│
└── Answers

The actual educational content can initially be simple demonstration content.

Do not spend the first implementation stage attempting to write the entire textbook.

---

5. Implementation Phase 1 — Repository Foundation

Create the basic repository structure.

png-textbook-platform/
│
├── framework/
│   ├── components/
│   ├── subjects/
│   ├── themes/
│   └── templates/
│
├── books/
│   └── grade-4/
│       └── mathematics/
│           ├── book.yml
│           ├── publication/
│           ├── curriculum/
│           ├── units/
│           ├── assessments/
│           ├── answers/
│           ├── illustrations/
│           └── references/
│
├── assets/
│
├── scripts/
│
├── tests/
│
├── output/
│
├── releases/
│
├── docs/
│
├── README.md
├── PROJECT_REQUIREMENTS.md
├── ARCHITECTURE.md
├── DECISIONS.md
├── DESIGN_SYSTEM.md
├── CONTENT_SCHEMA.md
├── BOOK_SCHEMA.md
├── PUBLICATION_SCHEMA.md
├── QA_SPECIFICATION.md
├── CHANGELOG.md
├── REVIEW.md
└── handover.md

Do not create unnecessary directories merely for future possibilities.

---

6. Phase 2 — Choose the Initial Technology

Before implementation, inspect the available development environment.

Determine:

- Python version
- available package manager
- PDF generation options
- EPUB generation options
- YAML parser
- Markdown parser
- testing framework
- image-processing libraries

Prefer mature, open-source tools.

Avoid introducing a large dependency stack unnecessarily.

Document the selected technologies and reasons in "DECISIONS.md" or an implementation document.

---

7. Phase 3 — Implement Book Configuration

Implement loading and validation of:

book.yml

The system must initially understand:

book:
  id:
  title:
  grade:
  subject:
  language:
  curriculum:

publication:
  author:
  publisher:
  copyright:

design:
  theme:
  page_size:

output:
  pdf:
  epub:

products:
  student_book:
  teacher_guide:
  workbook:

The implementation must reject malformed configuration.

---

8. Phase 4 — Implement Publication Metadata

Implement the publication metadata layer.

Support:

publication/
├── author.yml
├── publisher.yml
├── copyright.yml
├── edition.yml
├── credits.yml
└── acknowledgements.md

The engine should be able to read this information and use it when generating publication front matter.

Initial copyright:

license: "Copyright"
rights: "All rights reserved."

Do not hard-code a particular author's personal information into the publishing engine.

---

9. Phase 5 — Implement Curriculum Model

Create a minimal curriculum structure.

Example:

curriculum/
├── curriculum.yml
└── mapping.yml

Use stable IDs.

Example:

MATH-G4-NUM-001

The first prototype only needs a small representative curriculum dataset.

The implementation must prove that lessons can reference curriculum IDs.

---

10. Phase 6 — Implement Content Model

Implement support for:

units/
└── unit-01/
    ├── unit.yml
    ├── lesson-01.md
    ├── lesson-02.md
    ├── lesson-03.md
    └── assessment.yml

Lessons should support YAML front matter.

Example:

---
id: G4-MATH-L01
title: Place Value
grade: 4
subject: mathematics
unit: UNIT-01
sequence: 1

curriculum:
  - MATH-G4-NUM-001

objectives:
  - "Read and write numbers to 10 000"
  - "Identify the place value of digits"
---

The Markdown body contains the actual lesson content.

---

11. Phase 7 — Implement Core Components

Initially implement only the components necessary for the prototype.

Recommended first components:

lesson
objectives
vocabulary
example
worked-example
activity
practice
challenge
assessment
summary
figure
table

Do not implement every future component immediately.

The component architecture must allow additional components to be added later.

---

12. Phase 8 — Implement Mathematics Components

Implement a small mathematics-specific component set.

Initial components:

worked-example
calculation
problem
reasoning
practice
challenge

These should extend the general component system rather than create a separate rendering engine.

---

13. Phase 9 — Implement Basic Theme

Implement the initial:

primary

theme.

The theme should define:

- A4 page
- margins
- typography
- headings
- body text
- activity styling
- examples
- tables
- figures
- headers
- footers
- page numbering

Keep the initial design simple.

The objective is to prove the rendering architecture, not create the final commercial textbook design.

---

14. Phase 10 — Implement PDF Rendering

The first major milestone is:

«Generate a readable PDF from structured textbook source.»

The build should combine:

book.yml
+
publication metadata
+
curriculum
+
lesson Markdown
+
components
+
theme
+
assets

and produce:

output/
└── grade-4-mathematics/
    └── pdf/
        └── grade-4-mathematics.pdf

---

15. Required Front Matter

The generated PDF should initially contain:

Cover
Title Page
Publication Information
Copyright Page
Table of Contents

followed by:

Unit
Lessons
Assessment
Answers

The exact front-matter implementation can evolve.

---

16. Phase 11 — Implement Assessment Data

Create a small structured question bank.

Example:

questions:
  - id: Q-G4-MATH-001
    type: numeric
    curriculum:
      - MATH-G4-NUM-001
    question: "What is 24 × 6?"
    answer: 144
    marks: 1

The system must validate the structure.

---

17. Phase 12 — Implement Answer Generation

The platform should use the master assessment data to generate the answer section.

Do not manually duplicate the answer in another source file unless there is a clear reason.

The goal is:

Question Data
      ↓
Student Question
      +
Answer Key
      +
Teacher Resource

---

18. Phase 13 — Implement Basic QA

Create the first QA system.

At minimum it must detect:

Missing book.yml
Invalid YAML
Missing required fields
Duplicate IDs
Missing curriculum references
Missing lesson IDs
Missing lesson titles
Missing objectives
Missing content
Missing assessment answers
Missing assets
Broken asset references

The system should return:

PASS
WARNING
ERROR

---

19. Phase 14 — Implement Mathematics Answer Checking

Implement a basic mechanism for validating simple numeric questions.

For example:

24 × 6

must validate against:

144

The implementation should be conservative.

Do not attempt to build a full mathematical theorem prover during the first phase.

---

20. Phase 15 — Implement QA Report

Generate both:

qa-report.json

and:

qa-report.md

Example:

QA REPORT

Book:
Grade 4 Mathematics

Status:
PASS

Errors:
0

Warnings:
2

Checks:
✓ Configuration
✓ Curriculum
✓ Content
✓ Assessments
✓ Assets
✓ Publication
✓ PDF

---

21. Phase 16 — Automated Tests

Create tests for the platform itself.

At minimum test:

Configuration

- valid configuration
- missing configuration
- invalid configuration

Content

- valid lesson
- missing lesson ID
- missing title
- invalid curriculum reference

Assessment

- valid question
- invalid answer
- missing answer
- invalid question type

Assets

- valid asset
- missing asset

Rendering

- PDF successfully generated

QA

- errors correctly detected
- warnings correctly detected
- report generated

---

22. Phase 17 — Build Command

Create one primary command that can eventually perform the complete build.

For example:

python scripts/build.py books/grade-4/mathematics

The exact command is an implementation decision.

The command should eventually:

Load
 ↓
Validate
 ↓
Build
 ↓
Generate PDF
 ↓
Run QA
 ↓
Generate report

---

23. Phase 18 — Separate Validation from Rendering

Do not put all logic into one large script.

Prefer modular architecture.

Conceptually:

scripts/
├── build.py
├── validate.py
├── qa.py
└── visual_qa.py

And internally:

framework/
├── config/
├── content/
├── curriculum/
├── publication/
├── rendering/
├── assessment/
└── qa/

Exact implementation may differ.

---

24. Phase 19 — Visual QA

Do not attempt sophisticated AI visual analysis initially.

First make it possible to:

1. Generate PDF.
2. Render PDF pages to images.
3. Produce a contact sheet.
4. Inspect pages manually.
5. Record visual issues.

Automated visual anomaly detection can be added later.

---

25. Phase 20 — Prototype Completion

The first implementation milestone is achieved when the following works:

book.yml
   ↓
Curriculum
   ↓
Unit
   ↓
Lessons
   ↓
Assessment
   ↓
Publication Metadata
   ↓
Theme
   ↓
Build
   ↓
PDF
   ↓
QA Report

The generated PDF should look like a basic but coherent textbook rather than a collection of raw Markdown pages.

---

26. Definition of Done — Phase 1

Phase 1 is complete when:

- [ ] Repository structure exists
- [ ] Book configuration loads
- [ ] Publication metadata loads
- [ ] Curriculum loads
- [ ] Lessons load
- [ ] Components render
- [ ] Assessment data loads
- [ ] Answers can be generated
- [ ] Assets resolve
- [ ] PDF can be generated
- [ ] Basic QA runs
- [ ] QA report is generated
- [ ] Automated tests pass
- [ ] Prototype book builds successfully

---

27. What NOT to Build Yet

Do not spend significant time initially on:

AI writing automation
AI lesson planning
AI image generation
LMS integration
Kolibri integration
Interactive textbooks
Mobile applications
Cloud publishing
User accounts
Web dashboards
Advanced visual AI
Automated translation
Advanced analytics

These belong to later phases.

The foundation must work first.

---

28. Important Architecture Rule

Do not solve a content problem by modifying the publishing engine unnecessarily.

For example:

If a Grade 4 Mathematics lesson needs different content, modify the lesson.

If Mathematics needs a specialized component, extend the Mathematics framework.

Only modify the core engine when the capability genuinely belongs to the platform.

---

29. Important AI-Agent Rule

Do not assume that a feature is required merely because it appears in a future-looking specification.

Implement the current milestone first.

If a requirement is unclear:

1. inspect existing documentation
2. inspect existing code
3. determine whether the decision is already recorded
4. if genuinely ambiguous, document the ambiguity rather than inventing a major architectural decision

---

30. Change Management

After implementation:

Update:

CHANGELOG.md

with significant changes.

Update:

REVIEW.md

with:

- what was tested
- what worked
- what failed
- known limitations
- recommended next steps

If an architectural decision changes, update:

DECISIONS.md

---

31. Required Final Report From Claude Code

When the implementation milestone is complete, report:

1. What was built

List major components.

2. Files created

List important files.

3. Files modified

List important changes.

4. Technology choices

Explain the selected tools/libraries briefly.

5. Tests

Report:

Tests run:
Passed:
Failed:

6. Prototype Build

Report:

PDF:
Generated / Failed

Pages:
...

QA:
Passed / Failed / Warnings

7. Known Problems

List unresolved issues.

8. Recommended Next Step

Recommend the next implementation phase without silently starting unrelated work.

---

32. Final Instruction

Build the platform incrementally.

Do not replace the architecture with a simpler one-off textbook generator.

Do not create a textbook-specific system disguised as a platform.

The goal is a reusable publishing engine.

The first prototype is evidence that the architecture works.

---

33. Core Objective

The finished system should eventually make this possible:

Create New Book
       ↓
Select Grade
       ↓
Select Subject
       ↓
Supply Curriculum
       ↓
Write/Import Structured Content
       ↓
Add Assets
       ↓
Configure Publication
       ↓
Build
       ↓
QA
       ↓
Human Review
       ↓
Publish

without rebuilding the publishing system for every new textbook.

---

34. Final Principle

«Build the publishing machine first. Then use the machine to produce the books.»
