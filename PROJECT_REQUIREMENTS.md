PNG Textbook Production Platform

Project Requirements Specification

Project: PNG Textbook Production Platform
Repository: "png-textbook-platform"
Document: "PROJECT_REQUIREMENTS.md"
Version: 0.1
Status: Initial Specification
Country: Papua New Guinea

---

1. Purpose

The PNG Textbook Production Platform (PTPP) is a reusable, AI-assisted publishing system for planning, writing, designing, producing, validating, and publishing primary-school textbooks and related educational materials.

The platform is designed to support multiple:

- Grades
- Subjects
- Textbooks
- Teacher guides
- Assessment books
- Workbooks
- Digital editions

The platform must allow new books to be created without rebuilding the underlying publishing system.

---

2. Core Concept

The platform shall separate:

1. Publishing engine
2. Subject frameworks
3. Book-specific content
4. Publication metadata
5. Assets and illustrations
6. Quality assurance
7. Output formats

The fundamental model is:

Reusable Platform
        +
Subject Framework
        +
Grade/Curriculum
        +
Book Configuration
        +
Book Content
        ↓
Published Educational Product

---

3. Primary Objectives

The platform shall:

- Provide a repeatable textbook production workflow.
- Support multiple grades and subjects.
- Support PNG primary-school curriculum requirements.
- Allow AI-assisted planning and writing.
- Support human review and approval.
- Generate consistent professional layouts.
- Support illustrations, diagrams, tables and educational graphics.
- Automate quality-control checks wherever practical.
- Generate PDF and EPUB editions.
- Preserve source content independently of the final PDF.
- Maintain version history through Git.
- Make it easy to create future textbooks using the same framework.

---

4. Design Principles

The platform shall follow these principles.

4.1 Source-first

The PDF or EPUB shall never be the master copy.

Structured source content shall remain the authoritative source.

4.2 Reusability

The publishing engine shall be reusable across books.

A new textbook should primarily require:

- configuration
- curriculum data
- content
- assets

rather than changes to the publishing engine.

4.3 Modularity

Components should be reusable.

Examples:

- lesson
- activity
- worked example
- exercise
- assessment
- vocabulary
- diagram
- table
- summary

4.4 Curriculum traceability

Every major learning objective should be traceable from:

Curriculum
→ Unit
→ Lesson
→ Activity
→ Assessment

4.5 Human oversight

AI-generated content shall not automatically become final published content.

The workflow must include human review.

4.6 Reproducible builds

The same source and configuration should produce a consistent publication.

4.7 Version control

All significant changes should be traceable through Git.

---

5. Supported Educational Products

The platform should eventually support:

Student textbooks

- Main textbooks
- Workbooks
- Activity books
- Revision books

Teacher materials

- Teacher guides
- Teacher resource books
- Answer keys
- Assessment guides

Digital materials

- EPUB
- HTML/web editions
- Printable PDFs
- Potential future interactive materials

---

6. Grade and Subject Architecture

The platform shall support:

Grade
 └── Subject
      └── Book

Examples:

Grade 3
 ├── Mathematics
 ├── English
 └── Science

Grade 4
 ├── Mathematics
 ├── English
 └── Science

Grades and subjects must not require separate publishing engines.

---

7. Book Configuration

Every textbook shall have a central configuration file.

Example:

book:
  title: "Grade 4 Mathematics"
  grade: 4
  subject: mathematics
  language: English
  curriculum: PNG

publication:
  author: "[Author]"
  publisher: "[Publisher]"
  copyright_year: 2026
  license: "Copyright"

output:
  pdf: true
  epub: true

The configuration shall control the build process.

---

8. Curriculum System

The platform shall support curriculum mapping.

The curriculum system should be able to record:

- Strand
- Sub-strand
- Topic
- Learning outcome
- Content standard
- Performance indicator
- Grade
- Curriculum reference

Each lesson should be capable of linking to relevant curriculum requirements.

The platform should eventually provide curriculum coverage reports.

Example:

Curriculum Outcome
        ↓
Unit 3
        ↓
Lesson 14
        ↓
Activity 14.2
        ↓
Assessment Question 27

---

9. Content Architecture

Content shall be structured rather than stored only as free-form documents.

A typical lesson shall support:

Lesson
├── Lesson number
├── Title
├── Curriculum links
├── Learning objectives
├── Key vocabulary
├── Materials/resources
├── Introduction
├── Teaching content
├── Examples
├── Activities
├── Practice
├── Challenge
├── Assessment
├── Summary
└── Teacher notes

