Architecture Decision Records

PNG Textbook Production Platform (PTPP)

Repository: "png-textbook-platform"
Document: "DECISIONS.md"
Status: Active
Version: 1.0

---

1. Purpose

This document records important architectural, technical, publishing, and workflow decisions made for the PNG Textbook Production Platform.

The purpose is to ensure that:

- decisions are preserved
- future development does not contradict established principles
- Claude Code and other AI agents understand the intended architecture
- new features remain compatible with the platform
- major changes are deliberate rather than accidental

This document is a decision record, not a general requirements document.

---

2. Decision Status

Each decision may have one of these statuses:

PROPOSED
ACCEPTED
IMPLEMENTED
SUPERSEDED
REJECTED

An accepted decision should not be changed casually.

A decision that is no longer valid should be marked "SUPERSEDED" rather than deleted.

---

ADR-001 — Build a Reusable Textbook Production Platform

Status: ACCEPTED

Decision

The project will build a reusable textbook production platform rather than producing one textbook as an isolated project.

The platform must support multiple:

- grades
- subjects
- textbooks
- workbooks
- teacher guides
- assessment books
- digital publications

Reason

The objective is to create a system capable of producing many educational publications efficiently.

The first textbook is therefore a prototype for the platform, not the platform itself.

Consequence

Core publishing functionality must be reusable.

A new textbook should primarily require:

Configuration
+
Curriculum
+
Content
+
Assets

rather than new programming.

---

ADR-002 — One Repository for the Platform

Status: ACCEPTED

Decision

The core publishing platform will use one Git repository:

png-textbook-platform

Reason

The publishing engine, schemas, themes, QA system, subject frameworks, documentation, and book configurations are related components of one system.

Consequence

The repository can contain multiple books while maintaining one shared engine.

---

ADR-003 — Grades and Subjects Are Content, Not Git Branches

Status: ACCEPTED

Decision

Grades and subjects will not normally be represented as Git branches.

They will be represented as books/configurations/content.

Example:

books/
├── grade-3/
│   └── mathematics/
├── grade-4/
│   ├── mathematics/
│   └── science/
└── grade-5/
    └── english/

Reason

Branches represent development states or features, not permanent content categories.

Consequence

Git branches may be used for:

feature development
bug fixes
experiments
major revisions

but not simply:

grade-3
grade-4
grade-5

---

ADR-004 — Separate Publishing Engine from Book Content

Status: ACCEPTED

Decision

The publishing engine and textbook content must remain separate.

Conceptually:

Publishing Engine
       +
Subject Framework
       +
Theme
       +
Book Configuration
       +
Curriculum
       +
Content
       +
Assets
       ↓
Publication

Reason

Changing textbook content should not require modifying the publishing engine.

Consequence

The engine can be reused across many books.

---

ADR-005 — Source Content Is the Master

Status: ACCEPTED

Decision

Source files are the authoritative version of textbook content.

Generated files are outputs.

Source
  ↓
Build
  ↓
PDF / EPUB / HTML / other outputs

The generated PDF must never become the primary source for editing textbook content.

Reason

This enables:

- version control
- automated validation
- multiple formats
- easy revision
- reproducible builds

---

ADR-006 — Use Structured Content

Status: ACCEPTED

Decision

Textbook content will use structured Markdown and YAML metadata rather than relying entirely on page-layout software.

Example:

lesson-01.md
unit.yml
assessment.yml
book.yml

Reason

Structured content allows software to understand and validate the textbook.

It also allows the same content to generate different publications.

---

ADR-007 — Separate Content from Design

Status: ACCEPTED

Decision

Authors should write educational content without manually controlling final page layout.

Design will be controlled by:

Themes
Design tokens
Components
Templates
Publishing engine

Reason

This allows the same content to be rendered consistently across books and formats.

Consequence

Source content should avoid:

- manual page numbers
- absolute positioning
- arbitrary page breaks
- formatting hacks

---

ADR-008 — Use a Reusable Component System

Status: ACCEPTED

Decision

Common educational elements will be represented as reusable components.

Examples:

Objective
Vocabulary
Example
Worked Example
Activity
Practice
Challenge
Assessment
Summary
Definition
Tip
Investigation
Figure
Table

Reason

Reusable components provide consistent design and simplify automated rendering.

Consequence

Subject-specific components may extend the core component system.

