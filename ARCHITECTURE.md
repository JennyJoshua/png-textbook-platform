PNG Textbook Production Platform

System Architecture

Project: PNG Textbook Production Platform
Repository: "png-textbook-platform"
Document: "ARCHITECTURE.md"
Version: 0.1
Status: Initial Architecture

---

1. Architecture Overview

The platform is designed as a reusable textbook publishing engine.

Its architecture separates:

Platform Engine
      ↓
Subject Framework
      ↓
Book Configuration
      ↓
Curriculum
      ↓
Structured Content
      ↓
Assets
      ↓
Build System
      ↓
Quality Assurance
      ↓
Published Outputs

The platform must allow multiple books to use the same underlying engine.

---

2. Architectural Layers

The system consists of eight primary layers.

┌──────────────────────────────────────┐
│  1. BOOK CONFIGURATION               │
├──────────────────────────────────────┤
│  2. CURRICULUM                       │
├──────────────────────────────────────┤
│  3. CONTENT                          │
├──────────────────────────────────────┤
│  4. SUBJECT FRAMEWORK                │
├──────────────────────────────────────┤
│  5. ASSETS                           │
├──────────────────────────────────────┤
│  6. PUBLISHING ENGINE                │
├──────────────────────────────────────┤
│  7. QUALITY ASSURANCE                │
├──────────────────────────────────────┤
│  8. OUTPUT / RELEASE                 │
└──────────────────────────────────────┘

---

3. Book Configuration Layer

Every book shall have a central configuration file:

book.yml

This identifies the book and controls the build.

Example:

book:
  id: grade-4-mathematics
  title: "Grade 4 Mathematics"
  grade: 4
  subject: mathematics
  language: en
  curriculum: png

publication:
  author:
    name: "[Author]"
    role: "Author"

  publisher:
    name: "[Publisher]"
    location: "Papua New Guinea"

  copyright:
    holder: "[Copyright Holder]"
    year: 2026
    license: "Copyright"
    rights: "All rights reserved."

  edition:
    number: 1

design:
  theme: primary
  page_size: A4

output:
  pdf: true
  epub: true

products:
  student_book: true
  teacher_guide: false
  workbook: false

The configuration shall not contain the actual textbook content.

---

4. Publication Metadata Architecture

Publication metadata is treated as structured data.

publication/
├── author.yml
├── publisher.yml
├── copyright.yml
├── acknowledgements.md
└── credits.yml

The build engine combines these with "book.yml".

Publication information shall automatically populate:

- Cover
- Title page
- Copyright page
- Acknowledgements
- Credits
- PDF metadata
- EPUB metadata

---

5. Curriculum Layer

Curriculum information shall be stored separately from textbook prose.

Example:

curriculum/
├── curriculum.yml
├── strands/
├── outcomes/
└── mapping.yml

A curriculum item should have a stable identifier.

Example:

id: MATH-G4-NUM-001
grade: 4
subject: mathematics
strand: Number
outcome: "..."

Lessons can reference this identifier.

Example:

curriculum:
  - MATH-G4-NUM-001

This creates curriculum traceability.

---

6. Content Layer

Content shall be stored in structured, human-readable files.

The initial preferred format is Markdown with structured metadata.

Example:

units/
├── unit-01/
│   ├── unit.yml
│   ├── lesson-01.md
│   ├── lesson-02.md
│   ├── lesson-03.md
│   └── ...
│
└── unit-02/

Markdown is preferred because it is:

- Human-readable
- Git-friendly
- Easy for AI agents to modify
- Easy to convert
- Portable
- Easy to review

Structured metadata can be supplied through YAML front matter.

Example:

---
id: G4-MATH-L01
title: Place Value
grade: 4
subject: mathematics

curriculum:
  - MATH-G4-NUM-001

objectives:
  - "Read and write numbers to 10 000"
  - "Identify the place value of digits"
---

The lesson body follows the metadata.

---

7. Lesson Component Architecture

Lessons should be constructed from reusable components.

Conceptually:

Lesson
├── Metadata
├── Objectives
├── Vocabulary
├── Introduction
├── Explanation
├── Example
├── Activity
├── Practice
├── Challenge
├── Assessment
└── Summary

The renderer converts these components into the appropriate visual layout.

---

8. Component System

The publishing engine shall contain reusable components.

Example:

framework/components/
├── cover/
├── title-page/
├── copyright-page/
├── unit/
├── lesson/
├── objectives/
├── vocabulary/
├── example/
├── activity/
├── exercise/
├── assessment/
├── summary/
├── table/
├── figure/
└── callout/

A component should have:

Input
 ↓
Validation
 ↓
Rendering
 ↓
Output

---

9. Subject Framework Architecture

Subject-specific logic shall be separate from the core engine.

framework/
└── subjects/
    ├── mathematics/
    ├── english/
    ├── science/
    └── social-science/

Each subject may define:

- Components
- Content rules
- Validation rules
- Terminology
- Assessment structures
- Specialized rendering

The subject framework must extend the core engine rather than duplicate it.

---

10. Grade Architecture

Grades shall primarily be represented through book configuration and curriculum data.

