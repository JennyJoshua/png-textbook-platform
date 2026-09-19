DESIGN_SYSTEM.md

PNG Textbook Production Platform

Textbook Design System

Document: DESIGN_SYSTEM.md
Project: PNG Textbook Production Platform (PTPP)
Repository: "png-textbook-platform"
Status: Foundation Specification
Version: 1.0

---

1. Purpose

This document defines the visual design system for publications produced by the PNG Textbook Production Platform.

The design system controls:

- Page dimensions
- Margins
- Typography
- Colour
- Headings
- Lesson layouts
- Unit layouts
- Activities
- Examples
- Exercises
- Tables
- Figures
- Illustrations
- Captions
- Headers
- Footers
- Page numbering
- Covers
- Front matter
- Back matter
- Accessibility
- Print and digital presentation

The system must be reusable across grades, subjects and publication types.

---

2. Core Design Principle

Content and design must remain separate.

CONTENT
"What does the book say?"

DESIGN SYSTEM
"How should it look?"

PUBLISHING ENGINE
"How should the content be transformed into a publication?"

Authors should not manually control page formatting inside lesson content.

---

3. Design Hierarchy

Design settings follow:

Platform Design Defaults
        ↓
Theme
        ↓
Subject Theme
        ↓
Book Configuration
        ↓
Component

More specific settings override general settings.

---

4. Design Goals

The primary-school design system should produce books that are:

- Clear
- Attractive
- Child-friendly
- Professional
- Consistent
- Easy to read
- Easy to print
- Economical to produce
- Suitable for black-and-white printing where necessary
- Suitable for digital reading
- Accessible
- Appropriate for PNG primary education

Visual design must support learning rather than distract from it.

---

5. Primary Theme

The initial platform theme is:

theme:
  id: primary
  name: "Primary Education"

The primary theme should be suitable for Grades 1–6.

It should use:

- Strong visual hierarchy
- Large readable text
- Clear activity areas
- Consistent icons
- Moderate use of colour
- Clear illustrations
- Adequate whitespace

---

6. Page Size

Default:

page_size: A4
orientation: portrait

A4 is the initial default because it is practical for:

- School printing
- Photocopying
- Teacher use
- Digital PDF distribution
- Local production

Other sizes may be configured.

---

7. Supported Page Sizes

The engine should support:

A4
A5
Letter
Legal
Custom

Page dimensions should be defined centrally.

The content must not contain hard-coded page dimensions.

---

8. Page Margins

Default margins should provide sufficient space for:

- Binding
- Printing
- Notes
- Headers
- Footers

Example configuration:

margins:
  top: 18mm
  bottom: 18mm
  inside: 22mm
  outside: 18mm

Exact production values may be adjusted after prototype testing.

---

9. Print Safety

Important content must remain inside the printable area.

The publishing engine should provide:

safe area
bleed area
trim area

where relevant to professional print production.

The system should flag objects that extend outside allowed areas unless intentionally configured.

---

10. Typography

Typography should prioritize:

1. Readability
2. Availability
3. Unicode support
4. Digital compatibility
5. Print quality
6. Consistency

The initial design should use a highly readable sans-serif family.

Suggested default:

Noto Sans

The final font selection should be confirmed during implementation and tested for all required characters.

---

11. Font Families

The system should support:

typography:
  body: "Noto Sans"
  heading: "Noto Sans"
  emphasis: "Noto Sans"
  code: "Noto Sans Mono"

Fonts must be bundled or otherwise reliably available to the build system.

The platform must not depend on a font that exists only on one developer's computer.

---

12. Font Sizes

Initial guidelines:

Book title:
28–40 pt

Unit title:
24–30 pt

Lesson title:
20–26 pt

Major heading:
17–20 pt

Minor heading:
14–17 pt

Body:
11–13 pt

Caption:
9–11 pt

Footnote:
8–10 pt

Exact values should be controlled by the theme.

---

13. Body Text

Body text should have:

- Comfortable line spacing
- Adequate paragraph spacing
- Clear contrast
- Limited line length
- Consistent alignment

