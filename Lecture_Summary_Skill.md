# Helper Functions — Copy These Verbatim Into Your Script

These are the canonical helper functions for the lecture summary style.
Do not modify them. Do not create alternative versions. Copy them exactly.

---

## heading1 — Full-width dark blue section bar

```javascript
function heading1(text) {
  return new Paragraph({
    children: [
      new TextRun({
        text,
        bold: true,
        size: 28,
        color: "FFFFFF",
        font: "Calibri",
      })
    ],
    shading: { type: ShadingType.CLEAR, fill: "1F3864" },
    spacing: { before: 300, after: 120 },
    indent: { left: convertInchesToTwip(0.1) },
  });
}
```

**When to use:** Top-level section breaks. Prefix with "SECTION N:" e.g.
`heading1("SECTION 3: ChatGPT Integration for Small Businesses")`

---

## heading2 — Mid-blue subsection bar

```javascript
function heading2(text) {
  return new Paragraph({
    children: [
      new TextRun({
        text,
        bold: true,
        size: 26,
        color: "FFFFFF",
        font: "Calibri",
      })
    ],
    shading: { type: ShadingType.CLEAR, fill: "2E74B5" },
    spacing: { before: 240, after: 100 },
    indent: { left: convertInchesToTwip(0.1) },
  });
}
```

**When to use:** Numbered subsections within a section. Format: `"N.N  Title"`
e.g. `heading2("3.2  Why Small Companies Should Care")`

---

## heading3 — Bold underlined dark-blue sub-subsection

```javascript
function heading3(text) {
  return new Paragraph({
    children: [
      new TextRun({
        text,
        bold: true,
        size: 24,
        color: "1F3864",
        font: "Calibri",
        underline: { type: UnderlineType.SINGLE, color: "2E74B5" },
      })
    ],
    spacing: { before: 200, after: 80 },
  });
}
```

**When to use:** Sub-topics within a subsection. No number prefix needed.

---

## bodyText — Standard paragraph prose

```javascript
function bodyText(text) {
  return new Paragraph({
    children: [
      new TextRun({
        text,
        size: 22,
        font: "Calibri",
        color: "000000",
      })
    ],
    spacing: { before: 60, after: 60 },
  });
}
```

**When to use:** All explanatory prose. Use multiple `bodyText()` calls for
multiple paragraphs — never use `\n`. Always precedes bullet lists.

---

## bulletPoint — First-level bullet

```javascript
function bulletPoint(text, bold_prefix = null) {
  const children = [];
  if (bold_prefix) {
    children.push(new TextRun({
      text: bold_prefix + " ",
      bold: true,
      size: 22,
      font: "Calibri",
      color: "000000",
    }));
    children.push(new TextRun({
      text,
      size: 22,
      font: "Calibri",
      color: "000000",
    }));
  } else {
    children.push(new TextRun({
      text,
      size: 22,
      font: "Calibri",
      color: "000000",
    }));
  }
  return new Paragraph({
    children,
    bullet: { level: 0 },
    spacing: { before: 60, after: 60 },
    indent: { left: convertInchesToTwip(0.35), hanging: convertInchesToTwip(0.25) },
  });
}
```

**When to use:** List items. For bold prefix: `bulletPoint("rest of text", "Bold label:")`

---

## subBullet — Second-level bullet (indented)

```javascript
function subBullet(text) {
  return new Paragraph({
    children: [new TextRun({ text, size: 22, font: "Calibri", color: "000000" })],
    bullet: { level: 1 },
    spacing: { before: 40, after: 40 },
    indent: {
      left: convertInchesToTwip(0.7),
      hanging: convertInchesToTwip(0.25),
    },
  });
}
```

**When to use:** Sub-points under a bulletPoint. Use sparingly.

---

## calloutBox — Two-column labelled callout

```javascript
function calloutBox(label, text, fillColor) {
  return new Table({
    width: { size: 100, type: WidthType.PERCENTAGE },
    columnWidths: [1440, 7560],
    rows: [
      new TableRow({
        children: [
          new TableCell({
            width: { size: 1440, type: WidthType.DXA },
            shading: { type: ShadingType.CLEAR, fill: "1F3864" },
            children: [new Paragraph({
              children: [new TextRun({
                text: label,
                bold: true,
                color: "FFFFFF",
                size: 22,
                font: "Calibri",
              })],
              alignment: AlignmentType.CENTER,
            })],
            verticalAlign: "center",
          }),
          new TableCell({
            width: { size: 7560, type: WidthType.DXA },
            shading: { type: ShadingType.CLEAR, fill: fillColor || "D6E4F0" },
            children: [new Paragraph({
              children: [new TextRun({
                text,
                size: 22,
                font: "Calibri",
                color: "000000",
              })],
              spacing: { before: 60, after: 60 },
              indent: { left: convertInchesToTwip(0.1) },
            })],
          }),
        ],
      }),
    ],
    margins: { top: 40, bottom: 40 },
  });
}
```