The platform should not create a separate publishing engine for each grade.

Example:

books/
├── grade-3/
├── grade-4/
├── grade-5/
└── grade-6/

Each book selects the relevant:

Grade
+
Subject
+
Curriculum
+
Theme

---

11. Asset Architecture

Assets shall be separated from content.

illustrations/
├── diagrams/
├── generated/
├── photographs/
├── charts/
└── maps/

Each asset should have a meaningful filename.

Example:

place-value-chart.svg
multiplication-groups.png
water-cycle-diagram.svg

Where appropriate, asset metadata should record:

- Creator
- Source
- License
- Attribution
- Description

---

12. Illustration Pipeline

The platform should support multiple illustration sources.

AI Generated
      │
Original Artwork
      │
Open Licensed Resource
      │
Photograph
      │
Programmatically Generated Diagram
      ↓
     ASSET
      ↓
Metadata
      ↓
Validation
      ↓
Book

AI-generated assets should not automatically be assumed to be suitable for publication.

They must undergo human review.

---

13. Design System Architecture

Design is centralized.

framework/
└── themes/
    └── primary/
        ├── typography/
        ├── colors/
        ├── spacing/
        ├── page-layout/
        └── components/

A book selects a theme:

design:
  theme: primary

The theme controls visual presentation without changing the content.

---

14. Rendering Architecture

The rendering system converts structured source material into publication formats.

Markdown
+
YAML metadata
+
Book configuration
+
Templates
+
Design system
+
Assets
      ↓
  RENDER ENGINE
      ↓
 ┌────┴────┐
 ↓         ↓
PDF       EPUB

The architecture should keep the rendering layer independent from the content layer.

---

15. Build Pipeline

The build system should operate in stages.

1. Load configuration
        ↓
2. Load curriculum
        ↓
3. Load content
        ↓
4. Load publication metadata
        ↓
5. Validate source
        ↓
6. Resolve assets
        ↓
7. Render components
        ↓
8. Assemble publication
        ↓
9. Generate PDF
        ↓
10. Generate EPUB
        ↓
11. Run output validation
        ↓
12. Generate QA report

---

16. Validation Architecture

Validation should happen at multiple levels.

SOURCE VALIDATION
       ↓
CONTENT VALIDATION
       ↓
CURRICULUM VALIDATION
       ↓
ASSET VALIDATION
       ↓
BUILD VALIDATION
       ↓
OUTPUT VALIDATION
       ↓
VISUAL QA

A build should fail when critical errors are detected.

Warnings should be distinguished from errors.

---

17. Content Validation

The validator should check for:

- Missing required metadata
- Missing title
- Missing lesson ID
- Missing objectives
- Invalid curriculum references
- Duplicate IDs
- Duplicate lesson numbers
- Missing answers
- Missing assets
- Broken asset references
- Invalid component usage

---

18. Curriculum Validation

The system should be able to report:

Covered outcomes
Uncovered outcomes
Partially covered outcomes
Lessons associated with each outcome
Assessments associated with each outcome

Example report:

Curriculum Coverage Report

MATH-G4-NUM-001
✓ Lessons 1, 2, 4
✓ Assessment Questions 1–5

MATH-G4-NUM-002
✓ Lessons 5–7
⚠ No assessment mapped

---

19. Subject-Specific Validation

The architecture shall permit validators to be registered by subject.

Example:

Mathematics
→ calculation validator

English
→ vocabulary/grammar checks

Science
→ terminology/experiment structure checks

These validators should not contaminate the core publishing engine.

---

20. Assessment Architecture

Questions should be structured data wherever practical.

Example:

id: G4-MATH-Q001
type: multiple-choice
curriculum:
  - MATH-G4-NUM-001

question: "..."

options:
  - A
  - B
  - C
  - D

answer: B

This allows the same assessment data to generate:

- Student questions
- Answer keys
- Teacher guides
- Assessment reports
- Potential future digital quizzes

---

21. Answer Architecture

Answers shall preferably be stored as structured data rather than manually duplicated.

Conceptually:

Question Bank
      ↓
Student Book
      +
Answer Key
      +
Teacher Guide

This reduces inconsistencies.

---

22. Teacher Guide Architecture

Teacher guides should reuse the same underlying content.

Master Content
      │
 ┌────┴─────┐
 ↓          ↓
Student    Teacher
Book       Guide

Teacher-specific material may include:

- Teaching notes
- Suggested activities
- Answers
- Misconceptions
- Differentiation
- Extension
- Remediation
- Assessment guidance

---

23. Output Architecture

Build outputs should be separated from source.

output/
├── grade-4-mathematics/
│   ├── pdf/
│   ├── epub/
│   ├── previews/
│   └── qa/

Generated files should not be treated as source files.

---

24. Release Architecture

Published editions should be immutable once released.

Example:

releases/
└── grade-4-mathematics/
    ├── v1.0/
    │   ├── Grade4-Mathematics.pdf
    │   ├── Grade4-Mathematics.epub
    │   └── release-notes.md
    │
    └── v1.1/

---

25. Git Architecture

"main" represents the stable project.

Feature branches should be used for development.

Examples:

main