Default alignment:

left aligned

Full justification should only be used if it improves readability and does not create distracting spacing.

---

14. Paragraphs

Paragraphs should not normally be separated using blank lines manually.

The design engine controls:

paragraph spacing
line spacing
first-line behaviour
widows/orphans

This keeps layout consistent.

---

15. Headings

Heading hierarchy:

Book
  ↓
Part
  ↓
Unit
  ↓
Lesson
  ↓
Section
  ↓
Subsection

Example:

UNIT 1
Numbers

Lesson 1
Place Value

Teaching Content

Practice

Heading levels must remain structurally meaningful for digital formats.

---

16. Unit Opening

Every unit should have a distinct opening page or opening section.

Possible elements:

Unit number
Unit title
Unit introduction
Learning outcomes
Key vocabulary
Unit illustration

Example:

UNIT 1

NUMBER AND PLACE VALUE

In this unit you will learn to...

You will learn:
• ...
• ...
• ...

The exact appearance belongs to the theme.

---

17. Lesson Opening

Each lesson should clearly identify:

Lesson number
Lesson title
Learning objectives

Example:

LESSON 1

PLACE VALUE

Learning objectives

By the end of this lesson you should be able to:
• read numbers to 10 000;
• identify place values;
• compare numbers.

---

18. Learning Objectives Box

Objectives may be displayed using a reusable component:

┌───────────────────────────┐
│ Learning Objectives       │
│                           │
│ By the end of this lesson │
│ you will be able to...    │
└───────────────────────────┘

The component should be configurable by theme.

---

19. Vocabulary Component

Vocabulary should have a consistent visual treatment.

Example:

KEY WORDS

digit
A symbol used to write numbers.

place value
The value of a digit based on its position.

The design should distinguish the term from its definition.

---

20. Key Idea Component

Important concepts may use:

KEY IDEA

Example:

┌──────────────────────────────┐
│ KEY IDEA                     │
│ A digit's value depends on   │
│ its position in a number.    │
└──────────────────────────────┘

The component should not rely on colour alone.

---

21. Example Component

Examples should be visually distinguishable from ordinary teaching text.

Example:

EXAMPLE

What is the value of 7 in 3 742?

7 is in the hundreds place.

7 × 100 = 700

Answer: 700

---

22. Worked Example

Worked examples should visually communicate a sequence.

WORKED EXAMPLE

Step 1
...

Step 2
...

Step 3
...

Answer
...

Mathematics and science themes may have specialized versions.

---

23. Activity Component

Activities should be immediately recognizable.

Example:

ACTIVITY

Work with a partner.

1. Choose a number.
2. Write it.
3. Identify each digit's place value.
4. Explain your answer.

The activity component may include an icon or label.

---

24. Discussion Component

Example:

DISCUSS

Why do we use different units
to measure different objects?

Talk about your ideas with a partner.

---

25. Practice Component

Practice questions should be easy to identify.

Example:

PRACTICE

1. Write 4 305 in words.

2. What is the value of 6 in 6 421?

3. Complete the table.

Adequate writing space should be provided for printed workbooks where configured.

---

26. Challenge Component

Challenge activities may use a distinct visual style.

Example:

CHALLENGE

Can you find three different
four-digit numbers whose digits
add up to 15?

The visual treatment should communicate extension rather than required core content.

---

27. Assessment Component

Assessment sections should have a consistent structure.

Example:

CHECK YOUR LEARNING

1. ...
2. ...
3. ...

The student book should not reveal hidden answer metadata.

---

28. Teacher Note

Teacher-only content should use a separate component.

Example:

TEACHER NOTE

Ask learners to explain their method
before showing the worked example.

Teacher notes must not accidentally appear in student editions.

---

29. Definition Component

Definitions should be concise.

Example:

DIGIT

A symbol used to write numbers.

Definitions may automatically feed the glossary.

---

30. Tip Component

Example:

TIP

Remember to check the place of each digit
before deciding its value.

---

31. Warning Component

Warnings are particularly useful for:

