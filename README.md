# Production-grade-AI-powered-automated-workflow

This first multi-agentic project has a commercial purpose. Hence, the exact context and implementation won't be disclosed.

Technically speaking, the nature of this project and its constraints led to the following architectural decisions:
- a balance between tools used: n8n for the orchestration layer, python (through http nodes) for the multi-agents layer through an iterative secondary workflow
- four agents types: planner, writer, validator, assembler; RAG has been foreseen to extract key information from historical data stored on local drive
- since agents have been included in the process, two 'human in the loop' nodes have been foreseen for control and risk management, with feedback forms and iterative corrective loops
- LLM component: local (e.g. Mistral on Ollama) or cloud solution (Mistral, Anthropic, OpenAI mainly)
- Docker containers used for portability; they include: n8n, agent, postgres, qdrant
- Next step: thinking about a UI setup, if relevant