Not every subject must use every component.

Subject frameworks may define appropriate variations.

---

10. Subject Frameworks

The platform shall allow subject-specific components.

Mathematics

Potential components:

- Worked example
- Let's calculate
- Problem solving
- Practice
- Challenge
- Mathematical reasoning

Science

Potential components:

- Investigation
- Prediction
- Observation
- Experiment
- Results
- Conclusion

English

Potential components:

- Reading
- Vocabulary
- Grammar
- Speaking
- Listening
- Writing
- Comprehension

Subject frameworks shall use the common publishing engine while allowing appropriate educational structures.

---

11. Publication Metadata

Publication information shall be a core feature.

Each book shall support:

Author

- Name
- Role
- Biography
- Website
- Contact information where appropriate

Publisher

- Name
- Location
- Website
- Contact information where appropriate

Copyright

- Copyright holder
- Copyright year
- License
- Rights statement

Edition

- Edition number
- Publication date

ISBN

- ISBN where assigned

Credits

- Editor
- Illustrator
- Contributors

Acknowledgements

- Acknowledgements text

---

12. Initial Author and Copyright Configuration

The initial publishing model shall support the user as the author.

The platform shall not hard-code the author's identity into the publishing engine.

Author information shall be supplied through book metadata.

The initial copyright configuration shall be:

License: Copyright
Rights: All rights reserved.

The system should be designed so that the copyright/license can be changed later if a different licensing model is selected.

---

13. Generated Publication Pages

The publication engine should automatically generate:

- Cover
- Title page
- Copyright page
- Publication information
- Acknowledgements
- Table of contents
- Main content
- References
- Answer section where applicable

Publication metadata shall flow automatically into the appropriate pages.

---

14. Design System

The platform shall maintain a centralized design system.

It should define:

- Page sizes
- Margins
- Typography
- Heading hierarchy
- Paragraph styles
- Colour usage
- Tables
- Callout boxes
- Activities
- Examples
- Illustrations
- Captions
- Headers
- Footers
- Page numbering
- Chapter/unit numbering

The design system should be reusable across textbooks.

Subject-specific variations should be configurable.

---

15. Illustration and Graphics System

The platform shall support:

- Illustrations
- Educational diagrams
- Charts
- Tables
- Icons
- Maps
- Mathematical diagrams
- Science diagrams
- Photographs where appropriately licensed
- AI-generated artwork where appropriate

Assets shall be stored separately from text content.

Every significant asset should have metadata where appropriate:

- filename
- description
- source
- creator
- license
- attribution requirement

---

16. AI-Assisted Production

The platform is intended to work with AI agents.

The preferred workflow is:

ChatGPT
   ↓
Planning / reasoning / review
   ↓
Project specifications
   ↓
GitHub
   ↓
Claude Code
   ↓
Implementation / content production / automation
   ↓
Build + QA
   ↓
ChatGPT + human review

AI must operate within project requirements and documented decisions.

AI agents should not silently alter fundamental project architecture.

---

17. Automated Quality Assurance

The platform shall provide automated checks where practical.

Structural checks

- Missing files
- Missing sections
- Duplicate lesson numbers
- Invalid metadata
- Broken references
- Missing assets

Content checks

- Missing learning objectives
- Missing answers
- Missing curriculum mappings
- Duplicate questions
- Inconsistent terminology

Layout checks

- Page overflow
- Missing images
- Broken image references
- Invalid page structure
- Unexpected blank pages

Subject-specific checks

The platform should eventually support specialized validation.

For Mathematics this may include:

- Calculation verification
- Answer verification
- Question/answer consistency

---

18. Visual Quality Assurance

Successful generation of a PDF shall not constitute final approval.

The platform shall support:

Source
 ↓
Build
 ↓
PDF
 ↓
Render pages
 ↓
Visual inspection
 ↓
Corrections
 ↓
Rebuild

Visual review should check:

- Page balance
- Typography
- Image placement
- Page breaks
- Tables
- Activities
- Headers/footers
- Captions
- Blank pages
- Consistency

---

19. Build System

The platform shall provide a reproducible build process.

Conceptually:

book.yml
     +
content
     +
curriculum
     +
assets
     +
templates
     +
design system
        ↓
      BUILD
        ↓
   PDF / EPUB

The build system should produce clearly identified output files.

---

20. Output Formats

Initial required formats:

- PDF
- EPUB

