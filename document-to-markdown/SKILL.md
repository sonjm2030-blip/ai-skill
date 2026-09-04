---
name: document-to-markdown
description: >
  Convert copied webpages, documents, PDF exports, screenshots, and images
  into clean, faithful Markdown. Preserve meaningful structure, text, tables,
  code, links, and visual information while removing interface noise and
  extraction artifacts. Works across domains and document types.
---

# Document to Markdown

Convert provided content into clean, faithful, reusable Markdown.

The input may include:

- fully copied webpage content
- copied document text
- PDF files
- PDF exports of webpages
- screenshots
- individual images
- HTML-like copied content
- combinations of the above

This skill is domain-independent.

Do not assume that the document belongs to any particular:

- company
- industry
- website
- wiki platform
- technical field
- language
- document type

The goal is document digitization and structural conversion, not summarization.

## 1. Core behavior

Preserve the source document's meaningful content as faithfully as possible.

Preserve when present:

- title
- metadata
- headings
- paragraphs
- lists
- tables
- links
- footnotes
- citations
- quotations
- code
- commands
- formulas
- filenames
- technical identifiers
- captions
- diagrams
- charts
- screenshots
- meaningful images

Do not:

- summarize
- paraphrase
- rewrite
- simplify
- expand
- fact-check
- translate
- change terminology
- add conclusions

unless explicitly requested.

## 2. Source priority

When multiple representations of the same document are supplied, use them together.

For textual content, prefer:

1. clean copied text
2. embedded/selectable PDF text
3. visible text in screenshots or images

For visual content, prefer:

1. original supplied image
2. screenshot
3. PDF-rendered visual

Do not replace reliable copied text with lower-quality extraction.

## 3. Main content extraction

Identify the actual document content and separate it from surrounding interface elements.

Preserve content that contributes to the meaning of the document.

Remove interface noise such as:

- global navigation
- menus
- breadcrumbs
- search controls
- account controls
- edit controls
- reaction controls
- share buttons
- profile widgets
- comment-entry interfaces
- pagination controls
- duplicated headers
- repeated footers
- decorative icons
- accessibility-only interface strings
- unrelated recommendations
- advertisements when clearly outside the document body

Do not use a fixed list of site-specific UI labels as the primary rule.

Determine whether an element belongs to the document based on context and function.

## 4. Metadata

Preserve useful document-level metadata when clearly available.

Examples:

- title
- author
- publication date
- last updated date
- source URL
- version
- organization
- document identifier

Optional frontmatter:

---
title: "..."
author: "..."
source_url: "..."
date: "..."
---

Do not invent missing metadata.

Remove metadata that is merely interface state or account information.

## 5. Heading structure

Reconstruct a logical Markdown heading hierarchy.

Use:

# Document title

## Major section

### Subsection

#### Nested subsection

Preserve the source hierarchy whenever possible.

Repair obvious extraction artifacts but do not redesign the document.

## 6. Paragraphs

Repair line wrapping introduced by:

- browser copying
- narrow layouts
- PDF rendering
- page breaks
- column layouts

Preserve intentional paragraph boundaries.

## 7. Lists

Recover ordered and unordered list structure.

Repair:

- duplicated bullets
- isolated bullet symbols
- broken indentation
- list items split across lines

Preserve numbering when sequence or numbering is meaningful.

## 8. Tables

Convert reliably identifiable tables into Markdown tables.

Preserve:

- headers
- rows
- columns
- values
- inline code
- meaningful links

Do not guess missing or ambiguous cells.

If a complex table cannot be represented safely in Markdown, preserve it as structured text or retain the image.

## 9. Code and technical content

Preserve technical strings exactly.

Examples include:

- source code
- commands
- file paths
- URLs
- configuration
- JSON
- JSONL
- SQL
- filenames
- model names
- identifiers
- version numbers

Use inline code or fenced code blocks appropriately.

Never silently modify executable or technical content.

## 10. Links

Preserve links that are meaningful parts of the document.

Examples:

- references
- citations
- related documents
- attachments
- source repositories
- datasets
- specifications
- supporting material

Remove links whose only purpose is controlling the webpage interface.

## 11. Sensitive URL cleanup

Copied webpages may expose temporary or security-related query parameters.

Do not reproduce authentication credentials or secrets.

Remove identifiable parameters such as:

- access tokens
- session identifiers
- API keys
- authentication tokens
- CSRF tokens
- temporary signatures

If an interface-action link becomes meaningless after sanitization, remove the link.

Do not invent replacement values.

## 12. Images

