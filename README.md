PNG Textbook Production Platform

PTPP

A reusable AI-assisted platform for planning, writing, designing, validating, producing, and publishing primary-school textbooks and related educational resources.

---

1. What This Project Is

The PNG Textbook Production Platform (PTPP) is being developed as a textbook production system, not as a one-off book project.

The platform is designed to make it possible to create multiple educational publications using the same underlying publishing framework.

It will support:

- Primary-school textbooks
- Workbooks
- Activity books
- Revision books
- Teacher guides
- Answer books
- Assessment books
- Digital editions

The initial focus is Papua New Guinea primary education.

---

2. Core Idea

The platform separates:

CONTENT
+
PUBLISHING
+
QUALITY ASSURANCE

Educational content is stored as structured source material.

The publishing engine transforms that source into finished publications.

Curriculum
    ↓
Structured Content
    ↓
Assets
    ↓
Publishing Engine
    ↓
QA
    ↓
PDF / EPUB / HTML / Digital Products

---

3. The Most Important Principle

«Do not design the platform around one textbook. Design the textbook around the platform.»

A new textbook should primarily require:

Book Configuration
+
Curriculum
+
Content
+
Assets

rather than new programming.

---

4. AI-Assisted Production Workflow

The project uses a workflow similar to modern software development.

ChatGPT

Used primarily for:

- planning
- reasoning
- architecture
- curriculum analysis
- content planning
- specifications
- design decisions
- review
- QA analysis
- problem solving

Claude Code

Used primarily as the production/implementation agent for:

- inspecting the repository
- creating and editing files
- implementing the publishing engine
- writing scripts
- building publications
- running tests
- running QA
- fixing implementation issues
- reporting results

GitHub

GitHub is the project source of truth.

It stores:

- source code
- textbook content
- configuration
- schemas
- assets
- tests
- documentation
- QA rules
- build scripts

---

5. How the System Works

The intended production pipeline is:

PLAN
  ↓
CURRICULUM
  ↓
CONTENT
  ↓
ASSETS
  ↓
DESIGN
  ↓
BUILD
  ↓
AUTOMATED QA
  ↓
VISUAL QA
  ↓
HUMAN REVIEW
  ↓
RELEASE

The process is iterative.

Draft
 ↓
Validate
 ↓
Build
 ↓
Review
 ↓
Revise
 ↓
Validate
 ↓
Build
 ↓
Release

---

6. Repository Structure

The repository is organized approximately as follows:

png-textbook-platform/
│
├── framework/
│   ├── components/
│   ├── subjects/
│   ├── themes/
│   └── templates/
│
├── books/
│   └── grade-X/
│       └── subject/
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

The exact implementation may evolve, but the separation of responsibilities must remain.

---

7. Platform Layers

The architecture consists of eight major layers.

1. Book Configuration
2. Curriculum
3. Content
4. Subject Framework
5. Assets
6. Publishing Engine
7. Quality Assurance
8. Output and Release

Book Configuration

Defines:

- title
- grade
- subject
- language
- curriculum
- book type
- products
- outputs
- QA settings

Curriculum

Defines curriculum requirements and stable curriculum IDs.

Content

Contains:

- units
- lessons
- activities
- examples
- exercises
- assessments
- questions
- answers

Subject Framework

Provides subject-specific structures and components.

Initial subjects:

- Mathematics
- English
- Science
- Social Science

Assets

Contains:

- illustrations
- diagrams
- charts
- maps
- photographs
- icons

Publishing Engine

Transforms structured source content into publications.

QA

Validates the source and generated outputs.

Output

Produces:

- PDF
- EPUB
- HTML
- future digital formats

---

8. Book Architecture

Each textbook follows:

Grade
  ↓
Subject
  ↓
Book

Example:

books/
└── grade-4/
    └── mathematics/
        └── book.yml

Another book can therefore be:

books/
└── grade-6/
    └── science/
        └── book.yml

The same publishing engine can produce both.

---

9. Book Configuration

Each book has a central "book.yml".

Example:

book:
  id: grade-4-mathematics
  title: "Grade 4 Mathematics"
  grade: 4
  subject: mathematics
  language: en
  curriculum:
    id: png
    version: "2026"

publication:
  author:
    name: "[Author]"
  publisher:
    name: "[Publisher]"
    location: "Papua New Guinea"
  copyright:
    holder: "[Copyright Holder]"
    year: 2026
    license: "Copyright"
    rights: "All rights reserved."

design:
  theme: primary
  page_size: A4

