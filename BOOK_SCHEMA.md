BOOK_SCHEMA.md

PNG Textbook Production Platform

Book Configuration Schema

Document: BOOK_SCHEMA.md
Project: PNG Textbook Production Platform (PTPP)
Repository: "png-textbook-platform"
Status: Foundation Specification
Version: 1.0

---

1. Purpose

This document defines the configuration schema for an individual book within the PNG Textbook Production Platform.

The publishing engine must be reusable.

A new textbook should normally be created by supplying a new book configuration and content rather than modifying the publishing engine.

The central configuration file is:

books/<grade>/<subject>/book.yml

For example:

books/
└── grade-4/
    └── mathematics/
        └── book.yml

---

2. Core Principle

A book is defined by:

Grade
+
Subject
+
Curriculum
+
Content
+
Publication Metadata
+
Design
+
Products
+
Output Configuration

The publishing engine reads these settings and builds the required publication.

---

3. Book Configuration Hierarchy

Configuration follows this hierarchy:

Platform Defaults
        ↓
Subject Defaults
        ↓
Grade Defaults
        ↓
Theme Defaults
        ↓
Book Configuration
        ↓
Unit Configuration
        ↓
Lesson Metadata

A more specific setting overrides a more general setting.

For example:

Platform:
page_size = A4

Theme:
font = "Noto Sans"

Book:
page_size = A5

The book setting overrides the theme and platform default.

---

4. Basic Book Configuration

Minimum example:

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

  publisher:
    name: "[Publisher]"

  copyright:
    holder: "[Copyright Holder]"
    year: 2026
    license: "Copyright"
    rights: "All rights reserved."

output:
  pdf: true
  epub: true

---

5. Complete Book Configuration

A full configuration may contain:

book:
  id:
  title:
  subtitle:
  short_title:
  grade:
  subject:
  book_type:
  language:
  languages:
  curriculum:
  country:
  edition:

publication:
  author:
  contributors:
  editor:
  illustrator:
  publisher:
  copyright:
  acknowledgements:
  isbn:
  identifiers:

design:
  theme:
  page_size:
  orientation:
  margins:
  typography:

content:
  curriculum:
  units:
  assessments:
  answers:
  references:
  glossary:

products:
  student_book:
  teacher_guide:
  workbook:
  answer_book:
  assessment_book:

output:
  pdf:
  epub:
  html:
  web:
  kolibri:

qa:
  strict:
  curriculum_validation:
  accessibility:
  asset_validation:
  visual_validation:

Not every field is required.

---

6. Book Identity

The "book" section identifies the publication.

Example:

book:
  id: grade-4-mathematics
  title: "Grade 4 Mathematics"
  subtitle: "Learning Mathematics Through Practice and Discovery"
  short_title: "Grade 4 Mathematics"

  grade: 4
  subject: mathematics
  book_type: student_textbook

  language: en

  curriculum: png
  country: PG

  edition: 1

---

7. Book ID

The "id" must be unique within the repository.

Recommended format:

<grade>-<subject>-<book-type>

Examples:

grade-3-mathematics
grade-4-science
grade-5-english
grade-6-social-science

For alternative products:

grade-4-mathematics-workbook
grade-4-mathematics-teacher-guide

The ID should remain stable after publication.

---

8. Title

The title is the principal publication title.

Example:

title: "Grade 4 Mathematics"

The title may appear on:

- Cover
- Title page
- Copyright page
- PDF metadata
- EPUB metadata
- Website
- Library catalogue

---

9. Subtitle

Optional subtitle:

subtitle: "Learning Mathematics Through Practice and Discovery"

The subtitle should not be used to encode technical information.

---

10. Grade

The grade identifies the intended educational level.

Example:

grade: 4

The platform should support:

Elementary / Preparatory
Grade 1
Grade 2
Grade 3
Grade 4
Grade 5
Grade 6

The actual supported grades should be determined by the relevant curriculum configuration.

---

11. Subject

The subject identifies the academic framework.

Examples:

subject: mathematics

subject: english

subject: science

subject: social-science

Subject identifiers should use stable machine-readable names.

---

12. Book Type

The "book_type" field identifies the primary publication.

Supported core values:

student_textbook
workbook
activity_book
revision_book
teacher_guide
answer_book
assessment_book

