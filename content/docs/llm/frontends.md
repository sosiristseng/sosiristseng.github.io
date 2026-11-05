---
title: LLM front ends
tags:
- bookmarks
- ai
---

> Chat, general tasks, and coding agents

- [Hermes agent](https://hermes-agent.nousresearch.com/)
- [Lemonade](https://lemonade-server.ai/)
- [OpenWebUI](https://github.com/open-webui/open-webui) : User-friendly AI Interface supporting multiple backends.
- [Unsloth desktop](https://unsloth.ai/docs/desktop)
- [TinyWebUI](https://github.com/TinySuiteHQ/TinyWebUI)

## Coding agents

- [OpenCode](https://opencode.ai/) and [OpenChamber](https://openchamber.dev/).
- [Minimax code](https://github.com/MiniMax-AI/minimax-code) by Minimax.
- [Qwen code](https://github.com/qwenLM/qwen-code) by Qwen.
- [pi coding agent](https://pi.dev/): a minimalist agent. See also [oh-my-pi](https://github.com/can1357/oh-my-pi) for a preconfigured pi agent.

**Deepseek**

- [Codewhale](https://codewhale.net/): previously called `deepseek-tui
- [Deepseek harness (DSH)](https://www.deepseek.com/harness/) see also [Deepseek plugins](https://deepseekplugin.com/).
- [Reasonix](https://reasonix.io/) : cache-friendly harness for DeepSeek.

## MCP servers

> The [Model Context Protocol](https://en.wikipedia.org/wiki/Model_Context_Protocol) (MCP) is an open standard and open-source framework introduced by Anthropic in November 2024 to standardize the way artificial intelligence (AI) systems like large language models (LLMs) integrate and share data with external tools, systems, and data sources.

- [DuckDuckGo](https://github.com/nickclyde/duckduckgo-mcp-server)
- [Julia](https://github.com/aplavin/julia-mcp) : MCP server for persistent Julia sessions
- [Kaimon.jl](https://github.com/kahliburke/Kaimon.jl) : MCP server giving AI agents full access to Julia's runtime via a live Gate.

## Skills

> [Agent skills](https://agentskills.io/) are a lightweight, open format for extending AI agent capabilities with specialized knowledge and workflows.

### Julia

Running Julia code in with persistent Julia session(s) (with `Revise.jl`) to save package loading and JIT compilation time.

- [JuliaDaemon.jl](https://github.com/KristofferC/JuliaDaemon.jl): installs a `jld` skill for AI agents.
- [repld](https://github.com/Beforerr/repld) : stateful and persistent REPL-like kernel for fast incremental iteration.
