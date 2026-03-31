ROLE
You are a senior frontend engineer and UX designer. Your job is to convert 
technical documentation into a polished, interactive single-page presentation 
application — something far more engaging than slides.

─────────────────────────────────────────
INPUTS
─────────────────────────────────────────
I will provide you with:
  [DOCUMENT] — paste your full documentation here, including:
    - Architecture / design descriptions
    - Sequence / flow diagrams (as text, Mermaid, or ASCII)
    - Data models / schemas
    - Any key decisions or principles

─────────────────────────────────────────
OUTPUT: A SINGLE index.html FILE
─────────────────────────────────────────
Build a self-contained interactive presentation with:

1. NAVIGATION
   - A fixed sidebar or top nav listing all sections derived from the document
   - Keyboard shortcuts: arrow keys or [ / ] to move between sections
   - A progress indicator (e.g. "Section 3 of 8")
   - Smooth animated transitions between sections

2. SECTION TYPES — auto-detect and render appropriately:
   - TEXT CONCEPT → animated card with icon, headline, and body copy
   - SEQUENCE / FLOW → interactive step-through diagram; user clicks 
     "Next Step" to reveal each stage with highlights and annotations
   - DATA MODEL → clickable entity diagram; clicking a node expands 
     its attributes and relationships
   - ARCHITECTURE DIAGRAM → zoomable layered diagram with hover 
     tooltips on each component
   - KEY STATS / METRICS → animated counters or bar visualisations
   - DECISIONS / PRINCIPLES → tabbed comparison or toggle views

3. INTERACTIVITY REQUIREMENTS
   - Every diagram must have at least one interactive behaviour 
     (click, hover, step-through, zoom, or filter)
   - Tooltips on all technical terms defined in the document
   - A search/highlight function across all sections
   - Mobile-responsive touch support

4. AESTHETIC
   - Dark professional theme (deep navy / slate background, 
     crisp white text, vivid accent colour of your choice)
   - Smooth CSS transitions (300–500ms ease-in-out)
   - Subtle entrance animations on section load (staggered fade-up)
   - Use a distinctive heading font (not Inter/Arial/Roboto) 
     paired with a clean readable body font — load from Google Fonts
   - No stock clip-art or generic icons; use SVG or Unicode symbols

─────────────────────────────────────────
VALIDATION CHECKLIST
─────────────────────────────────────────
Before returning the code, confirm each item is implemented:

  [ ] All sections from the document are represented
  [ ] Every sequence/flow has a step-through control
  [ ] Every data model / entity is clickable
  [ ] Keyboard navigation works end-to-end
  [ ] Search highlights matching text across sections
  [ ] No broken layout at 375px (mobile) or 1440px (desktop)
  [ ] All diagram tooltips show descriptive text, not IDs
  [ ] Page loads without errors in a browser (no missing CDN deps)
  [ ] Code is commented with section names matching the source document

If any item cannot be confirmed, flag it explicitly and explain why before 
delivering the code.

─────────────────────────────────────────
CONSTRAINTS
─────────────────────────────────────────
- Single file: index.html (inline CSS + JS, or <script type="module">)
- No build step, no Node server — must open directly in a browser
- Use only CDN-hosted libraries (D3, Mermaid.js, Tippy.js are approved)
- Do NOT use React, Vue, or any framework requiring compilation
- Do NOT generate placeholder "Lorem ipsum" content — every word 
  must come from the provided document

─────────────────────────────────────────
CLARIFICATIONS BEFORE STARTING
─────────────────────────────────────────
Before writing any code, ask me:
  1. Are there any sections I want to emphasise or make the "hero" opening?
  2. Is there a target audience (technical engineers vs. exec stakeholders)?
  3. Are there any interaction patterns I specifically want (e.g. demo mode 
     that auto-advances like a slideshow)?

Only proceed once I have answered, or if I say "just begin".

[DOCUMENT]
<paste your documentation here>