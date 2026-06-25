---
title: Academic Writing and Presenting
authors:
  - name: Hanspeter Schmid
    affiliation: FHNW
  - name: Daniele Puccinelli
    affiliation: SUPSI
exports:
- format: pdf
  template: https://github.com/marbetschar/plain_latex_article/archive/refs/heads/main.zip
  output: AcWritPre.pdf
  id: acwritpre-pdf
downloads:
  - id: acwritpre-pdf
    title: Download as PDF
---

```{epigraph}
Clear thinking becomes clear writing; one can't exist without the other - William Zinsser
```

# Academic Presenting

Apply the four-element theory to assess and improve technical presentations:

## Air (Design & whitespace)
- Ensure adequate whitespace on slides
- Avoid clutter
- Use the rule of three for structure
- Create visual breathing room

## Water (Story & flow)
- Choose an appropriate story structure
- Maintain logical progression
- Ensure smooth transitions
- Keep the audience engaged

## Earth (Content & substance)
- Every slide element must help users grasp the topic
- Avoid information overload
- Use visual cues instead of laser pointers
- Maintain technical rigor

## Fire (Delivery & passion)
- Plan recording to include energy
- Maintain appropriate enthusiasm
- Use body language effectively
- Connect with the audience

## Presentation and Video Production Tools

```{list-table}
:header-rows: 1
:widths: 25 35 40

* - Category
  - Tools
  - Purpose
* - Presentation
  - LaTeX, LibreOffice Impress, PowerPoint
  - Creating slide decks
* - Recording
  - OBS Studio
  - Mixing and recording video/audio
* - Streaming
  - OBS Studio
  - Integration with conferencing tools
* - Video Editing
  - ShotCut, OpenShot
  - Cutting and editing video
* - Audio Editing
  - Audacity
  - Audio cleanup and editing
* - Final Production
  - Handbrake
  - Encoding and format conversion
```

# Academic Writing

## The Toulmin Method

The Toulmin method provides a framework for constructing rigorous, logical arguments - and consists of six components:

1. **Claim**: Main message to be conveyed
2. **Grounds**: Evidence supporting the claim  
3. **Warrant**: Assumption linking grounds to claim
4. **Backing**: Information supporting the warrant
5. **Rebuttal**: Potential objections to the claim
6. **Qualifier**: Nuances or conditions restricting the claim

```{note} Why Toulmin Matters
In engineering, evidence-based arguments require clear logical connections between data, assumptions, and conclusions.
```

```{prf:example} Climate Change Argument Example (from research literature)
- **Claim**: Current climate policies could leave around one-third of humanity outside the human climate niche by 2100
- **Grounds**: Over 600 million people already pushed out; projections show 22-39% by 2100
- **Warrant**: Human climate niche = temperature conditions where most humans lived historically
- **Backing**: Heat affects humans negatively (cognitive science research)
- **Qualifier**: "Could leave" and "around one-third" indicate probability
- **Rebuttal**: Some regions may adapt, but evidence suggests limits
```

```{prf:example} Political Science Prose Example (from APSR analysis)
- **Claim**: Academic writing is hard to read
- **Grounds**: APSR articles show heavy noun phrases, piled modifiers, buried verbs (>1000 examples)
- **Warrant**: Readability is important for effective communication
- **Backing**: Cognitive science shows poor readability confuses, misleads, distracts
- **Rebuttal**: Some complex ideas may require complex expression
```

## The ACCC Principles

The four principles of effective technical writing:

1. **Accuracy**: Both technical and linguistic precision
2. **Clarity**: Make the message effortless to understand
3. **Conciseness**: Eliminate waste; pretend each word costs money
4. **Coherence**: Ensure smooth flow at macro (structure) and micro (sentence) levels

### Accuracy (Technical & Linguistic Precision)

- **Technical**: Ensure all facts, data, and claims are correct
- **Linguistic**: Use proper grammar, spelling, and syntax
- **Example**: "Mobile Edge Computing paradigm is designed..." -> "**The** mobile edge computing paradigm **is designed**..."

```{warning} Common Error: Article Usage
English requires careful article selection based on specificity.
```

### Clarity (Effortless Understanding)

- Don't make the reader work too hard
- Adapt jargon to audience
- Define acronyms on first use
- **Example**: "The flexibility measures available range from traditional ones..." -> "Flexibility measures range from traditional approaches (grid extension, pumped hydro) to advanced strategies like demand side management."