Example:

book_type: student_textbook

This allows the same publishing engine to generate different educational products.

---

13. Language

Language uses a standard language identifier.

Example:

language: en

Future examples:

language: en

language: tok

language: ho

The system should support multilingual publications without changing the publishing engine.

---

14. Multiple Languages

A future multilingual book may define:

languages:
  - en
  - tok

The source content system may then support translated versions while preserving stable content IDs.

Example:

G4-MATH-L01
    ├── en
    └── tok

Translation should not require duplicating the publishing engine.

---

15. Curriculum

The curriculum identifies the educational framework to which the book is aligned.

Example:

curriculum:
  id: png
  version: "2026"

A more detailed configuration may specify:

curriculum:
  id: png
  country: PG
  version: "2026"
  subject: mathematics
  grade: 4

The actual curriculum data should remain in the book's "curriculum/" directory or an approved shared curriculum library.

---

16. Country

The country field identifies the primary educational context.

For Papua New Guinea:

country: PG

This should use ISO-style country codes.

The country setting may affect:

- Curriculum
- Language defaults
- Publication information
- Educational terminology
- Measurement conventions
- Currency examples
- Metadata

It must not hard-code country-specific assumptions into the core publishing engine.

---

17. Edition

Edition information:

edition:
  number: 1
  year: 2026
  name: "First Edition"

The publishing engine should automatically populate the relevant publication pages.

---

18. Publication Metadata

Publication metadata may be configured directly or referenced from the "publication/" directory.

Example:

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

The author's identity must remain book metadata rather than being hard-coded into the platform.

---

19. Author

The book may have one or multiple authors.

Single author:

author:
  - name: "[Author]"
    role: "Author"

Multiple authors:

author:
  - name: "[Author 1]"
    role: "Author"

  - name: "[Author 2]"
    role: "Author"

Additional author metadata may include:

author:
  - name: "[Author]"
    role: "Author"
    organization: "[Organization]"

---

20. Contributors

Additional contributors may be specified separately.

contributors:
  - name: "[Contributor]"
    role: "Curriculum Reviewer"

  - name: "[Contributor]"
    role: "Technical Reviewer"

Possible roles include:

Author
Editor
Curriculum Reviewer
Subject Reviewer
Technical Reviewer
Illustrator
Designer
Photographer
Translator
Contributor

---

21. Publisher

Publisher metadata:

publisher:
  name: "[Publisher]"
  location: "Papua New Guinea"

Additional information may include:

publisher:
  name: "[Publisher]"
  location: "Papua New Guinea"
  website: ""
  email: ""

Sensitive or unnecessary personal information should not be stored in the public configuration.

---

22. Copyright

Default publication model:

copyright:
  holder: "[Copyright Holder]"
  year: 2026
  license: "Copyright"
  rights: "All rights reserved."

This is the initial standard copyright configuration for the project.

The platform must also support future licensing models such as:

CC BY
CC BY-SA
CC BY-NC
CC BY-NC-SA
Public Domain
Custom License

The selected license must determine how the publication information is generated.

---

23. ISBN and Identifiers

ISBN is optional during development.

Example:

isbn:
  print: ""
  ebook: ""

Other identifiers may be supported:

identifiers:
  internal_id: "PTPP-G4-MATH-001"
  isbn13: ""

The publishing engine must not invent ISBNs.

---

24. Design Configuration

Design configuration controls the visual presentation without changing the source content.

Example:

design:
  theme: primary
  page_size: A4
  orientation: portrait

Possible themes:

primary
minimal
academic
workbook
teacher-guide

Themes should be reusable across books.

---

25. Page Size

Example:

page_size: A4

Supported sizes may include:

A4
A5
Letter
Legal
Custom

The design system determines the exact dimensions.

---

26. Orientation

Supported values:

orientation: portrait

or:

orientation: landscape

Landscape may be useful for:

- Maps
- Tables
- Certain science diagrams
- Activity pages
- Charts

---

27. Products

A single book configuration can control which related products are generated.

Example:

products:
  student_book: true
  teacher_guide: true
  workbook: false
  answer_book: true
  assessment_book: false

This enables one master content source to produce several related publications.

---

28. Student Book

student_book:
  enabled: true