output:
  pdf: true
  epub: true

The full configuration contract is defined in:

"BOOK_SCHEMA.md"

---

10. Content Model

Textbook content is structured.

Typical hierarchy:

Book
├── Front Matter
├── Unit
│   ├── Unit Overview
│   ├── Lesson
│   │   ├── Objectives
│   │   ├── Vocabulary
│   │   ├── Teaching Content
│   │   ├── Examples
│   │   ├── Activities
│   │   ├── Practice
│   │   ├── Challenge
│   │   ├── Assessment
│   │   └── Summary
│   └── Unit Assessment
├── Revision
├── Glossary
├── References
└── Answers

Content structure is defined in:

"CONTENT_SCHEMA.md"

---

11. Curriculum Traceability

Curriculum alignment is built into the content model.

The intended relationship is:

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

Stable curriculum IDs make this traceable.

Example:

MATH-G4-NUM-001

The platform should be able to produce curriculum coverage reports.

---

12. Publication Information

Publication metadata is separated from educational content.

A book may contain:

publication/
├── author.yml
├── publisher.yml
├── copyright.yml
├── edition.yml
├── credits.yml
└── acknowledgements.md

The initial copyright model is:

Copyright
All rights reserved.

The author and copyright holder are supplied through book metadata rather than hard-coded into the platform.

Publication rules are defined in:

"PUBLICATION_SCHEMA.md"

---

13. Design System

The platform uses a centralized design system.

The initial theme is:

primary

The initial default page size is:

A4 Portrait

Design controls include:

- typography
- spacing
- colours
- headings
- activities
- examples
- tables
- figures
- captions
- headers
- footers
- page numbering
- covers
- accessibility

Design rules are defined in:

"DESIGN_SYSTEM.md"

---

14. Subject Frameworks

Different subjects can use specialized components.

Mathematics

Examples:

Worked Example
Calculation
Number Line
Place Value Table
Problem Solving
Reasoning
Mental Mathematics
Challenge

Science

Examples:

Investigation
Question
Prediction
Materials
Method
Observation
Results
Discussion
Conclusion
Safety

English

Examples:

Reading
Comprehension
Vocabulary
Grammar
Spelling
Speaking
Listening
Writing
Phonics
Literature

Social Science

Examples:

Case Study
Map
Timeline
Source
Discussion
Community Activity
Research
Fieldwork
Comparison
Reflection

---

15. Assessment System

Assessment questions are stored as structured data.

This allows the platform to generate multiple products from the same question bank.

Question Bank
      │
      ├── Student Book
      ├── Workbook
      ├── Assessment
      ├── Answer Book
      ├── Teacher Guide
      └── Digital Quiz

Questions should have stable IDs and curriculum mappings.

---

16. Quality Assurance

QA is a built-in part of the publishing process.

The platform checks:

- configuration
- schemas
- IDs
- curriculum mappings
- lesson structure
- assessments
- mathematics
- assets
- asset licensing
- publication metadata
- accessibility
- PDF
- EPUB
- cross-references
- numbering
- visual layout

QA rules are defined in:

"QA_SPECIFICATION.md"

---

17. Human Review

Automated QA does not replace human review.

Human review remains necessary for:

- curriculum interpretation
- factual accuracy
- educational quality
- language
- cultural appropriateness
- illustrations
- sensitive content
- publication rights
- final visual quality

AI-generated content must be reviewed before publication.

---

18. Versioning

Git is used for project version control.

Example development progression:

v0.1  Prototype
v0.5  Pilot
v0.9  Pre-release
v1.0  Published

Technical source versions and publication editions are separate.

For example:

Source version:
v0.9.14

Publication:
1st Edition

---

19. Git Branching

"main" should contain the stable project.

Branches may be used for:

feature/*
fix/*
experiment/*

Grades and subjects should normally remain content/configuration rather than branches.

---

20. Working With Claude Code

Claude Code should begin by reading:

README.md
PROJECT_REQUIREMENTS.md
ARCHITECTURE.md
DECISIONS.md

It should then read the relevant specifications before modifying a subsystem.

For example:

Content work

Read:

CONTENT_SCHEMA.md
BOOK_SCHEMA.md

Design work

Read:

DESIGN_SYSTEM.md
ARCHITECTURE.md

QA work

Read:

QA_SPECIFICATION.md

Publication work

Read:

PUBLICATION_SCHEMA.md

---

21. Claude Code Operating Principles

Claude Code should:

1. Inspect the existing repository.
2. Read relevant documentation.
3. Understand existing architecture.
4. Avoid unnecessary redesign.
5. Make changes in small logical steps.
6. Test changes.
7. Run QA.
8. Document important changes.
9. Report unresolved issues.
10. Never silently override architectural decisions.

If a proposed implementation conflicts with "DECISIONS.md", the conflict should be identified before changing the architecture.

---

22. Development Philosophy

This project uses an iterative engineering approach.

Do not attempt to build the entire platform at once.

The preferred approach is:

Design
 ↓
Implement small component
 ↓
Test
 ↓
Use it
 ↓
Identify problems
 ↓
Improve
 ↓
Expand

---

23. Initial Development Roadmap

Phase 1 — Foundation

Build:

- repository structure
- configuration system
- book schema
- publication metadata
- documentation framework

Phase 2 — Content

Build:

- curriculum schema
- lesson schema
- unit schema
- components
- assessment schema
- answer system

Phase 3 — Rendering

Build:

- design system
- templates
- PDF renderer
- EPUB renderer
- metadata generation

Phase 4 — QA

Build:

- source validation
- curriculum validation
- assessment validation
- asset validation
- output validation
- QA reporting

Phase 5 — Prototype

Produce a complete textbook unit.

The prototype should exercise the complete pipeline.

Phase 6 — Refinement

Identify weaknesses and improve the platform.

Phase 7 — Scaling

Add:

- additional subjects
- additional grades
- additional products
- digital outputs
- advanced AI features

---

24. Future Direction

The platform is intentionally designed to grow beyond printed textbooks.

Potential future outputs include:

PDF
EPUB
HTML
Interactive Web Textbook
Kolibri Resources
LMS Content
Digital Assessments
Teacher Resources

Potential future AI features include:

AI Lesson Planner
AI Question Generator
AI Assessment Generator
AI Curriculum Mapping Assistant
AI Differentiation Assistant
AI Translation Assistant
AI Content Reviewer

These features should build on the structured content system rather than bypass it.

---

25. Golden Rules

The following rules apply to the project.

Rule 1

«Source content is the master.»

Rule 2

«Do not design the platform around one textbook.»

Rule 3

«Grades and subjects are content/configuration, not normally Git branches.»

Rule 4

«Separate content from design.»

Rule 5

«Use structured content wherever possible.»

Rule 6

«Use stable IDs for important entities.»

Rule 7

«Curriculum traceability is fundamental.»

Rule 8

«AI-generated content is draft until reviewed.»

Rule 9

«QA is part of the build process.»

Rule 10

«Human review is required before publication.»

Rule 11

«Never invent publication identifiers such as ISBNs.»

Rule 12

«Do not silently override established architectural decisions.»

---

26. Current Project State

The platform specifications currently define:

✓ Project requirements
✓ Architecture
✓ Content schema
✓ Book schema
✓ Publication schema
✓ Design system
✓ QA specification
✓ Architectural decisions

The next stage is implementation.

---

27. Important Documents

Document| Purpose
"README.md"| Project entry point
"PROJECT_REQUIREMENTS.md"| What the platform must do
"ARCHITECTURE.md"| How the platform is structured
"DECISIONS.md"| Why important decisions were made
"CONTENT_SCHEMA.md"| How textbook content is structured
"BOOK_SCHEMA.md"| How books are configured
"PUBLICATION_SCHEMA.md"| Publication metadata
"DESIGN_SYSTEM.md"| Visual design rules
"QA_SPECIFICATION.md"| Quality-control rules
"CHANGELOG.md"| Implementation history
"REVIEW.md"| Review findings
"handover.md"| AI-agent handover instructions

---

28. Final Objective

The ultimate objective is to create a system where producing a new textbook becomes a structured production process rather than starting from scratch every time.

Conceptually:

                 PTPP
                  │
       ┌──────────┴──────────┐
       │                     │
   CONTENT                 ENGINE
       │                     │
 Curriculum             Components
 Lessons                Themes
 Activities             Templates
 Assessments            Rendering
 Questions              QA
 Assets                 Outputs
       │                     │
       └──────────┬──────────┘
                  │
                  ▼
             PUBLICATIONS
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
   Textbook   Workbook   Teacher Guide
       │
       ├── EPUB
       ├── HTML
       ├── Kolibri
       └── Future Digital Products

The platform should ultimately make high-quality educational publishing faster, more systematic, more reusable, and easier to maintain while keeping the author and human reviewers in control.