**Label / fillColor combinations:**
| Label | fillColor constant | Meaning |
|---|---|---|
| `"📌 Key Learning"` | `LIGHT_BLUE` | Critical point flagged by instructor |
| `"Case"` | `LIGHT_GREEN` | Real-world example or mini case study |
| `"⚠️ Warning"` | `LIGHT_ORANGE` | Risk, ethical concern, or pitfall |
| `"Quote"` | `LIGHT_BLUE` | Near-verbatim instructor or expert quote |
| Named concept (e.g. `"FOBO"`) | `LIGHT_ORANGE` | Defined term with explanation |
| `"To Get Started"` | `LIGHT_BLUE` | Practical next steps or how-to |
| `"Story Learning"` | `LIGHT_ORANGE` | Lesson extracted from an anecdote |
| `"Networking Principle"` | `LIGHT_BLUE` | Soft-skills or career advice |

---

## insightBox — Numbered instructor insight

```javascript
function insightBox(number, title, text) {
  return new Table({
    width: { size: 100, type: WidthType.PERCENTAGE },
    columnWidths: [1080, 7920],
    rows: [
      new TableRow({
        children: [
          new TableCell({
            width: { size: 1080, type: WidthType.DXA },
            shading: { type: ShadingType.CLEAR, fill: "C55A11" },
            children: [new Paragraph({
              children: [new TextRun({
                text: `Insight ${number}`,
                bold: true,
                color: "FFFFFF",
                size: 20,
                font: "Calibri",
              })],
              alignment: AlignmentType.CENTER,
            })],
            verticalAlign: "center",
          }),
          new TableCell({
            width: { size: 7920, type: WidthType.DXA },
            shading: { type: ShadingType.CLEAR, fill: "FCE4D6" },
            children: [
              new Paragraph({
                children: [new TextRun({
                  text: title,
                  bold: true,
                  size: 22,
                  font: "Calibri",
                  color: "000000",
                })],
                spacing: { before: 40, after: 20 },
                indent: { left: convertInchesToTwip(0.1) },
              }),
              new Paragraph({
                children: [new TextRun({
                  text,
                  size: 20,
                  font: "Calibri",
                  color: "000000",
                })],
                spacing: { before: 20, after: 40 },
                indent: { left: convertInchesToTwip(0.1) },
              }),
            ],
          }),
        ],
      }),
    ],
    margins: { top: 60, bottom: 60 },
  });
}
```

**When to use:** Whenever the instructor presents numbered or named insights,
stories, or recurring lessons. The orange label creates strong visual anchoring.

---

## makeTable — Data table with dark-blue headers

```javascript
function makeTable(headers, rows, fillHeader = "1F3864") {
  const totalWidth = 9000;
  const colWidth = Math.floor(totalWidth / headers.length);
  const colWidths = headers.map(() => colWidth);

  const headerRow = new TableRow({
    tableHeader: true,
    children: headers.map((h, i) => new TableCell({
      width: { size: colWidths[i], type: WidthType.DXA },
      shading: { type: ShadingType.CLEAR, fill: fillHeader },
      children: [new Paragraph({
        children: [new TextRun({
          text: h,
          bold: true,
          color: "FFFFFF",
          size: 20,
          font: "Calibri",
        })],
        alignment: AlignmentType.CENTER,
        spacing: { before: 60, after: 60 },
      })],
    })),
  });

  const dataRows = rows.map((row, ri) => new TableRow({
    children: row.map((cell, ci) => new TableCell({
      width: { size: colWidths[ci], type: WidthType.DXA },
      shading: { type: ShadingType.CLEAR, fill: ri % 2 === 0 ? "FFFFFF" : "F2F2F2" },
      children: [new Paragraph({
        children: [new TextRun({
          text: cell,
          size: 20,
          font: "Calibri",
          color: "000000",
        })],
        spacing: { before: 60, after: 60 },
        indent: { left: convertInchesToTwip(0.05) },
      })],
    })),
  }));

  return new Table({
    width: { size: 100, type: WidthType.PERCENTAGE },
    columnWidths: colWidths,
    rows: [headerRow, ...dataRows],
    margins: { top: 40, bottom: 40 },
  });
}
```