- Science safety
- Common mathematical errors
- Practical activities

Example:

SAFETY

Do not taste or touch laboratory substances
unless your teacher tells you to do so.

Warnings must be visually distinguishable without depending only on colour.

---

32. Tables

Tables should have:

- Clear headings
- Adequate spacing
- Consistent borders
- Readable text
- Repeating header rows where tables span pages

The system should prevent rows from being split unnecessarily.

---

33. Figures

Figures may include:

Illustrations
Diagrams
Charts
Maps
Graphs
Photographs
Infographics

Every figure should support the learning objective or content.

Decorative graphics should not overwhelm instructional material.

---

34. Figure Captions

Example:

Figure 3. Place-value chart.

Captions should be automatically numbered where configured.

The engine should support:

Figure 1
Figure 2
Figure 3

without manually numbering them in source content.

---

35. Image Accessibility

Images should contain:

alt text

Complex images may additionally contain:

long description

The publishing engine should validate missing accessibility metadata.

---

36. Illustrations

Illustrations should be:

- Age appropriate
- Educationally relevant
- Clear
- Culturally appropriate
- Technically suitable for print
- Suitable for digital display

The system should distinguish between:

Instructional illustration
Decorative illustration
Diagram
Photograph
Chart
Map

---

37. Colour System

The primary theme should define a controlled colour palette.

Example conceptual roles:

Primary
Secondary
Accent
Background
Text
Muted
Success
Warning
Error

Exact colour values should be centralized in the theme.

Content authors should not select arbitrary colours.

---

38. Colour Accessibility

Colour combinations must provide sufficient contrast.

Information must never depend solely on colour.

For example:

Bad:

Correct answers are green.
Wrong answers are red.

Better:

✓ Correct
✗ Incorrect

Colour can reinforce meaning but must not be the only indicator.

---

39. Icons

Icons may be used for recurring components:

Activity
Discussion
Tip
Challenge
Safety
Assessment
Teacher Note

Icons must have consistent visual language.

The system should use a centralized icon set rather than individually sourced icons wherever possible.

---

40. Page Headers

Headers may contain:

Book title
Unit title
Lesson title

The exact information should depend on page type.

Front-matter pages may use no header.

---

41. Page Footers

Footers may contain:

Page number
Book short title
Copyright

The design system should permit different footer configurations for:

- Student books
- Teacher guides
- Workbooks
- Assessment books

---

42. Page Numbering

Page numbering should be generated automatically.

The publishing engine should support:

Roman numerals for front matter
Arabic numerals for main content

where appropriate.

Example:

i
ii
iii

1
2
3

---

43. Blank Pages

The engine should detect unnecessary blank pages.

Intentional blank pages may be explicitly configured.

Example:

blank_page:
  intentional: true

---

44. Page Breaks

Authors should not normally insert arbitrary page breaks.

The publishing engine should decide page flow based on content and design rules.

Explicit page breaks may be supported for:

- Unit openings
- Major sections
- Assessments
- Publication pages

---

45. Widows and Orphans

The rendering engine should minimize:

- Single lines at the top of a page
- Single lines at the bottom of a page
- Headings separated from their content
- Captions separated from figures

These should be automated wherever supported by the rendering technology.

---

46. Heading Protection

A heading should not appear alone at the bottom of a page.

Minimum rule:

Heading
+
at least one following content block

should remain together where possible.

---

47. Figure Protection

Figures and captions should normally remain together.

The system should avoid:

Page 10:
[Figure]

Page 11:
Figure 4. Caption

unless unavoidable.

---

48. Exercise Layout

Exercise pages should provide appropriate space.

Configuration may support:

exercise:
  answer_space: compact

or:

exercise:
  answer_space: generous

This is particularly important for workbook publications.

---

49. Mathematics Layout

Mathematical expressions should receive special treatment.

The system should support:

- Fractions
- Exponents
- Equations
- Number lines
- Tables
- Shapes
- Geometry
- Long calculations
- Mathematical symbols

Mathematics should remain machine-readable where practical.

---