---

ADR-009 — Subject Frameworks Extend the Core Platform

Status: ACCEPTED

Decision

The platform will have subject-specific frameworks.

Initial subjects include:

Mathematics
English
Science
Social Science

Reason

Different subjects require different pedagogical structures.

For example:

Mathematics may require:

Worked Example
Calculation
Problem Solving
Reasoning

Science may require:

Prediction
Materials
Method
Observation
Results
Conclusion

English may require:

Reading
Comprehension
Grammar
Vocabulary
Writing
Speaking
Listening

Consequence

Subject-specific functionality extends the platform without creating separate publishing systems.

---

ADR-010 — Grade Is Primarily Configuration

Status: ACCEPTED

Decision

Grades will primarily be represented through configuration, curriculum, content, and grade-specific design rules rather than separate publishing engines.

Reason

The underlying publishing technology is largely reusable between grades.

Consequence

A Grade 3 and Grade 6 book can use the same core engine while having different:

- curriculum
- vocabulary
- difficulty
- examples
- activities
- typography adjustments
- visual complexity

---

ADR-011 — Curriculum Traceability Is Required

Status: ACCEPTED

Decision

Curriculum references will use stable identifiers.

Example:

MATH-G4-NUM-001

Content and assessment items should link to these identifiers.

Reason

The platform must be able to answer:

«Which curriculum requirement does this lesson or assessment address?»

Consequence

The system can generate curriculum coverage and traceability reports.

---

ADR-012 — Curriculum and Content Are Separate

Status: ACCEPTED

Decision

Curriculum information will be stored independently from lesson content.

Example:

curriculum/
units/
lessons/

Reason

Curriculum documents may change while educational content remains partially reusable.

Consequence

Curriculum versions can be tracked independently.

---

ADR-013 — Publication Metadata Is Separate

Status: ACCEPTED

Decision

Author, publisher, copyright, edition, credits, and acknowledgements are treated as publication metadata.

Example:

publication/
├── author.yml
├── publisher.yml
├── copyright.yml
├── edition.yml
├── credits.yml
└── acknowledgements.md

Reason

Publication information is fundamentally different from educational content.

Consequence

The same publishing engine can produce publications for different authors or publishers.

---

ADR-014 — Author Identity Is Book Metadata

Status: ACCEPTED

Decision

The author's identity will not be hard-coded into the publishing engine.

The current textbook author will be supplied through book publication metadata.

Reason

The platform must support future authors and collaborators.

Consequence

Changing author information does not require modifying the engine.

---

ADR-015 — Initial Copyright Model

Status: ACCEPTED

Decision

The initial textbooks will use standard copyright.

Default:

license: "Copyright"
rights: "All rights reserved."

Reason

This reflects the intended initial ownership model.

Consequence

The platform must still support other licensing models in the future.

Possible future licenses include:

CC BY
CC BY-SA
CC BY-NC
CC BY-NC-SA
Public Domain
Custom

---

ADR-016 — Do Not Invent ISBNs

Status: ACCEPTED

Decision

The platform may store ISBN information but must never generate or invent an ISBN.

Reason

ISBNs are official publication identifiers.

Consequence

Missing ISBN information should produce a warning rather than fabricated data.

---

ADR-017 — Asset Rights Must Be Tracked

Status: ACCEPTED

Decision

Illustrations, photographs, diagrams, maps, charts, and other external assets must have rights/licensing metadata.

Reason

Book copyright and individual asset rights are separate issues.

Consequence

Unknown asset licensing should trigger a QA warning or release-blocking error depending on configuration.

---

ADR-018 — AI Content Is Draft Until Reviewed

Status: ACCEPTED

Decision

AI-generated educational content is treated as draft content until reviewed and approved.

This applies to:

- text
- questions
- answers
- illustrations
- diagrams
- metadata suggestions
- lesson plans

Reason

AI can accelerate production but should not be treated as the final authority for educational accuracy.

Consequence

AI-generated material enters the same validation and human-review process as other content.

---

ADR-019 — ChatGPT and Claude Code Have Different Roles

Status: ACCEPTED

Decision

The project will use a two-stage AI workflow.

ChatGPT

Primarily responsible for:

- planning
- reasoning
- architecture
- curriculum analysis
- specifications
- review
- design decisions
- QA analysis
- identifying problems
- preparing instructions