Potential future formats:

- HTML
- Web textbook
- Print-ready files
- Accessible digital editions
- Interactive educational materials

---

21. Versioning

The platform shall support versioned publications.

Example:

v0.1 — Prototype
v0.5 — Pilot
v0.9 — Pre-publication
v1.0 — First published edition
v1.1 — Corrections
v2.0 — Major revision

Each published edition should be reproducible from its source state.

---

22. Repository Architecture

The repository shall broadly follow:

png-textbook-platform/
│
├── framework/
├── books/
├── assets/
├── scripts/
├── tests/
├── output/
├── docs/
│
├── README.md
├── handover.md
├── PROJECT_REQUIREMENTS.md
├── ARCHITECTURE.md
├── DESIGN_SYSTEM.md
├── CONTENT_SCHEMA.md
├── BOOK_SCHEMA.md
├── PUBLICATION_SCHEMA.md
├── QA_SPECIFICATION.md
├── DECISIONS.md
├── CHANGELOG.md
└── REVIEW.md

---

23. Scalability Requirement

The architecture must allow the addition of:

New Grade
New Subject
New Textbook
New Edition
New Author
New Publisher
New Curriculum

without requiring a redesign of the entire platform.

---

24. First Prototype

The first implementation shall not attempt to produce an entire textbook immediately.

The initial proof-of-concept shall use:

Grade: 3
Subject: Mathematics
Product: Student textbook

The prototype should contain at least one complete unit.

The prototype must demonstrate:

Book configuration
        ↓
Curriculum mapping
        ↓
Structured lessons
        ↓
Illustrations
        ↓
Layout
        ↓
Automated QA
        ↓
PDF
        ↓
EPUB
        ↓
Visual QA

---

25. Definition of Done — Platform Prototype

The prototype shall be considered successful when:

- A book can be configured without changing core publishing code.
- A grade can be changed through book configuration.
- A subject framework can be selected.
- Structured lessons can be added.
- Curriculum mappings can be stored.
- Author and publisher information can be supplied.
- Copyright information is automatically generated.
- Illustrations can be incorporated.
- A book can be built into PDF.
- A book can be built into EPUB.
- Automated validation can run.
- Generated pages can be visually inspected.
- The system can produce a complete prototype unit.
- Documentation explains how another textbook is created.

---

26. Future Direction

The platform should eventually evolve into a complete educational publishing system capable of producing a family of textbooks such as:

Grade 1
Grade 2
Grade 3
Grade 4
Grade 5
Grade 6

across multiple subjects.

The long-term architecture should also allow the same structured educational content to support:

Student Textbook
      +
Teacher Guide
      +
Workbook
      +
Assessment Book
      +
Digital/HTML Edition
      +
eLibrary Resources

without rewriting the underlying content from scratch.

---

27. Development Philosophy

The platform shall be developed incrementally.

Do not build the entire system blindly.

Use the cycle:

PLAN
 ↓
SPECIFY
 ↓
IMPLEMENT
 ↓
BUILD
 ↓
TEST
 ↓
REVIEW
 ↓
IMPROVE

Each major feature should be tested using a real textbook use case.

The first textbook is therefore both:

1. an educational product, and
2. a test case for the publishing platform.

---

28. Initial Technology Principle

The exact technical implementation shall be selected during the architecture phase.

The platform should favour:

- Open standards
- Portable source formats
- Reproducible builds
- Free/open-source tooling where practical
- Git/GitHub compatibility
- Automation
- Extensibility
- Minimal vendor lock-in

Technology choices must be documented in "ARCHITECTURE.md" and "DECISIONS.md".

---

29. AI Agent Operating Principle

Claude Code shall be treated as a production/implementation agent rather than the ultimate decision-maker.

Before making significant architectural changes, it shall:

1. Read project documentation.
2. Identify existing decisions.
3. Preserve established interfaces.
4. Test changes.
5. Document significant changes.
6. Report unresolved issues.

ChatGPT and human review shall provide architectural and editorial oversight.

---

30. Project Success

The ultimate measure of success is not simply whether the system can generate a PDF.

The platform should make it possible to move from:

"I want to create a Grade 5 Science textbook"

to:

Curriculum
    ↓
Book plan
    ↓
Structured content
    ↓
Illustrations
    ↓
Automated checks
    ↓
Professional layout
    ↓
Human review
    ↓
Published textbook

using the same reusable production system.

The platform should become a textbook publishing engine, not a one-off book-making project.
