🏦 Senior Mortgage Underwriting System

Multi-Agent System · Agent-to-Agent (A2A) · Model Context Protocol (MCP) · RAG · Human-in-the-Loop · DeepEval

Build a production-style underwriting workflow where specialist agents analyse a loan file, a Critic peer-reviews their work over A2A, a Decision Agent issues a verdict grounded in policy, and a senior underwriter signs off on the borderline cases - with every run scored by DeepEval.

🏢 Business Problem - Consistent, Auditable Loan Decisions

Mortgage underwriting is slow, manual, and inconsistent. A single application requires an underwriter to reconcile credit history, income stability, asset sourcing and property condition against a long policy manual - and two underwriters reading the same file can reach different conclusions. The work is repetitive enough to automate, yet high-stakes enough that automation cannot be careless.

A system that decides loans carries real risk: an approval that should have been declined exposes the lender to default; a decision that leans on a protected characteristic is a Fair Lending violation; a decision no one can explain fails an audit. The goal here is speed with a paper trail - compress the manual work into a single run, while grounding every judgement in the written policy and keeping a human on the file wherever discretion is required.

🏗️ Solution & Approach

The system is assembled from six layers, each mapped to a specific protocol or technology:

Layer	Technology	Role
Tool infrastructure	FastMCP server	Exposes the underwriting calculators and policy retrieval so agents never compute figures themselves
Orchestration	LangGraph (supervisor + specialists)	An LLM-planner Supervisor routes four specialists, drives a rework loop, and releases to the Decision Agent
Inter-agent review	A2A	The Critic is exposed as a standalone Agent-to-Agent service; the Supervisor calls it as a client
Policy grounding	RAG (Chroma + section-aware chunking)	Specialists cite the policy manual by section number instead of reasoning from memory
Human oversight	LangGraph interrupt() / Command	A conditional approval pauses the graph for a senior underwriter's sign-off
Evaluation	DeepEval	Six agentic metrics score the trace of every run and end in a single PASS/FAIL