Claude Code

Primarily responsible for:

- repository inspection
- implementation
- file creation/editing
- automation
- scripts
- rendering
- testing
- running QA
- fixing implementation issues
- reporting results

Reason

This separates strategic reasoning from production implementation.

---

ADR-020 — GitHub Is the Source of Truth for the Project

Status: ACCEPTED

Decision

GitHub will contain the authoritative project source.

It will contain:

- source content
- configuration
- schemas
- publishing engine
- assets where appropriate
- tests
- documentation
- QA rules
- build scripts

Reason

Git provides:

- version history
- rollback
- collaboration
- branching
- change tracking
- reproducibility

---

ADR-021 — AI Agents Must Read Project Documentation First

Status: ACCEPTED

Decision

AI coding agents must inspect project documentation before implementing significant changes.

At minimum they should read:

README.md
PROJECT_REQUIREMENTS.md
ARCHITECTURE.md
DECISIONS.md

and any relevant schema/specification.

Reason

AI agents can otherwise make technically reasonable changes that contradict project decisions.

Consequence

Project documentation becomes part of the engineering interface.

---

ADR-022 — AI Agents Must Not Override Architectural Decisions

Status: ACCEPTED

Decision

Claude Code or another AI agent may identify a better technical approach, but must not silently replace an established architectural decision.

It should:

1. identify the conflict
2. explain the proposed alternative
3. record the issue
4. request a decision where appropriate

Reason

Implementation agents are responsible for execution, not unilateral architectural governance.

---

ADR-023 — QA Is Built Into the Publishing Pipeline

Status: ACCEPTED

Decision

QA will not be treated as an optional final activity.

It will be integrated into the build pipeline.

Validate
 ↓
Build
 ↓
Validate Output
 ↓
Visual QA
 ↓
Human Review
 ↓
Release

Reason

Early detection is cheaper and more reliable than discovering errors after publication.

---

ADR-024 — Release Requires Zero Critical Errors

Status: ACCEPTED

Decision

A release build must have:

Critical Errors = 0

Warnings may remain only after review and acceptance.

Reason

Known critical errors should never be knowingly published.

---

ADR-025 — Human Review Remains Mandatory

Status: ACCEPTED

Decision

Automated QA cannot provide final approval for educational publication.

Human review is required for:

- curriculum interpretation
- educational quality
- factual accuracy
- cultural suitability
- language quality
- illustrations
- sensitive content
- copyright/legal suitability
- final visual quality

Reason

These areas require professional judgment and contextual understanding.

---

ADR-026 — Visual QA Is Required

Status: ACCEPTED

Decision

A successful source validation/build does not automatically mean the book is visually acceptable.

The generated publication must undergo visual inspection.

Reason

Many layout problems cannot reliably be detected from source files alone.

Examples:

clipped images
awkward page breaks
broken tables
orphan headings
excessive whitespace

---

ADR-027 — PDF and EPUB Are Generated Outputs

Status: ACCEPTED

Decision

PDF and EPUB are generated from the master source.

They are not independently maintained as primary content.

Reason

Maintaining multiple manually edited versions would create inconsistency.

---

ADR-028 — One Master Content Model Can Generate Multiple Products

Status: ACCEPTED

Decision

Where practical, the same structured content should generate:

- student textbook
- workbook
- teacher guide
- answer book
- assessment book
- digital edition

Reason

This reduces duplicated work and prevents inconsistencies.

Example

Master Question
       ↓
 ┌─────┼─────┬──────────┐
 ↓     ↓     ↓          ↓
Book  Quiz  Workbook  Answer Key

---

ADR-029 — Assessments Are Structured Data

Status: ACCEPTED

Decision

Assessment questions will be stored as structured data rather than embedded only as ordinary prose.

Reason

Structured questions can be reused and validated.

They can support future:

- quizzes
- answer keys
- teacher guides
- digital assessments
- LMS integration
- assessment reports

---

ADR-030 — Stable IDs Are Fundamental

Status: ACCEPTED

Decision

Important textbook entities will use stable IDs.

Examples:

Book
Unit
Lesson
Curriculum Outcome
Question
Figure
Activity
Assessment

Reason

Stable IDs enable:

- references
- traceability
- automated validation
- content reuse
- future database integration

---

ADR-031 — Avoid Page-Specific Source Formatting

