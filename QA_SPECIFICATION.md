QA Specification

PNG Textbook Production Platform (PTPP)

Repository: "png-textbook-platform"
Document: "QA_SPECIFICATION.md"
Status: Initial Specification
Version: 1.0

---

1. Purpose

This document defines the Quality Assurance (QA) system for the PNG Textbook Production Platform.

The QA system must automatically check textbook source content, curriculum alignment, assessments, assets, publication metadata, accessibility, generated outputs, and visual layout before a textbook is released.

The goal is to make textbook production repeatable, testable, and auditable, similar to software development.

A textbook should not be considered ready for publication simply because it has been written.

It must pass defined quality checks.

---

2. Core QA Principle

The platform follows:

«Write → Validate → Build → Test → Review → Release»

The publishing system must distinguish between:

- Errors
- Warnings
- Informational messages
- Human-review requirements

Automated QA supports human review. It does not replace educational, editorial, legal, or professional judgment.

---

3. QA Pipeline

The standard QA pipeline is:

Source Content
      ↓
Schema Validation
      ↓
Curriculum Validation
      ↓
Content Validation
      ↓
Assessment Validation
      ↓
Asset Validation
      ↓
Publication Validation
      ↓
Accessibility Validation
      ↓
Build
      ↓
PDF/EPUB/HTML Validation
      ↓
Visual QA
      ↓
QA Report
      ↓
Release Decision

---

4. QA Levels

The platform should support the following QA levels.

4.1 Level 1 — Source QA

Checks the source files before publishing.

Examples:

- YAML syntax
- Markdown structure
- required fields
- duplicate IDs
- invalid references
- missing files
- invalid configuration

---

4.2 Level 2 — Educational QA

Checks educational structure and curriculum traceability.

Examples:

- lessons linked to curriculum outcomes
- learning objectives present
- appropriate assessment coverage
- unit structure complete
- grade and subject consistency

---

4.3 Level 3 — Technical QA

Checks generated outputs.

Examples:

- PDF generated successfully
- EPUB generated successfully
- no missing images
- no broken internal links
- no unresolved references
- metadata present

---

4.4 Level 4 — Visual QA

Checks the appearance of the generated publication.

Examples:

- overflowing text
- clipped figures
- broken tables
- poor page breaks
- headings stranded at page bottoms
- blank pages
- inconsistent spacing
- incorrect numbering
- unreadable diagrams

---

4.5 Level 5 — Human QA

Human review remains mandatory for:

- factual accuracy
- curriculum suitability
- cultural appropriateness
- language quality
- pedagogical quality
- illustrations
- sensitive content
- copyright/legal suitability
- final publication approval

---

5. Severity Levels

Every QA finding should have a severity.

ERROR

A condition that normally prevents release.

Examples:

Missing required lesson ID
Invalid curriculum reference
Broken image
Duplicate question ID
PDF generation failure
Missing required answer

---

WARNING

A condition that should be reviewed but may not prevent release.

Examples:

Missing ISBN
Long lesson without activity
Low assessment coverage
Missing image attribution
Very long paragraph
Potentially inconsistent terminology

---

INFO

Useful information that does not indicate a problem.

Examples:

24 lessons processed
180 questions validated
32 illustrations found
PDF generated successfully

---

HUMAN_REVIEW

A condition that cannot reliably be decided automatically.

Examples:

Curriculum interpretation requires review
Illustration culturally appropriate?
Question pedagogically appropriate?
AI-generated image suitable?
Language appropriate for grade?

---

6. QA Configuration

QA should be configurable through "book.yml".

Example:

qa:
  strict: true

  curriculum_validation: true
  content_validation: true
  assessment_validation: true
  asset_validation: true
  publication_validation: true
  accessibility_validation: true
  output_validation: true
  visual_validation: true

  fail_on:
    - error

  warn_on:
    - warning

Development builds may allow warnings.

Release builds should normally fail on errors.

---

7. Source Validation

7.1 Configuration Validation

The platform must validate:

- "book.yml"
- publication metadata
- theme configuration
- subject configuration
- unit configuration
- lesson metadata

Required fields must be present.

Invalid values must be reported.

---

7.2 YAML Validation

The system must detect:

- invalid YAML
- malformed lists
- malformed objects
- incorrect data types
- missing required keys

Example error:

ERROR:
books/grade-4/mathematics/book.yml

Field:
book.grade

Problem:
Expected integer but received "Grade Four".

---

8. ID Validation

All structured entities require stable IDs.

The system must detect:

- duplicate IDs
- missing IDs
- invalid ID formats
- references to nonexistent IDs

Entities include:

Books
Units
Lessons
Curriculum outcomes
Questions
Figures
Activities
Assessments

Example:

ERROR: Duplicate lesson ID G4-MATH-L05
Files:
unit-02/lesson-03.md
unit-03/lesson-01.md

---

9. Content Structure Validation

Each lesson should contain the required structural elements defined by the content schema.

Example:

required:
  - objectives
  - teaching_content
  - activities
  - practice
  - summary

Optional sections may include:

Vocabulary
Examples
Challenge
Assessment
Teacher Note
Reflection

The validator should distinguish between required and optional components.

---

10. Lesson Validation

For every lesson check:

- valid ID
- title present
- grade present
- subject present
- unit reference valid
- curriculum reference present
- objectives present
- content present
- activities present where required
- assessment opportunity present where required
- summary present
- no empty sections

Example:

ERROR:
G4-MATH-L08

Missing:
curriculum mapping

WARNING:
G4-MATH-L08

No challenge activity defined.

---

11. Unit Validation

Every unit should contain:

- valid unit ID
- title
- grade
- subject
- sequence
- curriculum mapping
- lessons
- overview

Optional:

- unit assessment
- review
- project
- extension activities

The validator must check lesson ordering.

Example:

WARNING:
Unit 3 lesson sequence is:

1
2
4
5

Lesson 3 is missing.

---

12. Curriculum Validation

Curriculum alignment is a core feature of the platform.

Every curriculum-linked lesson should reference valid curriculum IDs.

Example:

curriculum:
  - MATH-G4-NUM-001
  - MATH-G4-NUM-002

The system checks:

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

---

13. Curriculum Coverage Analysis

The QA system should generate a curriculum coverage report.

Example:

PNG Grade 4 Mathematics

Curriculum outcomes: 48

Covered:
44

Partially covered:
3

Not covered:
1

Coverage:
91.7%

The platform should report coverage, not automatically declare educational adequacy.

Human review is required for curriculum interpretation.

---

14. Curriculum Traceability

The platform should allow each assessment question to be traced back to the relevant curriculum requirement.

Example:

MATH-G4-NUM-001
        ↓
Unit 1
        ↓
Lesson 3
        ↓
Practice Exercise
        ↓
Question Q-G4-MATH-034

This allows curriculum audits and future revision.

---

15. Content Quality Checks

Automated content checks should identify potential problems such as:

- empty paragraphs
- repeated headings
- excessive repetition
- suspiciously short lessons
- extremely long paragraphs
- malformed lists
- unresolved placeholders
- accidental draft text
- TODO markers
- internal comments accidentally included

Search for:

TODO
FIXME
TBD
[INSERT]
[IMAGE]
[CHECK]
DRAFT
PLACEHOLDER

These should normally generate errors or warnings before release.

---

16. Language Checks

Where practical, the platform may check:

- spelling
- repeated words
- sentence length
- paragraph length
- heading consistency
- terminology consistency
- capitalization
- punctuation

Automated language checking should be treated as advisory.

It must not automatically rewrite educational content during QA.

---

17. Mathematics Validation

Mathematics requires additional QA.

Where questions contain computable answers, the system should validate:

- arithmetic
- equations
- numerical answers
- units
- percentages
- fractions
- simple algebra where supported

Example:

question:
  text: "What is 24 × 6?"

answer:
  value: 144

The validator can calculate:

24 × 6 = 144

and compare the result.

If the stored answer differs:

ERROR:
Question Q-G4-MATH-021

Expected:
144

Stored answer:
154

---

18. Mathematics Answer Consistency

The platform should check consistency between:

- question
- student answer
- answer key
- teacher guide
- workbook
- assessment output

The same source question should not produce contradictory answers in different publications.

---

19. Assessment Validation

Assessment questions must contain required fields.

Example:

id: Q-G4-MATH-001
type: multiple_choice
grade: 4
subject: mathematics
curriculum:
  - MATH-G4-NUM-001
question: "..."
options:
  - "..."
  - "..."
  - "..."
  - "..."
answer: "..."
difficulty: medium
marks: 1

Checks include:

- valid question ID
- valid question type
- curriculum mapping
- question text
- answer
- options where required
- valid answer
- marks
- difficulty where required

---

20. Question-Type Validation

The validator should apply different rules to different question types.

Multiple Choice

Check:

- at least two options
- exactly one correct answer unless configured otherwise
- correct answer exists in options

Multiple Select

Check:

- multiple valid answers permitted
- all correct answers exist in options

True/False

Check:

- answer is true or false

Numeric

Check:

- numeric answer
- acceptable tolerance where configured

Matching

Check:

- matching pairs are complete
- no orphan entries

