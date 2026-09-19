PUBLICATION_SCHEMA.md

PNG Textbook Production Platform

Publication Metadata Schema

Document: PUBLICATION_SCHEMA.md
Project: PNG Textbook Production Platform (PTPP)
Repository: "png-textbook-platform"
Status: Foundation Specification
Version: 1.0

---

1. Purpose

This document defines the standard publication metadata used by textbooks and related educational publications produced by the PNG Textbook Production Platform.

Publication metadata describes the publication and its ownership, rather than the educational content itself.

It includes:

- Author
- Publisher
- Copyright holder
- Copyright year
- License
- Edition
- ISBN
- Contributors
- Editors
- Illustrators
- Acknowledgements
- Credits
- Publication identifiers
- Publication statements

---

2. Separation of Concerns

The platform separates:

CONTENT
"What does the book teach?"

BOOK CONFIGURATION
"What is this particular book?"

PUBLICATION METADATA
"Who created, owns and publishes it?"

DESIGN SYSTEM
"How is it presented?"

PUBLISHING ENGINE
"How is it produced?"

Publication information must not be hard-coded into the publishing engine.

---

3. Publication Directory

Each book may contain:

publication/
├── author.yml
├── publisher.yml
├── copyright.yml
├── edition.yml
├── credits.yml
└── acknowledgements.md

Example:

books/
└── grade-4/
    └── mathematics/
        ├── book.yml
        ├── publication/
        │   ├── author.yml
        │   ├── publisher.yml
        │   ├── copyright.yml
        │   ├── edition.yml
        │   ├── credits.yml
        │   └── acknowledgements.md
        ├── curriculum/
        ├── units/
        └── assessments/

---

4. Publication Metadata Object

The complete publication metadata may be represented as:

publication:

  author:
    - name: "[Author]"
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
    year: 2026
    name: "First Edition"

  isbn:
    print: ""
    ebook: ""

  credits:
    editor: []
    illustrator: []
    designer: []
    reviewer: []

  acknowledgements: ""

---

5. Author Schema

Authors are the primary creators of the educational publication.

Example:

author:
  - name: "[Author]"
    role: "Author"

Multiple authors:

author:
  - name: "[Author 1]"
    role: "Author"

  - name: "[Author 2]"
    role: "Author"

---

6. Author Fields

Supported fields:

Field| Required| Description
"name"| Yes| Author's published name
"role"| Yes| Author role
"organization"| Optional| Associated organization
"bio"| Optional| Short publication biography
"order"| Optional| Display order

Example:

author:
  - name: "[Author]"
    role: "Author"
    organization: "[Organization]"
    order: 1

Only information intended for publication should be included.

---

7. Author Display Name

The name stored in the publication metadata is the name that may appear in the book.

The system must not assume that a person's legal name, account name, or GitHub username is the correct publication name.

The author explicitly controls the published author name.

---

8. Publisher Schema

Example:

publisher:
  name: "[Publisher]"
  location: "Papua New Guinea"

Extended version:

publisher:
  name: "[Publisher]"
  location: "Papua New Guinea"
  city: "Port Moresby"
  country: "PG"

---

9. Publisher Fields

Field| Required| Description
"name"| Yes| Publisher name
"location"| Optional| General publisher location
"city"| Optional| City
"country"| Optional| Country
"website"| Optional| Official publication website
"email"| Optional| Publication contact

Only public-facing contact information should be included.

---

10. Copyright Schema

The initial project default is:

copyright:
  holder: "[Copyright Holder]"
  year: 2026
  license: "Copyright"
  rights: "All rights reserved."

This means the publication is initially treated as a standard copyrighted work.

---

11. Copyright Holder

The copyright holder may be:

- The author
- A publisher
- An organization
- Multiple rights holders

Example:

copyright:
  holder: "[Copyright Holder]"

Multiple holders:

copyright:
  holders:
    - "[Copyright Holder 1]"
    - "[Copyright Holder 2]"

The publishing engine must support both forms where required.

---

12. Copyright Year

Example:

copyright:
  year: 2026

For later editions:

copyright:
  year: 2028

The year must be explicit rather than automatically inferred from the current system date.