The student book contains learner-facing material.

It should normally exclude:

- Teacher notes
- Hidden answers
- Teacher-only assessment guidance
- Internal production information

---

29. Teacher Guide

teacher_guide:
  enabled: true

The teacher guide may reuse:

- Lesson content
- Objectives
- Curriculum mapping
- Activities
- Answers
- Assessment guidance

Additional teacher-specific content should be maintained separately.

---

30. Workbook

workbook:
  enabled: true

A workbook may reuse:

- Practice questions
- Activities
- Assessment items
- Exercises

The workbook should be generated from structured content rather than copied manually.

---

31. Answer Book

answer_book:
  enabled: true

The answer book should be generated from the question bank and answer data.

This reduces duplication and helps prevent inconsistencies.

---

32. Assessment Book

assessment_book:
  enabled: false

Assessment books may be generated from structured assessment content.

The same question bank can support:

Textbook
Workbook
Assessment
Answer Book
Teacher Guide
Digital Quiz

---

33. Content Configuration

Content paths may be specified as:

content:
  curriculum: curriculum/
  units: units/
  assessments: assessments/
  answers: answers/
  references: references/

The default directory structure should normally be used so that books remain predictable.

---

34. Unit Ordering

Unit sequence should normally be determined by:

sequence: 1

inside each unit's "unit.yml".

The publishing engine should not rely solely on filesystem alphabetical order.

Example:

unit-01
unit-02
unit-03

is convenient, but the authoritative order is the metadata.

---

35. Assessments

Assessment configuration:

assessments:
  enabled: true
  source: assessments/

Additional options:

assessments:
  lesson_assessments: true
  unit_assessments: true
  final_assessment: true

---

36. Answers

Answer generation:

answers:
  enabled: true
  source: answers/

The engine should validate that every published question requiring an answer has a corresponding answer.

---

37. Glossary

Glossary generation:

glossary:
  enabled: true

Glossary entries may be collected automatically from structured vocabulary metadata.

---

38. References

References:

references:
  enabled: true
  source: references/

References should distinguish between:

- Curriculum documents
- Books
- Websites
- Open educational resources
- Images
- Other source material

---

39. Output Configuration

The output section determines which publication formats are generated.

Example:

output:
  pdf: true
  epub: true
  html: true
  web: false
  kolibri: false

---

40. PDF

pdf:
  enabled: true
  print_ready: true

Possible future options:

pdf:
  enabled: true
  print_ready: true
  screen: true

The engine may generate separate print and screen versions.

---

41. EPUB

epub:
  enabled: true

The EPUB must use the same master content.

It should not be maintained manually as a separate book.

---

42. HTML

html:
  enabled: true

HTML may be used for:

- Website publication
- Browser-based textbooks
- Digital resources
- Future interactive features

---

43. Kolibri

Future configuration:

kolibri:
  enabled: false

When implemented, the platform should produce resources compatible with the school's Kolibri environment where technically appropriate.

---

44. Quality Assurance

Book-level QA configuration:

qa:
  strict: true

  curriculum_validation: true
  content_validation: true
  assessment_validation: true
  asset_validation: true
  accessibility_validation: true
  output_validation: true
  visual_validation: true

---

45. Strict Mode

When:

strict: true

the build should fail for critical errors.

Examples:

Missing required metadata
Broken curriculum reference
Missing image
Missing answer
Duplicate content ID
Invalid question type
Invalid configuration
Missing license information

Warnings should remain distinguishable from errors.

---

46. Development Mode

A development configuration may use:

qa:
  strict: false

This allows incomplete content during development while still reporting problems.

Production releases should normally use strict validation.

---

47. Complete Example

book:

  id: grade-4-mathematics

  title: "Grade 4 Mathematics"

  subtitle: "Learning Mathematics Through Practice and Discovery"

  short_title: "Grade 4 Mathematics"

  grade: 4

  subject: mathematics

  book_type: student_textbook

  language: en

  country: PG

  curriculum:
    id: png
    version: "2026"

  edition:
    number: 1
    year: 2026
    name: "First Edition"


