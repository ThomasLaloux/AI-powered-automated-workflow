# AI-powered document generation

## Business constraints
- Flexibility of use between LLMs/SLMs
- Keeping historical data local
- Generating word and pdf documents
- Human in the loop: intermediary status and final validation
- Sending the final document by email to the client, after second HITL validation
- Data confidentiality

## Architecture
- A balance between tools: n8n for the orchestration layer, python (through http nodes) for the multi-agents layer through an iterative secondary workflow
- Four agents types for text generation: planner, developer, validator, assembler
- RAG is used to extract key information from historical data stored on local drive
- Two 'human in the loop' nodes have been foreseen for control and risk management right after both agentic parts, with feedback forms and iterative corrective loops
- Both cloud LLM (Mistral, Anthropic, OpenAI mainly) and self-hosted SLM (e.g. Mistral on Ollama) can be used
- Docker containers used for portability while running the workflow in a production environment; containers: n8n, agent, postgres, qdrant

## Outcomes
- An automated process running on self-hosted n8n (a user interface could also be proposed in v2)
- Time savings: 20-40h a month in operational processes, more time for managing other files or for strategic thinking/actions.
- 24-48k EUR a year at a 100 EUR hourly rate, without considerint the reduced number of errors and opportunity costs.