Ordering

Check:

- all items included
- ordering answer valid

Fill Blank

Check:

- expected answer exists

Extended Response

Check:

- marking guidance or model answer exists where required

---

21. Assessment Coverage

The platform should analyse whether curriculum outcomes are represented in assessments.

Example:

Outcome MATH-G4-NUM-001

Lessons:
6

Assessment questions:
12

Assessment coverage:
Present

The system should flag outcomes that have substantial teaching content but no corresponding assessment opportunity.

---

22. Difficulty Distribution

Where difficulty levels are defined, QA should report the distribution.

Example:

Easy:       40%
Medium:     45%
Difficult:  15%

The platform should report the distribution rather than automatically deciding whether it is pedagogically correct.

---

23. Asset Validation

Every asset must have metadata.

Example:

id: FIG-G4-MATH-001
filename: place-value-chart.png
description: "Place value chart for numbers to 10 000"
source: original
creator: "[Author]"
license: "Copyright"

Checks include:

- file exists
- valid filename
- supported format
- metadata exists
- description exists
- licensing information exists
- asset reference resolves correctly

---

24. Missing Asset Detection

The build must detect references to missing assets.

Example:

ERROR:
Lesson G4-MATH-L04 references:

figures/place-value-chart.png

File not found.

The build must not silently substitute missing assets.

---

25. Asset Licensing

The platform must distinguish between:

Original
Third-party
Public Domain
Creative Commons
Licensed
AI-generated
Photograph
Government resource
Unknown

Unknown licensing status should generate an error for release builds when the asset is included in the publication.

The platform must not make unsupported legal conclusions about whether an asset is legally usable.

---

26. AI-Generated Assets

AI-generated illustrations may be used where appropriate.

The platform should retain internal metadata identifying:

- asset
- generation status
- creation method
- creator/project
- date where available
- licensing/rights information where applicable

Human review remains required.

---

27. Publication Metadata Validation

Check:

- author
- publisher
- copyright holder
- copyright year
- rights statement
- edition
- acknowledgements where required
- credits where required

Example:

ERROR:
Copyright holder is missing.

WARNING:
ISBN has not been supplied.

ISBN must never be invented by the system.

---

28. Publication Consistency

The following information must remain consistent across:

- "book.yml"
- title page
- copyright page
- cover
- PDF metadata
- EPUB metadata
- website metadata

Examples:

Title
Author
Publisher
Edition
Copyright year

A mismatch should generate an error.

---

29. Accessibility Validation

The platform should check:

- images have alt text
- complex figures have descriptions where appropriate
- tables have meaningful headings
- links have meaningful labels
- information is not conveyed through colour alone
- text remains readable
- headings follow logical hierarchy
- digital output contains appropriate accessibility metadata where supported

Example:

ERROR:
Figure FIG-G4-SCI-004 has no alt text.

---

30. PDF Validation

Generated PDFs should be checked for:

- successful generation
- page count
- readable metadata
- embedded fonts where required
- missing fonts
- missing images
- broken links
- unresolved references
- blank pages
- corrupted pages
- correct page numbering
- correct table of contents
- correct bookmarks where supported

---

31. EPUB Validation

Generated EPUB files should be checked for:

- valid EPUB structure
- valid metadata
- valid navigation
- valid internal links
- valid images
- valid XHTML/content
- valid CSS
- missing resources
- malformed package files

The platform should use an EPUB validation tool where available.

---

32. Cross-Reference Validation

The platform must validate references such as:

See Figure 3.2
See Activity 4
See Lesson 7
See page XX
See Question Q-G4-MATH-012

No unresolved references should remain in a release build.

Temporary placeholders such as:

page XX
Figure TBD
Question TBD

must fail release QA.

---

33. Numbering Validation

Automatically validate:

- unit numbers
- lesson numbers
- activity numbers
- question numbers
- figure numbers
- table numbers
- page numbers

The system should detect:

- duplicates
- missing numbers
- unexpected resets
- inconsistent references

---

34. Table Validation

Check:

- table has headings
- rows are structurally valid
- no missing cells where prohibited
- table fits within page constraints
- table is not unnecessarily split
- table remains readable

Visual QA must inspect complex tables.

---

35. Figure Validation

Check:

- figure exists
- figure reference exists
- caption exists where required
- alt text exists
- image resolution is adequate
- image is not distorted
- image fits page boundaries

---

36. Visual QA

Visual QA is mandatory for release builds.

The system should:

1. Generate PDF.
2. Render PDF pages to images.
3. Generate a contact sheet.
4. Identify representative pages.
5. Flag suspicious pages.
6. Allow human inspection.
7. Record findings.

