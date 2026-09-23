<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/RU-EducationalPlatform/.github/main/assets/prosaidon-logo-dark.svg">
  <img src="https://raw.githubusercontent.com/RU-EducationalPlatform/.github/main/assets/prosaidon-logo.svg" alt="prosAIdon" width="420">
</picture>

<br><br>

**One document platform that writes, computes, tests and grades.**

<br>

![IDoc](https://img.shields.io/badge/IDoc-0.1.8-1F8F7A?style=flat-square&labelColor=0E2A31)
![Desktop](https://img.shields.io/badge/desktop-macOS%20·%20Windows%20·%20Linux-0E2A31?style=flat-square&labelColor=1F8F7A)
![Knowsy](https://img.shields.io/badge/Knowsy-47%20modules-1F8F7A?style=flat-square&labelColor=0E2A31)
![Live](https://img.shields.io/badge/live-idoc.page-0E2A31?style=flat-square&labelColor=1F8F7A)

</div>

---

A course is written in four or five programs that do not speak to each other. The
notes are in Word, the equations are in LaTeX, the quiz is in Canvas, the code
demo is a screenshot, and the exam is a PDF somebody re-types into a gradebook at
midnight. Each tool is fine. The seams between them are where the evenings go.

prosAIdon builds the two halves of a replacement: a document format that carries
its own assessment, and a library of interactive modules that a document can put
a student inside.

<br>

<div align="center">
<img src="https://raw.githubusercontent.com/RU-EducationalPlatform/.github/main/assets/idoc-editor.jpg" alt="The IDoc editor: source on the left, live preview on the right with typeset maths, graded questions and a chart" width="880">
<br>
<sub>Source on the left, the live document on the right. The same file prints to PDF and grades itself.</sub>
</div>

---

## IDoc

A single `@` introducer, one source file, and the output is a web page, a PDF, a
printable exam or a slide deck. What LaTeX and Markdown cannot do is the second
half: the questions are part of the document, and they mark themselves.

```idoc
@qc(10)
Using only NAND gates, how many are needed to build a 2-input XOR? @q(fn: 4)

@graph(type=line, x=fanout, y=delay, title="Propagation delay vs fan-out", trend)
@data
fanout,delay
1,2.1
4,7.2
6,12.1
@end
```

That is the whole document. It renders, it prints, and question 1 is worth ten
points whether the student answers it in a browser or on paper with a pencil.

**252 directives. 52 question kinds. 49 widgets. 43 chart types. 10 paper venues.**

Maths is written without backslashes (`frac`, `alpha`, `leq`) and typesets
through KaTeX on screen and Typst in the PDF. Beyond prose and questions there
are real instruments: a breadboard with a simulated ATmega328P that compiles your
sketch, a KiCad-class schematic editor running ngspice, a PCB studio, a CAD
kernel, a spreadsheet with about sixty functions that charts read from live, 3-D
terrain and maps, and slide decks with a presenter view.

Paper exams get a barcode and registration marks, so a stack of scanned sheets
comes back aligned, cropped per answer, marked, and queued for review.

A course is a file and a folder. `ECE231.course` is text you can read, diff and
hand to a colleague; `ECE231.lms/` holds the roster, grades, submissions and an
append-only event log, also text. A semester zips up and unzips on someone else's
laptop.

<div align="center">

**[Try it at idoc.page](https://idoc.page)** &nbsp;·&nbsp; **[Download the app](https://github.com/RU-EducationalPlatform/idoc-desktop/releases/latest)**

</div>

### The desktop app

The same editor, installed, with the documents on your own disk. macOS on Apple
silicon and Intel, Windows, and Linux as an AppImage. Python, C and C++, Arduino
builds, speech and offline narration arrive as add-on packs you install from
inside the app, so the download stays under 400 MB instead of three gigabytes.

| | |
|---|---|
| **Latest** | [0.1.8](https://github.com/RU-EducationalPlatform/idoc-desktop/releases/latest) |
| **Platforms** | macOS (arm64, x64), Windows x64, Linux x86_64 |
| **Repository** | [idoc-desktop](https://github.com/RU-EducationalPlatform/idoc-desktop) |

Installers are unsigned, so macOS and Windows will warn you on first open.

---

## Knowsy

Forty-seven interactive modules for the things that do not survive a static page.
You do not read about how a pipeline stalls; you watch hazards move through one.
You do not memorise a truth table; you drop minterms on a Karnaugh map and watch
it group itself.

Assembly simulators for x86, AArch64, RISC-V and LC-3, each with real registers,
flags and a memory inspector. Bits as numbers and bits as characters. Boolean
algebra, K-maps, integer overflow, floating point, Hamming codes and CRC. A
Verilog simulator with a waveform viewer. A Smith chart you drag a load around.
Antenna radiation patterns in 2-D polar and a 3-D dome. A shader playground with
GPU printf. Solar system flight, celestial navigation, map projections.

They run at **[knowsy.duckdns.org](https://knowsy.duckdns.org)**, and a professor
can open one on a projector without signing in to anything.

### How the two fit together

A Knowsy module can be embedded in an IDoc paper as coursework. The module runs
in an iframe, the document sets the task, and the module reports **what the
student did, never what they scored**. A module that could post `score: 1` is a
module a student can post `score: 1` from, with the browser console open, and
every mark underneath it becomes decoration. The score is worked out on the
server, next to the roster and the audit chain.

Ten modules are wired this way for a digital logic course: bit interpretation,
bits as characters, bit operations, boolean algebra, Karnaugh maps, RISC-V, x86,
Verilog, the solar system and the shader playground.

---

## Where it runs

`idoc.page` is one hostname over two independent stacks, each with its own
database, routed by a cookie. Behind them sit an isolated container for running
student code, a separate host for education records, and an integration box that
every change passes through first.

<div align="center">
<img src="https://raw.githubusercontent.com/RU-EducationalPlatform/.github/main/assets/architecture.svg" alt="Production architecture: five trust zones from the public internet through the nginx edge and application tier to isolated code execution and a restricted education-records database" width="720">
</div>

In production today with **350 users in Rutgers ECE, for ECE231 Digital Logic
Design**. A real course, with real homework, real exams and real grades, which is
the only test that has ever told us anything.

---

## The repositories

| Repository | What it is |
|---|---|
| **[idoc-desktop](https://github.com/RU-EducationalPlatform/idoc-desktop)** | The installed app. Public: downloads, add-on packs, the update feed. |
| **IDoc** | The platform. Engine, editor shell, accounts, the LMS, the deployment. Private. |
| **Knowsy** | The interactive modules and the class platform. Private. |
| **blockloaders** | Block formats and WASM tools behind the maps, terrain and 3-D. Private. |

---

<div align="center">
<sub>

**prosAIdon** &nbsp;·&nbsp; Dov Kruger &nbsp;·&nbsp; Satrajit Ghosh

<img src="https://raw.githubusercontent.com/RU-EducationalPlatform/.github/main/assets/prosaidon-mark.svg" alt="" width="26">

</sub>
</div>
