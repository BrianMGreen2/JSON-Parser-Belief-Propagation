# JSON Belief Propagation Diagram

This project is a lightweight interactive HTML page that renders a Mermaid sequence diagram as SVG to explain how fragile assumptions in JSON parsing can propagate through an AI system. The diagram shows how a model emits JSON-like output, a parser or validator tries to repair or coerce it, and downstream tools or stateful systems can inherit ambiguity, silent errors, or unintended side effects.

## What this is

The page visualizes a failure pattern common in LLM and agent workflows: a system treats malformed or partially valid JSON as “close enough,” then retries, patches, or coerces the payload until it passes a parser or schema validator. That local recovery step can create a false sense of correctness, because the system now behaves as if the data is trustworthy even when meaning was lost or changed during repair.

The diagram is rendered in the browser using Mermaid sequence diagram syntax, then exposed as SVG so it can be viewed online, downloaded, and reused in presentations, articles, or documentation. Mermaid supports sequence diagrams directly, which makes it a practical format for keeping the diagram editable in version control while still exporting a polished SVG output for sharing.

## Why it matters

In AI systems, JSON often gets treated as proof of correctness when it is really just a transport format or serialization layer. A payload can be syntactically parseable yet still be semantically wrong, partially truncated, silently coerced, or inconsistent with what a downstream tool expects.

That matters because downstream systems may act on the repaired payload as if it is valid: tools run with wrong arguments, validators perform best-effort type coercion, and stateful systems record side effects that are expensive to reverse. Research and practitioner discussions on multi-agent reliability increasingly emphasize that error propagation, brittle chains, and weak validation boundaries are major causes of failure in agentic systems.

The broader lesson is architectural: JSON is useful plumbing, but it is not the same thing as integration, semantic alignment, or governance. When teams rely on parser tolerance instead of strict contracts, they risk building hidden interoperability debt into their agent and tool pipelines.

## What it can be used for

This artifact is useful for:

- Blog posts and essays about JSON, interoperability, agent reliability, or AI architecture debt.
- Conference or workshop slides explaining how local parsing fixes create downstream error propagation in tool-using agents.
- Internal architecture reviews, especially when discussing schema validation, retry logic, tool contracts, and observability in LLM systems.
- Teaching material for AI governance, data interoperability, semantic validation, or safe agent design.
- Product and engineering documentation where an editable diagram is preferable to a static screenshot.

## How to use it

1. Open the HTML file locally or deploy it from a public GitHub repository to Vercel as a static page.
2. View the interactive diagram in the browser and use the built-in control to download the rendered SVG version for reuse in other tools.
3. Upload the exported SVG into Notion, slides, or documentation systems when you want a portable static asset.
4. Edit the Mermaid source in the HTML file if you want to adapt the narrative for a stricter-contract version, a multi-parser disagreement example, or a domain-specific variant such as healthcare AI or agent governance.

## Why the HTML version is useful

The HTML version is especially practical because it combines three things in one artifact: an editable Mermaid source, a browser-rendered diagram, and an export path to SVG. That makes it easy to keep the diagram in Git, publish it publicly through Vercel, and still maintain a reusable visual asset for downstream publishing workflows.
Unlike a flat image checked into a repo, the HTML version preserves the logic of the sequence diagram in text form. That makes revisions easier when the argument evolves, for example if the diagram needs to distinguish between syntax validity, schema validity, semantic validity, and execution safety.

## Core idea

The diagram is built around a simple claim: a parser error is not just a local formatting issue. In agentic systems, it can become a belief propagation problem, where the system moves from “this output might be wrong” to “this repaired output is probably safe,” and then acts on that belief downstream.