**Column width note:** Default distributes evenly. For uneven columns (e.g.
narrow label + wide description), override `colWidths` manually — they must
still sum to 9000.

---

## spacer — Blank spacing paragraph

```javascript
function spacer() {
  return new Paragraph({
    text: "",
    spacing: { before: 80, after: 80 },
  });
}
```

**When to use:** Between every heading and its content. Between distinct content
blocks. Between callout/insight boxes and surrounding content.

---

## pageBreakPara — Hard page break

```javascript
function pageBreakPara() {
  return new Paragraph({ children: [new PageBreak()] });
}
```

**When to use:** Between major SECTION blocks only. Never mid-section.

---

## codeBlock — Monospace code snippet

```javascript
function codeBlock(lines) {
  // lines: array of strings, one per line
  return lines.map(line => new Paragraph({
    children: [new TextRun({
      text: line,
      size: 18,
      font: "Courier New",
      color: "1F3864",
    })],
    shading: { type: ShadingType.CLEAR, fill: "F5F5F5" },
    spacing: { before: 10, after: 10 },
    indent: { left: convertInchesToTwip(0.3) },
  }));
}
```

**When to use:** When lecture content includes code snippets or terminal commands.
Pass an array of strings, one per line. Spread into children: `...codeBlock([...])`

---

## quoteBlock — Centred italic pull-quote

```javascript
function quoteBlock(quoteText, attribution) {
  return new Paragraph({
    children: [
      new TextRun({
        text: `"${quoteText}"`,
        italics: true,
        size: 24,
        color: "1F3864",
        font: "Calibri",
      }),
      ...(attribution ? [new TextRun({
        text: `  — ${attribution}`,
        bold: true,
        size: 22,
        font: "Calibri",
        color: "444444",
      })] : []),
    ],
    alignment: AlignmentType.CENTER,
    shading: { type: ShadingType.CLEAR, fill: "D6E4F0" },
    spacing: { before: 120, after: 120 },
    indent: {
      left: convertInchesToTwip(0.5),
      right: convertInchesToTwip(0.5),
    },
  });
}
```

**When to use:** Prominent quotes from industry leaders, notable instructor
statements, or framework-defining phrases. E.g. Jeff Bezos on agility.

---

## titleBlock — Document header (always first in children)

```javascript
function titleBlock(programme, title, subtitle, instructor) {
  return [
    new Paragraph({
      children: [new TextRun({
        text: programme,
        size: 24,
        color: "666666",
        font: "Calibri",
      })],
      alignment: AlignmentType.CENTER,
      spacing: { before: 400, after: 60 },
    }),
    new Paragraph({
      children: [new TextRun({
        text: title,
        bold: true,
        size: 40,
        color: "1F3864",
        font: "Calibri",
      })],
      alignment: AlignmentType.CENTER,
      spacing: { before: 60, after: 60 },
    }),
    new Paragraph({
      children: [new TextRun({
        text: subtitle,
        bold: true,
        size: 30,
        color: "2E74B5",
        font: "Calibri",
      })],
      alignment: AlignmentType.CENTER,
      spacing: { before: 60, after: 120 },
    }),
    new Paragraph({
      children: [new TextRun({
        text: instructor,
        size: 22,
        color: "444444",
        font: "Calibri",
      })],
      alignment: AlignmentType.CENTER,
      spacing: { before: 40, after: 600 },
    }),
  ];
}
```

**Usage:** `...titleBlock("NTU/NBS Executive Programme", "COMPREHENSIVE LECTURE SUMMARY NOTES", "Day 2: AI Use Cases & Business Strategy", "Instructor: ...")`

---

## footerLine — Document end marker

```javascript
function footerLine(text) {
  return new Paragraph({
    children: [new TextRun({
      text,
      size: 20,
      color: "888888",
      font: "Calibri",
      italics: true,
    })],
    alignment: AlignmentType.CENTER,
    spacing: { before: 400, after: 200 },
  });
}
```

**Usage:** `footerLine("End of Lecture Summary — Day 2")` — always last element.
