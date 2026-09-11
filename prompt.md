# Role & Context
You are a Principal Software Engineer and Language Architect specializing in TypeScript, Compiler Technologies, Design System Engines, and Open-Source Infrastructure. 

You are tasked with architecting a standalone, world-class, framework-agnostic **Typography Engine & Type System** in TypeScript. 
This system will serve as a foundational building block for a larger enterprise content/email rendering engine, but it must also be published as an open-source library  capable of standing completely on its own.

The implementation must strictly adhere to the highest standards of software craftsmanship: 
idiomatic TypeScript, 
absolute type safety, 
zero generic `any`, 
clean domain abstractions, 
bulletproof unit testing, 
comprehensive JSDoc documentation, 
and zero runtime overhead for pure type operations.

---

## Technical Context & Architectural Mandates

### 1. Unified Reference Landscape & Core Dependencies
Your design must synthesize, merge, and extend the patterns established in the following industry-standard type specifications and open-source models:
* **Markdown AST (`mdast` v3):** `https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/mdast/v3/index.d.ts` (For semantic block & inline typography nodes: Heading, Paragraph, Strong, Emphasis, InlineCode, Blockquote).
  
* **HTML AST (`hast` v2):** `https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/hast/v2/index.d.ts` (For element properties, inline styling attributes, and DOM transformation targets).
  
* **Unlayer Shared Elements:** `https://github.com/unlayer/elements/blob/main/packages/shared/src/types.ts` (For component prop bags and decoupling layout logic from style props).
  
* **React Email Head & Typography Shell:** `https://github.com/resend/react-email/blob/main/packages/react-email/src/components/head/head.tsx` (For web font injection, font-family fallbacks, and Outlook mso font normalization).
  
* **MJML Core & Typography Schemas:** `https://github.com/mjmlio/mjml/tree/master/packages/mjml-core` & `@types/mjml` (For client-safe line-height, font-size locking, and unit normalization).

### 2. Core Functional Requirements

#### A. Design Token Schema & Type Contracts (`TypographyTokens`)
* **Font Family Stack:** Support multi-tier font fallback chains (e.g., `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif`). Must distinguish between Web Fonts (Google Fonts/Custom @font-face) and Native System Fallbacks.
  
* **Typographic Scale & Units:** Strict, type-safe representation of font sizes, line heights, letter spacings, and font weights (`100` through `900` + named strings like `'bold'`, `'medium'`).
  
* **Unit Normalization:** Enforce email-safe units. Automatic conversion or validation between unitless line-height multipliers (e.g., `1.5`) and explicit pixel values (e.g., `'24px'`) necessary for Outlook and legacy renderers.
  

#### B. Component & Node Prop Interfaces (`TypographyProps`)
* Implement clean discriminated interfaces for typographic elements: `HeadingProps` (with `depth: 1 | 2 | 3 | 4 | 5 | 6`), `ParagraphProps`, `CaptionProps`, `CodeBlockProps`, and `InlineTextProps`.
  
* Support text transform (`uppercase`, `lowercase`, `capitalize`), text alignment (`left`, `center`, `right`, `justify`), text decoration (`underline`, `line-through`), and color tokens.


---

## Expected Output Structure & Deliverables

Your response must be delivered in a clear, modular, and professional format containing the following 5 complete sections:

### 1. Executive Architectural Specification
* High-level domain analysis and architectural decision records (ADRs).
* Class and Type Relationship Diagrams (ASCII/Mermaid format).
* Explanation of how `mdast`, `hast`, and `Unlayer` interfaces are merged without structural conflicts.

### 2. Complete, Production-Ready TypeScript Core (`src/`)
Provide clean, idiomatic, fully-typed TypeScript code across these exact modules (no `// TODO` or truncated implementation allowed):
* `src/types/tokens.ts`: Design token interfaces, brand types, scale definitions, and utility type helpers.
* `src/types/nodes.ts`: AST-compatible typography node props and discriminated unions.
* `src/constants/defaults.ts`: Standard fallback font stacks (Sans, Serif, Mono), scale defaults, and reset styles.
  


### 3. Open-Source API Design & JSDoc Documentation
* Every exported type, interface, class, and method must include comprehensive JSDoc comments containing `@example`, `@param`, `@returns`, and `@throws` tags.
* Establish clear, intuitive naming conventions suitable for open-source publication on npm under `@email-ast/typography`.

### 4. Comprehensive Test Suite (`tests/`)
Provide a complete, zero-dependency test file written using Node.js Native Test Runner (`node:test`) and strict assertions (`node:assert`):
* Test token validation and default fallback application.
* Test unit normalization (e.g., unitless to `px` conversion for line heights).
* Test serialization of style props to inline CSS strings.
* Test edge cases: invalid font weights, missing fallbacks, and dangerous CSS injections.

### 5. Developer Guide & Open-Source Package README (`README.md`)
* Detailed documentation explaining how to install, import, and integrate the typography engine into external frameworks or custom compiler pipelines.
* Code snippets demonstrating integration with `mdast`/`hast` processors and `oclif` CLI tools.

---

## Quality Bar & Technical Constraints
1. **Zero `any` Policy:** Use explicit generics, `unknown`, type narrowing, type predicates, or conditional types where flexibility is required.
2. **Immutability:** All token configurations and engine instances must be strictly immutable (`Readonly<T>` / `Object.freeze`).
3. **Performance:** Type operations must compile cleanly without triggering excessive recursion depth limits in TypeScript compiler (`tsc`).
4. **Zero External Runtime Dependencies:** Core types and compilers must depend strictly on TypeScript standard libraries and native JS built-ins.

   
