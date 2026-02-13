## 1. Overview
This repository contains a Proof of Concept (PoC) exploring how brand guidelines can be structured as explicit knowledge rather than injected as unstructured context into generative models.

The goal is not to replace generative models, but to provide a structured knowledge layer that enables more controlled and traceable brand-consistent outputs.

This experiment addresses a practical problem:

As brand rules grow in complexity, injecting large JSON blocks into prompts becomes difficult to scale and reason about.

## 2. Problem Context
In many generative workflows, brand rules are:

Stored as large JSON documents
Injected entirely into model context
Interpreted implicitly by the model

This works in early stages, but as the number of brands, campaigns, and constraints increases, the system becomes:
Context-heavy instead of context-aware
Difficult to debug
Hard to scale consistently

The core issue is not generation quality — it is knowledge representation.

## 3. Approach
This PoC explores a structured, query-based approach:
Instead of treating brand guidelines as static text, they are modeled as connected entities with explicit relationships.

The system introduces:
A lightweight knowledge schema (RDF-style modeling)
Explicit relationships between Brand, Campaign, Typography, Imagery Rules, and Visual Anchors
Query-based context assembly (SPARQL)
Validation guardrails using SHACL

The objective is simple:
Shift from brute-force context injection
to selective, structured context assembly.

## 4. Key Concepts

🔹 Knowledge-First Modeling
Brand rules are represented as structured data rather than descriptive text.

The system queries relevant constraints instead of sending all rules to the model.

🔹 Spec-Driven Prompt Assembly
Prompts are constructed from structured data retrieved for a specific campaign.

This separates:
Visual narrative context
Graphic constraints (typography, logo usage)
Style guidance
Negative constraints

The prompt becomes a compiled output of structured knowledge.

🔹 Constraint Awareness
The schema distinguishes between:
Positive style guidance
Negative restrictions
Campaign-specific overrides

This creates a clearer separation between hard constraints and creative flexibility.

## 5. Repository Structure

### schema.ttl
Knowledge Schema
Defines entities and relationships between:
Brands
Campaigns
Typography rules
Imagery constraints
Visual anchors

This separates conceptual elements from graphic assets.

### data.ttl
Brand Instance Data
Contains structured data representing a sample brand scenario, including:

Typography preferences
Logo usage rules
Style constraints (e.g., no neon)
Visual anchor definitions
query.sparql — Context Assembly Logic
Retrieves campaign-specific constraints and compiles them into a structured system prompt.

This demonstrates selective retrieval instead of full-context injection.
shapes.ttl — Validation Rules
Defines SHACL constraints to ensure structural integrity of the dataset.
For example:

Preventing campaigns without required visual anchors
Ensuring mandatory relationships exist

## 6. Scope & Limitations
This PoC does not:
Implement automated conflict resolution
Include advanced rule precedence logic
Optimize for latency
Replace model reasoning

It focuses specifically on demonstrating structured knowledge representation and selective context assembly.

## 7. Why This Matters
As generative systems scale across multiple enterprise brands, consistency and traceability become more important than raw generation capability.

This PoC illustrates how structured knowledge modeling can:
Improve scalability
Increase traceability
Reduce brittle prompt engineering
Provide a foundation for future constraint-aware agents

It is not a finished system, but a structural step toward more controllable generative workflows.