50. Science Layout

Science pages may use specialized components for:

Investigation
Materials
Method
Observation
Results
Conclusion
Safety

These components should follow the same overall design language as mathematics and other subjects.

---

51. English Layout

English books may use specialized components for:

Reading
Vocabulary
Grammar
Writing
Speaking
Listening
Comprehension

Long reading passages should have a comfortable text layout.

---

52. Maps

Maps should include appropriate:

- Title
- Legend
- Labels
- Scale where required
- Orientation where useful
- Source/attribution where required

The map design should be optimized for both print and digital output.

---

53. Charts and Graphs

Charts should have:

- Clear labels
- Units
- Titles where appropriate
- Legible axes
- Accessible representation

The system should not rely solely on colour to distinguish data series.

---

54. Cover Design

The cover should include configurable elements:

Book title
Subtitle
Grade
Subject
Author
Publisher
Edition
Main illustration

Example conceptual structure:

┌─────────────────────────────┐
│                             │
│       GRADE 4               │
│       MATHEMATICS            │
│                             │
│     [MAIN ILLUSTRATION]     │
│                             │
│       [Author]              │
│       [Publisher]           │
│                             │
└─────────────────────────────┘

The actual cover design belongs to the selected theme.

---

55. Spine and Back Cover

The system should eventually support print-cover layouts containing:

Front Cover
Spine
Back Cover

where required.

Back cover metadata may include:

- Short description
- Author
- Publisher
- ISBN
- Barcode placeholder
- Website
- Edition

---

56. Front Matter Design

Front matter should have a consistent hierarchy:

Cover
Title Page
Copyright Page
Acknowledgements
Contents
Preface / Introduction

Not every publication requires every component.

---

57. Table of Contents

The TOC should be generated automatically from document structure.

Example:

CONTENTS

Unit 1 Numbers .................... 1
  Lesson 1 Place Value ........... 3
  Lesson 2 Comparing Numbers ..... 8

Unit 2 Addition .................. 15

Page numbers must never be typed manually.

---

58. Cross-References

Cross-references should use stable content IDs.

For example:

See Lesson G4-MATH-L03.

The rendering engine may display:

See Lesson 3, Comparing Numbers.

Page references should be generated automatically where supported.

---

59. Glossary Design

Glossary entries should be automatically formatted.

Example:

GLOSSARY

digit
A symbol used to write numbers.

place value
The value of a digit based on its position.

Alphabetical ordering should be automatic.

---

60. Answer Section Design

Answer sections should be clearly separated from student content.

Example:

ANSWERS

Unit 1

Lesson 1
1. 700
2. 2
3. 3 427

Answer formatting may differ depending on the product type.

---

61. Teacher Guide Design

Teacher guides should retain the visual identity of the student book while clearly distinguishing teacher-only information.

Possible components:

Teaching Notes
Suggested Questions
Common Misconceptions
Answers
Differentiation
Assessment Guidance
Materials

---

62. Workbook Design

Workbooks should prioritize writing space.

The workbook theme may use:

Larger answer areas
Activity boxes
Writing lines
Grid spaces
Tables
Check boxes

The same core design system should be reused.

---

63. Assessment Book Design

Assessment publications should prioritize:

- Clear instructions
- Question numbering
- Adequate answer space
- Mark allocation where appropriate
- Clean pages
- Minimal distraction

---

64. Digital Design

Digital outputs should adapt to screen reading.

The source content must not assume:

- Fixed page width
- Printed page numbers
- Physical page turning
- Left/right page relationships

Responsive HTML and EPUB layouts should use the same design language while adapting to screen size.

---

65. Print vs Digital

The platform should treat:

PRINT DESIGN

and:

DIGITAL DESIGN

as related themes rather than forcing identical layouts.

Example:

Same:
Typography
Colours
Component identity
Heading hierarchy

Different:
Page dimensions
Navigation
Screen spacing
Interactive elements

---

66. Theme Configuration

Themes should be stored under:

framework/
└── themes/
    └── primary/
        ├── theme.yml
        ├── typography.yml
        ├── colours.yml
        ├── components.yml
        ├── page-layout.yml
        └── cover.yml

---

67. Example Theme Configuration

theme:
  id: primary
  name: "Primary Education"

page:
  size: A4
  orientation: portrait

typography:
  body: "Noto Sans"
  heading: "Noto Sans"

components:
  objectives: true
  vocabulary: true
  example: true
  activity: true
  challenge: true
  assessment: true

accessibility:
  minimum_contrast: true
  require_alt_text: true

---

68. Subject Themes

Subject frameworks may extend the primary theme.

Example:

framework/
├── themes/
│   └── primary/
│
└── subjects/
    ├── mathematics/
    │   └── design/
    ├── english/
    │   └── design/
    └── science/
        └── design/

Subject extensions should not create completely unrelated visual systems.

---

69. Design Tokens

The system should eventually use centralized design tokens.

Example:

spacing:
  xs: 2mm
  sm: 4mm
  md: 8mm
  lg: 12mm
  xl: 18mm

radius:
  small: 2mm
  medium: 4mm

border:
  thin: 0.5pt

This allows global design changes without editing individual lessons.

---

70. No Manual Page Formatting

The following should generally be prohibited in source content:

Manual page numbers
Manual headers
Manual footers
Manual font sizes
Manual margin instructions
Manual table-of-contents page numbers
Absolute positioning
Hard-coded page coordinates

These belong to the publishing system.

---

71. Design Validation

The QA system should check:

- Missing fonts
- Unsupported characters
- Overflow
- Clipped text
- Broken figures
- Missing captions
- Poor page breaks
- Empty pages
- Heading isolation
- Figure/caption separation
- Table overflow
- Inconsistent numbering
- Missing page numbers
- Contrast problems
- Missing alt text

---

72. Visual QA

Every production release should include visual inspection.

Recommended process:

Build PDF
    ↓
Render pages to images
    ↓
Generate contact sheet
    ↓
Inspect representative pages
    ↓
Inspect flagged pages
    ↓
Correct source/design
    ↓
Rebuild

Visual QA should cover:

- Cover
- Front matter
- Unit opening
- Normal lesson
- Activity page
- Example page
- Table-heavy page
- Illustration-heavy page
- Assessment page
- Answer page
- Final page

---

73. Design Review

A book should be reviewed at three levels:

Level 1 — System

Is the design system internally consistent?

Level 2 — Book

Does the book maintain consistent visual hierarchy?

Level 3 — Page

Does each page render correctly?

---

74. Design Change Management

Design changes should be centralized.

For example:

Change body font

should require changing the theme configuration, not editing hundreds of lessons.

Similarly:

Change activity box design

should modify the activity component/theme rather than every activity.

---

75. Reusability

The same design system should support:

Grade 1 Mathematics
Grade 2 Mathematics
Grade 4 Mathematics
Grade 6 Science
Grade 5 English
Teacher Guides
Workbooks
Assessment Books

without creating a separate design engine for each book.

---

76. Definition of Done

"DESIGN_SYSTEM.md" is implemented when:

- Page sizes are configurable.
- Margins are centrally controlled.
- Typography is centrally controlled.
- Themes are reusable.
- Colours are centralized.
- Headings are structured.
- Units have consistent openings.
- Lessons have consistent openings.
- Activities use reusable components.
- Examples use reusable components.
- Tables are styled consistently.
- Figures and captions are managed automatically.
- Headers and footers are generated automatically.
- Page numbering is automatic.
- TOC generation is automatic.
- Accessibility requirements are validated.
- Print and digital layouts can share the same content.
- Visual QA can identify layout problems.

---

77. Golden Rule

The design system should make it possible to say:

«Write the content once, then let the platform consistently turn it into a professional textbook.»

Therefore:

AUTHOR
  ↓
Structured Content
  ↓
DESIGN SYSTEM
  ↓
PUBLISHING ENGINE
  ↓
Consistent Publication

A new textbook should not require manually designing hundreds of pages.

The platform should design them automatically.