---

13. Copyright Statement

The publishing engine should generate a standard statement from the metadata.

Example output:

Copyright © 2026 [Copyright Holder]

All rights reserved.

The actual wording should be controlled by the publication template.

---

14. Rights Statement

Example:

rights: "All rights reserved."

This should be displayed in the copyright/publication information section.

The system should allow custom rights statements where necessary.

---

15. License

The license field identifies the legal distribution terms.

Initial default:

license: "Copyright"

The platform should support:

Copyright
CC BY
CC BY-SA
CC BY-NC
CC BY-NC-SA
Public Domain
Custom

The engine must not silently change a book's license.

---

16. Custom License

A custom license may be defined as:

license:
  type: custom
  name: "Custom Educational License"
  file: publication/license.md

The complete license should be stored separately when it is too long for YAML.

---

17. Edition Schema

Example:

edition:
  number: 1
  year: 2026
  name: "First Edition"

Possible later editions:

edition:
  number: 2
  year: 2028
  name: "Second Edition"

---

18. Edition Statement

The publishing engine should generate an edition statement automatically.

Example:

First Edition, 2026

or:

Second Edition, 2028

The author/publisher should be able to override the display wording if required.

---

19. ISBN

ISBN information is optional during development.

Example:

isbn:
  print: ""
  ebook: ""

When assigned:

isbn:
  print: "978-..."
  ebook: "978-..."

The platform must not generate or guess ISBNs.

---

20. Multiple ISBNs

Different publication formats may have different ISBNs.

Example:

isbn:
  print: "978-..."
  ebook: "978-..."
  epub: "978-..."

If a publication does not have an ISBN, the field may remain empty.

---

21. Other Identifiers

The publication may have internal identifiers.

Example:

identifiers:
  publication_id: "PTPP-G4-MATH-001"
  edition_id: "PTPP-G4-MATH-001-E1"

These are separate from externally assigned identifiers such as ISBN.

---

22. Contributors

Contributors who are not primary authors should be listed separately.

Example:

contributors:

  - name: "[Contributor]"
    role: "Curriculum Reviewer"

  - name: "[Contributor]"
    role: "Subject Reviewer"

Possible roles:

Curriculum Reviewer
Subject Reviewer
Technical Reviewer
Educational Consultant
Contributor
Researcher
Translator
Proofreader

---

23. Editor

Editors may be represented separately.

editors:

  - name: "[Editor]"
    role: "Editor"

  - name: "[Editor]"
    role: "Copy Editor"

The distinction between author and editor must be retained.

---

24. Illustrator

Illustrators:

illustrators:

  - name: "[Illustrator]"
    role: "Illustrator"

For individual illustrations, the asset metadata may identify the specific creator.

---

25. Designer

Publication design credits:

designers:

  - name: "[Designer]"
    role: "Book Designer"

The publishing engine may automatically include the designer credit where configured.

---

26. Reviewer

Reviewers may include:

reviewers:

  - name: "[Reviewer]"
    role: "Curriculum Reviewer"

  - name: "[Reviewer]"
    role: "Subject Reviewer"

Reviewer information should only be published if the relevant person/organization has agreed to publication of the credit.

---

27. Credits Schema

A combined credits file may be used:

credits:

  editor:
    - name: "[Editor]"

  illustrator:
    - name: "[Illustrator]"

  designer:
    - name: "[Designer]"

  reviewers:
    - name: "[Reviewer]"
      role: "Subject Reviewer"

  contributors:
    - name: "[Contributor]"
      role: "Contributor"

---

28. Acknowledgements

Acknowledgements should be stored in:

publication/acknowledgements.md

Example:

# Acknowledgements

The author acknowledges the teachers, learners,
reviewers and other contributors who assisted in
the development of this publication.

Acknowledgements are optional.

---

29. Curriculum Acknowledgement

Where appropriate, the publication may acknowledge the curriculum or educational authority on which the book is based.

Such wording must be factually accurate and should not imply official endorsement unless such endorsement exists.

---

30. Institutional Affiliation

An author or contributor may have an institutional affiliation.

Example:

author:
  - name: "[Author]"
    role: "Author"
    organization: "[Organization]"

The organization should only be identified as an affiliation where appropriate.

---

31. Publication Contact

Optional public contact information:

contact:
  email: ""
  website: ""

The platform should not automatically expose private contact information.

---

32. Publication Status

A book may have a publication status:

status:
  stage: draft

Supported stages:

draft
review
pilot
pre-release
published
archived

This metadata may control which publication information and warnings appear during builds.

---

33. Publication Dates

Optional:

dates:
  created: "2026-01-01"
  published: ""
  revised: ""

The publishing engine must not invent publication dates.

---

34. Version

Technical content version and publication edition are different concepts.

Example:

version: "1.0.0"

edition:
  number: 1
  year: 2026

"version" refers to the production/source version.

"edition" refers to the published edition.

---

35. Difference Between Version and Edition

Example:

Source version:
1.0.7

Publication:
First Edition, 2026

A correction to the source may result in:

1.0.8

without necessarily creating a new edition.

A substantial published revision may result in:

Second Edition

The publishing workflow must keep these concepts separate.

---

36. Front Matter

The publishing engine should support standard front-matter components:

Cover
Title Page
Publication Information
Copyright Page
Acknowledgements
Contents
Preface
Introduction

Only configured sections should be generated.

---

37. Cover

The cover should be generated from:

Book title
Subtitle
Grade
Subject
Author
Publisher
Edition
Cover artwork

The exact visual design belongs to "DESIGN_SYSTEM.md".

---

38. Title Page

The title page may contain:

Title
Subtitle
Author
Publisher
Edition

Example:

Grade 4 Mathematics

Learning Mathematics Through Practice and Discovery

[Author]

[Publisher]

First Edition
2026

---

39. Copyright Page

The copyright page should be generated from publication metadata.

Possible structure:

Grade 4 Mathematics

First Edition, 2026

Copyright © 2026 [Copyright Holder]

All rights reserved.

Author: [Author]
Publisher: [Publisher]

ISBN:
Print:
Ebook:

[Additional publication statements]

The exact wording and order should be controlled by the publication template.

---

40. Acknowledgements Page

If acknowledgements are enabled:

Acknowledgements

[Content from acknowledgements.md]

If no acknowledgements exist, the engine should not generate an empty page.

---

41. Credits Page

If credits are enabled:

Credits

Author
[Author]

Editor
[Editor]

Illustrator
[Illustrator]

Curriculum Reviewer
[Reviewer]

The engine should omit empty categories.

---

42. Metadata for Digital Publications

The publication metadata should populate digital metadata where supported.

Examples:

Title
Author
Publisher
Language
Copyright
Identifier
Description
Subject
Publication date

This information should be generated from the same source metadata.

---

43. Metadata Consistency

The platform must ensure consistency between:

book.yml
publication/*.yml
PDF metadata
EPUB metadata
Cover
Title page
Copyright page
Website metadata

For example, the author name should not differ between the cover and EPUB metadata unless intentionally configured.

---

44. Copyright and Assets

Book copyright and asset licensing are separate concepts.

For example:

Book:
Copyright © 2026 [Author]

Illustration:
Copyright © 2026 [Illustrator]

Photograph:
CC BY 4.0

The asset's license must not automatically inherit the book's license.

---

45. Asset Attribution

Where an external asset requires attribution, the asset metadata should contain:

creator:
source:
license:
attribution:

The publishing engine should be able to collect these into an attribution section when required.

---

46. Third-Party Content

Third-party material must have explicit rights information before publication.

The QA system should flag:

Missing creator
Missing source
Missing license
Missing attribution
Unknown rights

The book should not be considered publication-ready if required rights information is unresolved.

---

47. AI-Generated Material

Where AI-generated material is used, the project's internal records should identify it where necessary for rights and production management.

Example asset metadata:

creator:
  type: ai_assisted
  name: "[Tool/Workflow]"

source: generated

license: Copyright

The platform should not make unsupported legal claims about ownership of AI-generated material.

Publication/legal decisions should be reviewed by the rights holder or publisher.

---

48. Publication Metadata Validation

The publishing engine should validate:

Author

- Author exists
- Name is not empty

Publisher

- Publisher exists where required

Copyright

- Holder exists
- Year exists
- License exists
- Rights statement exists

Edition

- Edition number is valid
- Edition year is valid

ISBN

- If supplied, format should be validated
- ISBN should never be generated automatically

Credits

- Empty credit entries are rejected
- Duplicate entries should be detected where appropriate

---

49. Publication Metadata Warnings

The system should generate warnings for:

ISBN missing
Publisher missing
Acknowledgements not supplied
Credits not supplied
Publication date missing
Asset attribution incomplete
License information incomplete

Not every warning should prevent development builds.

Production rules are controlled by QA configuration.

---

50. Publication Metadata Security

The repository may contain information that is not intended for publication.

Therefore:

PUBLICATION METADATA
≠
PRIVATE PROJECT INFORMATION

Private contact details, credentials, internal notes and confidential contracts must not be stored in public-facing publication metadata.

---

51. Example Complete Publication Directory

publication/
├── author.yml
├── publisher.yml
├── copyright.yml
├── edition.yml
├── identifiers.yml
├── credits.yml
├── acknowledgements.md
└── license.md

Not every file is required.

The publishing engine should support both:

Central publication metadata

and:

Separate publication metadata files

provided the precedence rules are clearly defined.

---

52. Recommended Precedence

When the same information appears in multiple locations:

Book-specific publication metadata
        ↓
Book.yml publication section
        ↓
Subject defaults
        ↓
Platform defaults

The most specific valid value wins.

However, duplicate conflicting values should generate a warning so that accidental inconsistencies are not hidden.

---

53. Example Author File

"publication/author.yml"

authors:

  - name: "[Author]"
    role: "Author"
    order: 1

---

54. Example Publisher File

"publication/publisher.yml"

publisher:

  name: "[Publisher]"

  location: "Papua New Guinea"

  city: ""

  country: PG

---

55. Example Copyright File

"publication/copyright.yml"

copyright:

  holder: "[Copyright Holder]"

  year: 2026

  license: "Copyright"

  rights: "All rights reserved."

---

56. Example Edition File

"publication/edition.yml"

edition:

  number: 1

  year: 2026

  name: "First Edition"

---

57. Example Credits File

"publication/credits.yml"

credits:

  editors: []

  illustrators: []

  designers: []

  reviewers: []

  contributors: []

---

58. Example Publication Metadata

A complete example:

publication:

  author:
    - name: "[Author]"
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
    year: 2026
    name: "First Edition"

  isbn:
    print: ""
    ebook: ""

  credits:

    editors: []

    illustrators: []

    designers: []

    reviewers: []

    contributors: []

---

59. Future Publishing Support

The publication schema should eventually support:

Print books
EPUB
Digital textbooks
Web publications
Kolibri resources
Teacher guides
Workbooks
Assessment books
Translated editions
Revised editions
Co-published editions
Institutional publications

The publication metadata model should remain independent of the output format.

---

60. Definition of Done

"PUBLICATION_SCHEMA.md" is implemented when:

- Authors can be defined.
- Multiple authors are supported.
- Publisher information can be defined.
- Copyright holder can be defined.
- Copyright year can be defined.
- Copyright license can be defined.
- Rights statements can be defined.
- Edition information can be defined.
- ISBN information can be stored.
- Contributors can be credited.
- Editors can be credited.
- Illustrators can be credited.
- Designers can be credited.
- Reviewers can be credited.
- Acknowledgements can be included.
- Publication metadata can populate PDF and EPUB metadata.
- Copyright and asset licensing remain separate.
- Missing or inconsistent metadata is detected.
- Private information is kept separate from public publication information.

---

61. Golden Rule

Publication metadata should answer:

«Who created this publication, who owns it, who published it, what edition is it, and under what rights may it be used?»

It should do this without becoming mixed with the educational content or the publishing engine.

The platform therefore maintains:

CONTENT
      +
BOOK CONFIGURATION
      +
PUBLICATION METADATA
      +
DESIGN
      +
PUBLISHING ENGINE
      +
QA
      ↓
FINAL PUBLICATION