```{tip} Pro Tip: Audience Adaptation
In technical reports, define everything. In scientific papers, define based on target audience.
```

### Conciseness (Eliminate Waste)

- Remove unnecessary words
- Give greater visibility to key information
- **Example**: "We have designed and implemented the Google File System, a scalable distributed file system..." -> "We designed and implemented the Google File System, a scalable distributed file system providing fault tolerance on commodity hardware."

```{tip} Writing Philosophy: The 20-Word Rule
Aim for an average of 20 words per sentence.
```

### Coherence (Smooth Flow)

- **Macro-level**: Follow predictable structure based on audience
- **Micro-level**: Help reader follow along sentence-to-sentence
- **Example**: Ensure each paragraph has a clear topic sentence

```{note} Structure Matters
In engineering papers, predictable structure ensures readers can quickly locate information.
```

## Identify and Correct Common Flaws

```{list-table}
:header-rows: 1
:widths: 20 25 25 30

* - Flaw Type
  - Flawed Example
  - Corrected Version
  - Explanation
* - Ambiguous Antecedent
  - When Sarah gave her sister her book, she was pleased.
  - When Sarah gave her sister Sarah's book, the sister was pleased.
  - Unclear whether "she" refers to Sarah or her sister
* - Lack of Parallel Structure
  - The tasks include writing proposals, to attend meetings, and budgeting time.
  - The tasks include writing proposals, attending meetings, and budgeting time.
  - All list items must use same grammatical form
* - Number Mismatch
  - A comprehensive overviews were provided.
  - A comprehensive overview was provided.
  - Subject-verb agreement error
* - Dangling Modifier
  - Running the diagnostic software, the error codes were unclear.
  - Running the diagnostic software, the technician found the error codes unclear.
  - Modifier must logically attach to subject
* - Comma Splice
  - She writes well, she does not like to read.
  - She writes well, but she does not like to read.
  - Two independent clauses need conjunction
* - Run-on Sentence
  - How do you correct run-on sentences it's not as easy as it seems
  - How do you correct run-on sentences? It's not as easy as it seems.
  - Independent clauses need proper punctuation
* - Incorrect Article
  - We begin by discussing properties of sensor network.
  - We begin by discussing the properties of a sensor network.
  - Both nouns require articles based on specificity
```

## Relative Clauses

```{warning} UK vs. US English
UK English is more flexible with "which" in restrictive clauses, but "that" is preferred in formal academic writing.
```

### Restrictive Relative Clauses (Essential Information)

- Use **"that"** (not "which")
- **No comma** before the clause
- Removing the clause changes the meaning

```{prf:example}
- Incorrect: "The sample which was exposed to high temperatures showed changes."
- Correct: "The sample **that** was exposed to high temperatures showed changes."
- *Why*: We're identifying a specific sample
```

### Non-Restrictive Relative Clauses (Extra Information)

- Use **"which"** (not "that")
- **Comma** before the clause
- Removing the clause doesn't change core meaning

```{prf:example}
- Incorrect: "The crystalline sample that was stored in a vacuum chamber showed changes."
- Correct: "The crystalline sample **, which** was stored in a vacuum chamber, showed changes."
- *Why*: The storage detail is helpful but not essential
```

## Revision Strategies

### Using Generative AI Tools (Proceed with Caution)

**Do:**
- Use for formal revisions (grammar, style)
- Check everything thoroughly
- Document all AI use with prompts and responses
- Use iteratively, maintaining human control

**Don't:**
- Let AI modify your content
- Allow AI to stray from your original meaning
- Use AI for content generation
- Trust AI without verification

```{prf:example}
- Original: "An account of a stand-alone energy device (off-grid system) that combines an energy harvesting technology with a lithium-ion battery is also provided."
- AI Revision: "We also provide a description of a standalone energy device (off-grid system) that combines an energy harvesting technology with a lithium-ion battery."
- Human Revision: "We also describe a standalone energy device combining energy harvesting with a lithium-ion battery."
```

### Using Search Engines (Google as a Writing Tool)

Search engines provide valuable insights into usage patterns:

```{prf:example} Checking "data is" vs "data are"
- "Data are": ~100M hits
- "Data is": ~500M hits
- **Conclusion**: Both acceptable, but be consistent
```