Representative pages should include:

- cover
- title page
- copyright page
- contents
- unit opening
- lesson opening
- text-heavy page
- activity page
- table-heavy page
- figure-heavy page
- assessment page
- answer page
- final page

---

37. Visual Problems to Detect

The platform should attempt to identify:

- text overflow
- clipped text
- clipped images
- overlapping objects
- orphan headings
- excessive white space
- awkward page breaks
- broken tables
- distorted images
- inconsistent margins
- inconsistent typography
- incorrect headers
- incorrect footers
- missing page numbers
- blank pages
- extremely dense pages

Automated visual detection is advisory where detection is unreliable.

Human inspection remains the final authority.

---

38. Print QA

For print-oriented books, QA should check:

- page size
- margins
- bleed where applicable
- safe areas
- image resolution
- colour configuration where supported
- page numbering
- front/back matter
- blank-page handling
- cover dimensions

The actual printer's technical requirements should override platform defaults.

---

39. Digital QA

For digital editions, QA should check:

- responsive layout
- readable text
- navigation
- hyperlinks
- image scaling
- metadata
- accessibility
- EPUB structure
- device-independent rendering where possible

---

40. Build Reproducibility

A textbook build should be reproducible.

Given the same:

Source
+
Configuration
+
Framework version
+
Theme version
+
Assets

the platform should produce the same publication structure.

Build information should record:

build:
  platform_version: "..."
  book_version: "..."
  build_date: "..."
  git_commit: "..."

---

41. QA Report

Every build should generate a machine-readable QA report.

Example:

qa:
  status: passed

  errors: 0
  warnings: 4
  human_review: 8

  checks:
    source: passed
    curriculum: passed
    content: passed
    assessments: passed
    assets: passed
    publication: passed
    accessibility: passed
    pdf: passed
    epub: passed
    visual: review_required

A human-readable report should also be generated.

---

42. Example QA Report

PNG TEXTBOOK PRODUCTION PLATFORM
QA REPORT

Book:
Grade 4 Mathematics

Build:
v0.9

STATUS:
PASS WITH WARNINGS

--------------------------------
SOURCE
--------------------------------
Errors: 0
Warnings: 1

--------------------------------
CURRICULUM
--------------------------------
Errors: 0
Warnings: 2

Coverage: 94%

--------------------------------
CONTENT
--------------------------------
Errors: 0
Warnings: 3

--------------------------------
ASSESSMENTS
--------------------------------
Errors: 0
Warnings: 1

Questions: 184

--------------------------------
ASSETS
--------------------------------
Errors: 0
Warnings: 2

Assets: 73

--------------------------------
PUBLICATION
--------------------------------
Errors: 0
Warnings: 1

--------------------------------
ACCESSIBILITY
--------------------------------
Errors: 0
Warnings: 2

--------------------------------
PDF
--------------------------------
PASS

Pages: 168

--------------------------------
EPUB
--------------------------------
PASS

--------------------------------
VISUAL REVIEW
--------------------------------
Human review required.

--------------------------------
RELEASE
--------------------------------
NOT YET APPROVED

Reason:
Human visual and educational review required.

---

43. Release Gates

A publication may proceed to release only when:

Critical errors = 0
Required validation = passed
Required human review = completed
Visual review = completed
Publication metadata = approved
Assets = approved

Warnings may remain if they have been reviewed and accepted.

---

44. QA Status

The platform should use standardized statuses:

NOT_STARTED
RUNNING
FAILED
PASSED
PASSED_WITH_WARNINGS
HUMAN_REVIEW_REQUIRED
APPROVED_FOR_RELEASE
RELEASED

---

45. CI/CD Integration

QA should eventually run automatically through GitHub workflows.

Example:

Developer/Author changes content
        ↓
Git commit
        ↓
GitHub
        ↓
QA workflow
        ↓
Validation
        ↓
Build
        ↓
PDF/EPUB generation
        ↓
QA report
        ↓
Pass / Fail

A pull request containing a critical textbook error should be prevented from being merged into "main".

---

46. Local QA

The same QA system should be runnable locally.

Example future commands:

python scripts/qa.py

or:

python scripts/qa.py books/grade-4/mathematics

Possible commands:

python scripts/validate.py
python scripts/build.py
python scripts/qa.py
python scripts/visual_qa.py

Exact implementation is determined during the engineering phase.

---

47. Human Review Checklist

Automated QA must be supplemented by a human checklist.

Curriculum

- [ ] Curriculum interpretation is correct
- [ ] Content covers intended outcomes
- [ ] Sequence is appropriate
- [ ] Grade level is appropriate