feature/pdf-renderer
feature/epub-export
feature/math-validator
feature/teacher-guide
fix/page-overflow

Grades and subjects shall not normally be represented as branches.

They are products/content configurations within the repository.

---

26. AI Agent Architecture

AI agents interact with the repository through documented project rules.

The operating model is:

Human
  ↓
ChatGPT
  ↓
Specifications / Decisions
  ↓
GitHub
  ↓
Claude Code
  ↓
Implementation
  ↓
Tests
  ↓
Build
  ↓
Review

Claude Code shall inspect the repository before modifying it.

---

27. Documentation Architecture

The project shall maintain:

README.md

Public overview and quick start.

PROJECT_REQUIREMENTS.md

What the platform must do.

ARCHITECTURE.md

How the platform is structured.

DESIGN_SYSTEM.md

Visual and layout rules.

CONTENT_SCHEMA.md

How educational content is structured.

BOOK_SCHEMA.md

How books are configured.

PUBLICATION_SCHEMA.md

How author, publisher and copyright information is structured.

QA_SPECIFICATION.md

How quality assurance works.

DECISIONS.md

Important architectural decisions.

CHANGELOG.md

Changes over time.

REVIEW.md

Current review findings and outstanding issues.

handover.md

Instructions for Claude Code or another implementation agent.

---

28. Configuration Hierarchy

Configuration should follow this hierarchy:

Platform Defaults
       ↓
Subject Defaults
       ↓
Theme Defaults
       ↓
Book Configuration
       ↓
Unit Configuration
       ↓
Lesson Metadata

More specific configuration overrides more general configuration.

This allows maximum reuse.

---

29. Example Scaling Model

A Grade 3 Mathematics book might use:

Core Framework
+
Mathematics Framework
+
Primary Theme
+
PNG Grade 3 Curriculum
+
Grade 3 Mathematics Content

A Grade 6 Science book would use:

Core Framework
+
Science Framework
+
Primary Theme
+
PNG Grade 6 Curriculum
+
Grade 6 Science Content

The core publishing system remains unchanged.

---

30. Security and Intellectual Property

The platform shall keep publication ownership information separate from technical build configuration.

Copyright and licensing information shall be explicitly declared.

Assets with unknown or unsuitable licensing should generate validation warnings or errors depending on severity.

The platform should maintain attribution information for assets that require it.

---

31. Future Extensibility

The architecture should permit future additions such as:

- Interactive web textbooks
- Online assessments
- Kolibri-compatible resources
- Learning-management integration
- Audio resources
- Video resources
- AI-assisted lesson planning
- AI-assisted question generation
- Translation workflows
- Accessibility enhancements
- Multiple languages
- Multiple curricula
- Print-on-demand workflows

These should be added without fundamentally changing the core content model.

---

32. Architectural Rule

The most important architectural rule is:

«Do not design the platform around one textbook. Design the textbook around the platform.»

The first textbook is the test case for the platform, not the platform itself.

---

33. Initial Implementation Priority

Claude Code should implement the platform in this order:

Phase 1 — Foundation

- Repository structure
- Configuration system
- Book schema
- Publication metadata
- Documentation

Phase 2 — Content

- Curriculum schema
- Lesson schema
- Component system
- Assessment schema

Phase 3 — Rendering

- Design system
- Templates
- PDF generation
- EPUB generation

Phase 4 — QA

- Source validation
- Curriculum validation
- Asset validation
- Output validation
- QA reports

Phase 5 — Prototype

Build one complete Grade 3 Mathematics unit.

Phase 6 — Refinement

Use the prototype to identify weaknesses and improve the platform.

Phase 7 — Scaling

Add additional grades and subjects using the established architecture.

---

34. Architecture Success Criteria

The architecture will be considered successful when the platform can create a new textbook by supplying:

Book Configuration
+
Curriculum
+
Content
+
Assets

to the existing publishing engine and produce:

Professional PDF
+
EPUB
+
QA Report

without modifying the core publishing engine for ordinary textbook creation.

---

35. Final System Model

The complete architecture can be represented as:

                         PLATFORM
                            │
              ┌─────────────┴─────────────┐
              │                           │
        CORE ENGINE                 SUBJECT ENGINE
              │                           │
              └─────────────┬─────────────┘
                            │
                    BOOK CONFIGURATION
                            │
          ┌─────────────────┼─────────────────┐
          ↓                 ↓                 ↓
      CURRICULUM         CONTENT          PUBLICATION
          │                 │                 │
          │                 │          ┌──────┼──────┐
          │                 │          ↓      ↓      ↓
          │                 │       Author Publisher Copyright
          │                 │
          └────────┬────────┘
                   ↓
                 ASSETS
                   ↓
             DESIGN SYSTEM
                   ↓
             BUILD ENGINE
                   ↓
          ┌────────┴────────┐
          ↓                 ↓
        PDF               EPUB
          │                 │
          └────────┬────────┘
                   ↓
              QUALITY ASSURANCE
                   ↓
              HUMAN REVIEW
                   ↓
                RELEASE

This architecture gives us the foundation for a genuine reusable publishing platform, rather than a collection of scripts for making one book.