```{prf:example}
- "all the developed countries" vs "all of the developed countries" -> Former more common
- "interested in what they eat" vs "interested with what they eat" -> Former favored by 6 orders of magnitude
```

```{tip} Dictionary + Search Engine = Perfect Match
Check word meanings in dictionaries, then verify usage patterns with search engines.
```

## Writing Checklist

### Pre-Writing
- Understand the State of the Art
- Provide references to all sources
- Identify target audience

### During Writing
- Be ultra-careful with abstract and introduction
- Ensure macro-level cohesion
- Provide evidence for original claims
- Provide references for specialized knowledge
- Keep sentences reasonably short (~20 words)

### Grammar & Style
- Ensure sentence accuracy
- Maintain conciseness
- Achieve clarity
- Verify coherence
- Check sentence length
- Verify article usage
- Use parallel structures
- Clarify pronoun antecedents
- Use correct relative clauses
- Verify punctuation

### Final Steps
- Proofread thoroughly
- Check consistency (UK vs US spelling)
- Verify all citations
- Ensure proper figure/table labels

## Research Paper Structure

```{list-table}
:header-rows: 1
:widths: 20 10 30

* - Section
  - Required
  - Notes
* - Abstract
  - Yes
  - Always present
* - Introduction
  - Yes
  - Always present
* - Related Work
  - Yes
  - Always there, but position varies; may be before the conclusion
* - Description of Contribution
  - No
  - Flexible structure; there may be a section on methodology
* - Evaluation
  - No
  - Flexible structure; there may be a section on methodology
* - Conclusion
  - Yes
  - Always there (there may also be acknowledgements in between)
* - Bibliography
  - Yes
  - Always there (there may also be acknowledgements in between)
```

## Types of Academic Writing

```{list-table}
:header-rows: 1
:widths: 25 40 35

* - Type
  - Description
  - Key Characteristics
* - Scientific Publications
  - Peer-reviewed journals, magazines, conferences
  - Surveys, position papers, research papers, book chapters
  - Rigorous peer review, evidence-based, structured
* - Technical Reports
  - Internal or external documentation
  - Detailed methodology, results, conclusions
  - Often proprietary, less formal
* - Theses
  - Hybrid between technical reports and scientific publications
  - Depends on adviser and institutional culture
  - Extensive literature review, original research
* - Funding Proposals
  - Requests for research funding
  - Clear objectives, methodology, expected impact
  - Persuasive yet accurate
* - Paper Reviews
  - Critical assessment of others' work
  - Structured feedback (summary, strengths, weaknesses)
  - Anonymous, constructive
```

## Peer Review Process

Peer review is a critical component of academic quality control.

```{note} Peer Review Beyond Papers
The same concept applies to any form of writing. Feedback from colleagues is also a form of peer review.
```

### How Peer Review Works (Academic Context)

- **Definition**: Having peers assess work prior to publication
- **Format**: Always written, generally anonymous
- **Peers**: People from the same field
- **Purpose**: Quality control for conferences/journals
- **Limitation**: Not always sufficient (lack of incentives)

### Standard Review Structure

1. **Paper Summary**: Brief overview of content and contributions
2. **Strengths**: Positive aspects (implementation, results, hardware)
3. **Weaknesses**: Issues identified (readability, scientific motivation)
4. **Detailed Comments**: Specific, actionable feedback
5. **Confidential Comments**: For editors only

## Glossary

:::{glossary}
Toulmin Method
: A framework for constructing logical arguments, consisting of six components: claim, grounds, warrant, backing, rebuttal, and qualifier.

ACCC Principles
: The four principles of effective technical writing: Accuracy, Clarity, Conciseness, Coherence.

Restrictive Relative Clause
: A clause that provides essential information about the noun it modifies; uses "that" without a comma.

Non-Restrictive Relative Clause
: A clause that provides extra, non-essential information; uses "which" with a preceding comma.

Peer Review
: The process of having work evaluated by others in the same field prior to publication or acceptance.

h-index
: Hirsh index; a bibliometric indicator: the maximum value of h such that an author has published h papers that have each been cited at least h times.

Four Elements Framework
: A presentation improvement framework consisting of Air (design), Water (story), Earth (content), and Fire (delivery).

Generative AI
: Artificial intelligence systems that can generate text, images, or other content; must be used cautiously in academic writing.
:::