Educational Quality

- [ ] Explanations are accurate
- [ ] Examples are correct
- [ ] Activities are meaningful
- [ ] Assessments measure intended learning
- [ ] Difficulty is appropriate

Language

- [ ] Language is clear
- [ ] Grammar is correct
- [ ] Vocabulary is appropriate
- [ ] Instructions are understandable

Cultural Context

- [ ] Examples are culturally appropriate
- [ ] Images are appropriate
- [ ] Local context is represented appropriately
- [ ] No inappropriate assumptions are present

Visual Design

- [ ] Pages are readable
- [ ] Illustrations are appropriate
- [ ] Tables work correctly
- [ ] No clipping or overlap
- [ ] Page flow is logical

Publication

- [ ] Author information correct
- [ ] Publisher information correct
- [ ] Copyright information correct
- [ ] Edition correct
- [ ] Credits correct
- [ ] Asset rights reviewed

---

48. QA and AI

AI may assist with:

- detecting inconsistencies
- identifying missing content
- checking terminology
- checking mathematics
- generating QA suggestions
- comparing curriculum mappings
- identifying possible duplicate questions
- reviewing readability
- identifying suspicious content

AI must not silently change source content during QA.

Any substantive change must be proposed and reviewed.

---

49. QA as a Feedback Loop

QA is not only a final gate.

The intended workflow is:

Draft
 ↓
QA
 ↓
Identify problems
 ↓
Revise
 ↓
QA
 ↓
Build
 ↓
Visual Review
 ↓
Revise
 ↓
Final QA
 ↓
Release

This allows the textbook to improve iteratively.

---

50. Future QA Capabilities

The architecture should allow future additions including:

- automated plagiarism/similarity checking
- terminology consistency checking
- reading-level analysis
- curriculum coverage dashboards
- advanced mathematics symbolic checking
- science formula validation
- question-quality analysis
- answer-key consistency checking
- translation QA
- multilingual consistency checking
- accessibility scoring
- print preflight
- automated visual anomaly detection
- AI-assisted editorial review
- teacher review workflows
- curriculum reviewer approval workflows

These are future extensions and should not complicate the initial implementation unnecessarily.

---

51. Initial QA Implementation Priority

The first implementation should focus on:

Phase 1 — Essential

1. YAML/schema validation
2. Book configuration validation
3. Duplicate ID detection
4. Missing file detection
5. Curriculum reference validation
6. Lesson structure validation
7. Assessment validation
8. Asset reference validation
9. Publication metadata validation
10. PDF build validation

Phase 2

11. Mathematics answer validation
12. Assessment coverage
13. Accessibility checks
14. EPUB validation
15. Cross-reference validation
16. Numbering validation

Phase 3

17. Automated visual analysis
18. Curriculum coverage reports
19. Advanced language QA
20. Advanced assessment analysis
21. AI-assisted QA

---

52. QA Definition of Done

The QA system is considered complete when it can:

- validate book configuration
- validate content schemas
- detect duplicate IDs
- detect missing references
- validate curriculum mappings
- validate lesson structures
- validate assessment questions
- validate answer keys
- validate mathematics where supported
- validate assets
- validate asset licensing metadata
- validate publication metadata
- check accessibility requirements
- build PDF
- build EPUB
- validate generated outputs
- detect unresolved references
- generate a QA report
- distinguish errors from warnings
- support human review
- support release gates
- run locally
- run automatically through GitHub CI
- record the build/version information

---

53. Golden Rule

«No textbook is released directly from AI-generated content.»

AI may accelerate planning, writing, design, checking, and production.

The platform must provide the structure, traceability, validation, and reproducibility required to turn that work into a professional educational publication.

The final authority remains the author, editor, curriculum reviewer, and publisher.

---

54. Relationship to Other Platform Documents

This specification works together with:

PROJECT_REQUIREMENTS.md
ARCHITECTURE.md
CONTENT_SCHEMA.md
BOOK_SCHEMA.md
PUBLICATION_SCHEMA.md
DESIGN_SYSTEM.md

Future engineering documents should implement the requirements defined here rather than creating independent QA rules.

---

55. Final Architecture Principle

The textbook platform should make quality assurance a built-in property of the publishing process, not a final manual inspection.

                 TEXTBOOK SOURCE
                       │
                       ▼
              ┌──────────────────┐
              │   VALIDATION     │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │      BUILD       │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │   OUTPUT QA      │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │   VISUAL QA      │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │  HUMAN REVIEW    │
              └────────┬─────────┘
                       │
                       ▼
                    RELEASE

Core principle:

«The platform should make it difficult to accidentally publish a bad textbook.»
