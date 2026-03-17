
***

# 🌌 Aether: Fully Automated AI Research Orchestrator for Telecommunications

> From initial inspiration to a finalized paper, Aether is an end-to-end automated multi-agent workflow engine for telecommunications research.

Aether is a sophisticated, deep-automation multi-agent system designed specifically for researchers in the telecommunications domain. It autonomously manages the entire research lifecycle: brainstorming novel ideas, writing and testing Python simulation code, executing large-scale parameter sweeps, drafting IEEE-formatted LaTeX papers, and even conducting simulated peer reviews followed by automated revisions.

---

## 👁️ Vision

Modern telecommunications research involves complex theoretical derivations, tedious simulation tuning, and strict formatting requirements. Aether's vision is to liberate researchers from heavy, repetitive engineering tasks and boilerplate coding. By introducing an adversarial "Teacher-Student" planning mechanism and a highly concurrent agent architecture, Aether serves as your "24/7 AI Lab Manager." It empowers you to focus purely on high-level innovation and core architectural design.

---

## ✨ Core Features

* **👥 Multi-Agent Collaboration Architecture**
    * Built-in specialized roles including the Orchestrator, Student Planner, Teacher Critic, and Coder Agent, each executing specific responsibilities.
    * Supports an Adversarial Plan Mode where the Student proposes a research plan and the Teacher rigorously audits it to ensure feasibility and novelty.
* **⚡ High-Concurrency Task Management**
    * An underlying asynchronous task manager supports spawning multiple coding tasks or running several Python simulation scripts simultaneously.
    * Real-time monitoring of system physical memory and GPU VRAM utilization prevents hardware resource overflow.
* **🔄 Deep Human-in-the-Loop (HITL)**
    * During the idea generation and plan breakdown phases, users can seamlessly intervene, provide feedback, request modifications, or reject proposals.
    * Supports real-time interruption during workflow execution; users can inject emergency instructions via the chat interface to instantly redirect the AI's thought process.
* **🛡️ Robust System Engineering**
    * Integrates a powerful `JSON Repair` mechanism that perfectly handles complex LaTeX formulas and invalid escape characters often outputted by LLMs.
    * Features automatic Git version control for the workspace; every meaningful action taken by the Orchestrator triggers an automatic commit to safeguard data.

---

## 🗺️ Workflow

Aether's pipeline is strictly divided into 6 distinct, sequential phases:

1.  **💡 Phase 1: Generate Ideas (`1_Generate_Ideas`)**
    * Multiple Student Agents brainstorm innovative concepts in parallel, based on the user's theme and the local codebase.
    * Teacher Agents automatically query external databases to perform rigorous Novelty Checks and assign scores.
    * The system provides an interactive UI for users to select, evaluate, and refine ideas using natural language instructions.
2.  **💻 Phase 2: Generate Code (`2_Generate_Code`)**
    * The Orchestrator dissects the research plan and commands Coder Agents to write Python simulation scripts.
    * Coders repeatedly test their code in an isolated environment until it meets the expected requirements and outputs.
3.  **🔬 Phase 3: Perform Experiments (`3_Perform_Experiments`)**
    * Automatically dispatches execution commands to perform parameter sweeps (e.g., SNR, number of antennas) based on the predefined baseline comparisons.
    * Concurrently collects performance and complexity data across different scenarios, formatting and recording the results.
4.  **📄 Phase 4: Writeup (`4_Writeup`)**
    * Automatically drafts a high-quality, IEEE TCOM-standard LaTeX paper utilizing the recorded simulation data and research plan.
    * Generates comprehensive modules including Abstract, System Model, and Numerical Results, ultimately invoking `pdflatex` to compile the PDF.
5.  **📝 Phase 5: AI Peer Review (`5_Review`)**
    * Conducts a macroscopic layout and logical preliminary review using a PDFReader.
    * AI Reviewers then dive deep into the underlying codebase to cross-verify the strict consistency between the `Python` simulation implementation and the mathematical formulas described in the `Tex` files, outputting detailed Major/Minor Comments.
6.  **🔧 Phase 6: Update From Reviews (`6_Update_From_Reviews`)**
    * The system reads the generated review comments and autonomously decides whether to rewrite text, fix code, or spawn new tasks to acquire additional experimental data.
    * Automatically rewrites the affected `.tex` sections and figures, saving the finalized, rebuttal-ready version.

---

## 🏗️ System Architecture

Aether features a loosely coupled, highly extensible hierarchical architecture:

* **UI & Interaction Layer**
    * A modernized, asynchronous Web UI built on `Chainlit` provides a real-time task Dashboard. It displays the current execution round, GPU status, active running tasks, and execution durations.
* **Central Orchestration Layer**
    * The core `AgentSystem` class maintains the global state machine, action history, and conversational summaries.
    * Utilizes a `BaseContextBuilder` to dynamically construct global Prompt contexts—including directory trees, task monitors, and hardware statuses—tailored for different phases (coding, writing, experimenting).
* **Task & Tooling Layer**
    * **TaskManager**: Responsible for spawning and destroying asynchronous subprocess threads, intercepting system `stdout`/`stderr`, and implementing hard timeout fail-safes.
    * **ToolRegistry**: A plug-and-play tool registration center offering standardized capabilities such as `READ_FILE`, `WRITE_FILE`, `SEARCH_LITERATURE`, and `SPAWN_CODER`.
    * **WorkspaceManager**: Recursively parses the workspace file tree, handles automatic Git commits, and manages breakpoint saving for experiment states.
* **LLM Backend Layer**
    * A highly encapsulated `LLMAgent` supports state-of-the-art large language models including OpenAI, Anthropic Claude, Google Gemini, and DeepSeek.
    * Features robust fault-tolerance via Exponential Backoff retry mechanisms and real-time streaming token output capabilities.

***