Determine whether each image carries meaningful document information.

Meaningful images may include:

- photographs
- diagrams
- workflows
- charts
- plots
- screenshots
- figures
- scanned text
- visual tables
- maps
- illustrations that convey information

Remove images that are clearly only:

- avatars
- reaction icons
- navigation icons
- decorative separators
- interface decoration

Do not remove an image simply because it is not textual.

## 13. Full copy + image placeholders

Copied webpages may contain placeholders such as:

[image]

or:

[image](URL)

If the actual image is not provided and cannot be inspected, preserve its position using:

> [Image unavailable in provided input]

If surrounding text reliably identifies its purpose, a short known description may be added.

Never infer unseen image contents.

## 14. Supplied screenshots and images

When screenshots or images are supplied alongside copied text, match them to the document using:

1. surrounding text
2. nearby headings
3. captions
4. content similarity
5. visual order
6. attachment order

Do not force an uncertain match.

## 15. Diagrams and workflows

Preserve the original visual when possible.

Also provide a concise textual representation when the relationships are clear.

Example:

![Workflow](assets/workflow-01.png)

**Diagram summary**

Input → Processing → Validation → Output

The textual representation should improve searchability and accessibility.

Do not invent nodes, labels, arrows, or relationships.

Do not automatically replace the image with Mermaid.

## 16. Charts

Preserve meaningful charts.

Describe only information that can be reliably determined from the visual.

Do not infer exact numeric values from approximate graphical positions unless clearly readable.

If exact data labels are visible, they may be transcribed.

## 17. Image-based tables

If a table exists only as an image:

1. preserve the image
2. convert it to Markdown only when its structure and values are reliably readable

Do not guess ambiguous values.

## 18. Text inside images

Extract important visible text when sufficiently legible.

Do not invent unreadable:

- words
- numbers
- dates
- URLs
- code
- identifiers
- labels

When uncertain, retain the visual without speculative transcription.

## 19. PDF handling

For PDF inputs:

- use embedded text when available
- reconstruct logical reading order
- remove repeated page headers
- remove repeated page footers
- remove page numbers when they are not content
- merge paragraphs broken only by page boundaries
- preserve meaningful visual elements
- recover tables where reliable
- preserve captions
- preserve code and technical text exactly

When copied text and PDF are supplied together, use the copied text as the main textual source when it is cleaner.

Use the PDF primarily to recover:

- layout
- figures
- tables
- screenshots
- diagrams
- missing content

## 20. Screenshots

Screenshots may contain either document content or user-interface context.

Preserve the meaningful part.

Do not automatically transcribe every visible UI element.

If the screenshot itself is important, retain it and optionally add a concise description.

## 21. Conflicting inputs

If two supplied representations disagree, do not silently combine conflicting content.

Prefer the most direct and reliable source.

If the discrepancy appears to result from different versions of the document, retain the primary source and avoid inventing a merged version.

## 22. Missing information

Never fill missing document content from general knowledge.

Use explicit placeholders where necessary:

> [Image unavailable]

> [Content unreadable]

> [Table could not be reliably reconstructed]

## 23. Fidelity

The conversion should be loss-minimizing.

Formatting artifacts may be repaired, including:

- broken bullets
- duplicated headings
- malformed Markdown
- HTML escape artifacts
- PDF line wrapping
- accidental line breaks
- duplicated headers or footers
- broken table alignment

Substantive content must not be silently changed.

## 24. Output

For documents without extracted visual assets:

document.md

For documents with meaningful images:

document/
├── document.md
└── assets/
    ├── figure-01.png
    ├── diagram-01.png
    ├── screenshot-01.png
    └── table-01.png

Reference images with relative paths:

![Description](assets/figure-01.png)

Use descriptive filenames when practical.

## 25. Invocation

Short requests such as:

"이거 md로"

"마크다운으로 바꿔줘"

"이 페이지 정리해서 md로"

"PDF를 Markdown으로 변환해줘"

should trigger this workflow when relevant content is supplied.

The user may provide:

- text only
- text + screenshots
- text + PDF
- text + PDF + screenshots
- PDF only
- images only

Process whatever evidence is actually available.

## 26. Final validation

Before completing the conversion, verify that:

- meaningful content was preserved
- interface noise was removed
- headings are structurally valid
- lists are repaired
- tables are reliable
- technical content is unchanged
- meaningful links remain
- sensitive URL information is absent
- meaningful images were considered
- image contents were not invented
- PDF artifacts were removed
- no unintended summarization occurred
- the final Markdown is readable and valid