Status: ACCEPTED

Decision

Authors should not normally specify:

page 12
page break
place image exactly at X/Y

inside source content.

Reason

Page layouts differ between formats and may change when content changes.

Consequence

The publishing engine determines layout.

---

ADR-032 — Use Configuration Inheritance

Status: ACCEPTED

Decision

Configuration follows this hierarchy:

Platform Defaults
        ↓
Subject Defaults
        ↓
Grade Rules
        ↓
Theme Defaults
        ↓
Book Configuration
        ↓
Unit Configuration
        ↓
Lesson Metadata

More specific configuration overrides more general configuration.

Reason

This minimizes duplication.

---

ADR-033 — Primary Theme Is the Initial Design Theme

Status: ACCEPTED

Decision

The initial platform theme will be called:

primary

It is intended for primary-school educational publications.

Reason

The first target publications are primary-school textbooks.

Consequence

Future themes may include:

secondary
professional
minimal
print
digital

without changing the content model.

---

ADR-034 — A4 Is the Initial Default Page Size

Status: ACCEPTED

Decision

The initial default page size is:

A4 Portrait

The platform must remain configurable for other formats.

Reason

A4 is a practical initial format for development and educational publication.

Future support may include:

A5
Letter
Legal
Custom

---

ADR-035 — Content Must Be Format Independent

Status: ACCEPTED

Decision

Educational content should not depend on whether it will ultimately appear in:

- PDF
- EPUB
- HTML
- website
- digital learning platform

Reason

Future publication formats should not require rewriting the textbook.

---

ADR-036 — Accessibility Is Part of the Design

Status: ACCEPTED

Decision

Accessibility requirements will be incorporated into the content and design systems from the beginning.

Examples:

- alt text
- meaningful headings
- accessible tables
- readable typography
- no colour-only information

Reason

Accessibility should not be added as an afterthought.

---

ADR-037 — The Platform Should Support PNG Curriculum First

Status: ACCEPTED

Decision

The initial curriculum framework will support Papua New Guinea curriculum requirements.

The architecture should nevertheless remain capable of supporting other curricula later.

Reason

PNG is the initial target environment.

Consequence

Curriculum implementation must be modular rather than hard-coded into the entire engine.

---

ADR-038 — The Platform Should Be Suitable for Local Context

Status: ACCEPTED

Decision

The platform should support educational content appropriate to Papua New Guinea, including:

- local examples
- local geography
- local communities
- PNG contexts
- appropriate names and scenarios
- locally relevant illustrations

Reason

Educational relevance is improved when examples reflect learners' environments.

---

ADR-039 — Do Not Over-Engineer the First Version

Status: ACCEPTED

Decision

The first implementation should build the smallest useful publishing engine capable of producing a complete prototype textbook.

Reason

The platform should be proven through a real book before implementing every future feature.

Initial priority:

Foundation
 ↓
Content Model
 ↓
Rendering
 ↓
QA
 ↓
Complete Prototype
 ↓
Refinement
 ↓
Scaling

---

ADR-040 — First Prototype Is a Complete Book Unit

Status: ACCEPTED

Decision

The first meaningful prototype should be a complete unit rather than a collection of disconnected demonstrations.

Reason

A complete unit tests the entire pipeline:

Curriculum
Content
Components
Assets
Assessment
Rendering
QA

---

ADR-041 — The Platform Must Eventually Support Digital Learning

Status: ACCEPTED

Decision

The architecture should not prevent future integration with digital learning systems.

Potential future outputs include:

HTML
Interactive textbook
Kolibri resources
LMS content
Digital quizzes
Interactive assessments

Reason

The long-term objective is broader than printed books.

---

ADR-042 — The Platform Should Support AI-Assisted Future Features

Status: ACCEPTED

Decision

The architecture should allow future AI-assisted features including:

- lesson planning
- question generation
- differentiated activities
- answer generation
- curriculum mapping assistance
- translation
- teacher-guide generation
- content review
- assessment generation

Reason

Structured content creates a foundation for intelligent educational tools.

---

ADR-043 — Do Not Hard-Code One Book

Status: ACCEPTED

Decision

No major platform component should be designed around only one textbook.

The implementation must distinguish between:

Platform logic

and:

Book-specific content

Golden Rule

«Do not design the platform around one textbook. Design the textbook around the platform.»