publication:

  author:
    - name: "[Author]"
      role: "Author"

  contributors:
    - name: "[Contributor]"
      role: "Curriculum Reviewer"

  publisher:
    name: "[Publisher]"
    location: "Papua New Guinea"

  copyright:
    holder: "[Copyright Holder]"
    year: 2026
    license: "Copyright"
    rights: "All rights reserved."

  isbn:
    print: ""
    ebook: ""


design:

  theme: primary

  page_size: A4

  orientation: portrait


content:

  curriculum: curriculum/

  units: units/

  assessments: assessments/

  answers: answers/

  references: references/


products:

  student_book: true

  teacher_guide: false

  workbook: false

  answer_book: true

  assessment_book: false


output:

  pdf: true

  epub: true

  html: true

  web: false

  kolibri: false


qa:

  strict: true

  curriculum_validation: true

  content_validation: true

  assessment_validation: true

  asset_validation: true

  accessibility_validation: true

  output_validation: true

  visual_validation: true

---

48. Configuration Validation

The publishing engine must validate "book.yml" before attempting to build the book.

Validation should check:

Required

- "book.id"
- "book.title"
- "book.grade"
- "book.subject"
- "book.language"
- "book.curriculum"
- Author
- Copyright information
- Output configuration

Valid values

- Grade
- Subject
- Book type
- Language
- Curriculum
- Page size
- Orientation
- Output types

References

- Curriculum directory exists
- Unit directory exists
- Assessment directory exists when enabled
- Answer directory exists when enabled
- Asset directories exist when referenced

---

49. Configuration Override Rules

Configuration inheritance must be predictable.

Example:

Platform Default
page_size = A4

Subject Default
theme = mathematics

Theme Default
font = Noto Sans

Book
page_size = A5

Final configuration:

page_size = A5
theme = mathematics
font = Noto Sans

The engine must document every supported override.

---

50. What Must NOT Be Stored in book.yml

"book.yml" should not become a dumping ground.

Do not place large amounts of textbook content in it.

Do not store:

- Full lessons
- Long question banks
- Large bibliographies
- Image data
- Generated PDF content
- Page-specific formatting instructions

Those belong in their appropriate source directories.

---

51. Separation of Concerns

The architecture should remain:

book.yml
    ↓
"What is this book?"

CONTENT_SCHEMA.md
    ↓
"What does the book contain?"

DESIGN_SYSTEM.md
    ↓
"How should it look?"

PUBLISHING ENGINE
    ↓
"How do we build it?"

QA_SPECIFICATION.md
    ↓
"How do we verify it?"

This separation is fundamental to platform scalability.

---

52. New Book Creation

Creating a new book should eventually require approximately:

1. Create book directory.
2. Create book.yml.
3. Select grade.
4. Select subject.
5. Select curriculum.
6. Enter publication metadata.
7. Add curriculum mapping.
8. Add units.
9. Add lessons.
10. Add assessments.
11. Add assets.
12. Run validation.
13. Build publication.
14. Review output.
15. Release.

The core publishing engine should normally remain unchanged.

---

53. Example: Creating Another Book

A Grade 6 Science textbook would become:

books/
└── grade-6/
    └── science/
        ├── book.yml
        ├── publication/
        ├── curriculum/
        ├── units/
        ├── assessments/
        ├── answers/
        ├── illustrations/
        └── references/

The engine remains the same.

Only the configuration, curriculum, subject framework, content and assets change.

---

54. Definition of Done

"BOOK_SCHEMA.md" is implemented when:

- "book.yml" has a defined schema.
- Books can identify grade and subject.
- Books can select a curriculum.
- Publication metadata can be attached.
- Authors and publishers can be defined.
- Copyright information can be defined.
- Edition information can be defined.
- Multiple book products can be configured.
- PDF/EPUB/HTML output can be selected.
- QA behaviour can be configured.
- Configuration inheritance works predictably.
- Invalid configurations are detected before publishing.

---

55. Golden Rule

A new textbook should be a configuration and content problem, not a software-development problem.

The desired future workflow is:

Create Book
    ↓
Configure book.yml
    ↓
Add Curriculum
    ↓
Add Content
    ↓
Add Assets
    ↓
Run Build
    ↓
Automated QA
    ↓
Human Review
    ↓
Publish

The platform becomes successful when a new Grade 3, Grade 4, Grade 5 or Grade 6 textbook can follow this process without rewriting the publishing engine.