---

ADR-044 — Documentation Is Part of the Product

Status: ACCEPTED

Decision

Technical and publishing documentation is treated as part of the platform itself.

Core documents include:

README.md
PROJECT_REQUIREMENTS.md
ARCHITECTURE.md
DECISIONS.md
DESIGN_SYSTEM.md
CONTENT_SCHEMA.md
BOOK_SCHEMA.md
PUBLICATION_SCHEMA.md
QA_SPECIFICATION.md
CHANGELOG.md
REVIEW.md
handover.md

Reason

Future AI agents, developers, authors, and reviewers need a clear understanding of the system.

---

ADR-045 — Changes Must Be Traceable

Status: ACCEPTED

Decision

Significant architectural changes must be recorded in:

DECISIONS.md

Implementation changes should also be reflected in:

CHANGELOG.md

Reason

The platform will evolve over time.

Without a decision history, future contributors may not understand why the system works a particular way.

---

ADR-046 — The Platform Is Both a Publishing System and a Content System

Status: ACCEPTED

Decision

The platform should be designed as two closely connected systems:

CONTENT SYSTEM
      +
PUBLISHING SYSTEM

The content system manages:

- curriculum
- lessons
- questions
- answers
- assets
- educational structures

The publishing system manages:

- layout
- typography
- rendering
- PDF
- EPUB
- metadata
- QA
- release

Reason

This separation enables the educational content to be reused beyond traditional textbooks.

---

ADR-047 — Master Content Should Be Reusable Outside Books

Status: ACCEPTED

Decision

The structured educational content should eventually be reusable for:

- website lessons
- teacher resources
- digital learning
- quizzes
- LMS content
- Kolibri
- future applications

Reason

A well-structured lesson contains more value than its printed page.

---

ADR-048 — Release Versions Are Separate from Development Versions

Status: ACCEPTED

Decision

Technical source versions and publication editions are separate concepts.

Example:

Source:
v0.8.14

Publication:
1st Edition, 2027

Reason

Internal software revisions can occur without creating a new published edition.

---

ADR-049 — The Author Remains the Final Content Authority

Status: ACCEPTED

Decision

AI tools and software systems assist the author but do not replace the author's responsibility for the final educational content.

Reason

The platform is an authoring and publishing system, not an autonomous publisher.

---

ADR-050 — Future Decisions Must Preserve the Core Architecture

Status: ACCEPTED

Future technical decisions should be evaluated against these principles:

Reusable
Modular
Source-first
Structured
Curriculum-traceable
AI-assisted
Human-reviewed
Testable
Reproducible
Format-independent
Accessible
Scalable

A new feature that violates one of these principles should require explicit architectural review.

---

6. Decision Change Procedure

When a significant architectural change is proposed:

Step 1

Identify the existing decision.

Step 2

Explain why it may no longer be suitable.

Step 3

Describe the proposed alternative.

Step 4

Identify consequences.

Step 5

Approve or reject the change.

Step 6

Update this document.

Step 7

If replacing an old decision, mark the old decision:

SUPERSEDED

Do not silently delete historical decisions.

---

7. AI Agent Rule

Any AI coding agent working on this repository should follow:

«Read the decisions before changing the architecture.»

If an implementation request conflicts with this document, the agent should identify the conflict rather than silently choosing an alternative architecture.

---

8. Current Architectural Summary

The platform can be summarized as:

                    PTPP
                     │
        ┌────────────┴────────────┐
        │                         │
   CONTENT SYSTEM          PUBLISHING SYSTEM
        │                         │
   Curriculum                 Themes
   Units                       Components
   Lessons                     Templates
   Assessments                 Rendering
   Questions                   PDF
   Answers                     EPUB
   Assets                      QA
        │                         │
        └────────────┬────────────┘
                     │
                     ▼
                PUBLICATION

The same content may eventually feed:

Printed Textbook
      │
      ├── Workbook
      ├── Teacher Guide
      ├── Answer Book
      ├── Assessment
      ├── Website
      ├── EPUB
      ├── HTML
      ├── Kolibri
      └── Interactive Learning

---

9. Foundational Principle

The most important architectural decision is:

«Create the educational content once, structure it properly, validate it rigorously, and allow the platform to transform it into many high-quality educational products.»

The platform exists to make that process repeatable.
