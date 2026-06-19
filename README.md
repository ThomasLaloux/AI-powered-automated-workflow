# AI-powered document generation under constraints

## Context
- Multi-agent system for automated drafting of professional business documents under formatting and data-confidentiality constraints. Replaces a manual process consuming 20–40 hours per month.

## Business constraints
- Flexibility of use between LLMs/SLMs
- Keeping historical data local
- Generating word and pdf documents
- Human in the loop: intermediary status and final validation
- Sending the final document by email to the client, after second HITL validation
- Data confidentiality

## Inputs/Output
- Inputs: historical document database, new client-specific data and context
- Output: structured Word document (filled in section by section) → validated → PDF created → delivered to the client.

## Tech stack
- Python · n8n · Qdrant · PostgreSQL · Docker · Ollama · SLMs (Qwen, Mistral) · LLM APIs (Anthropic/OpenAI/Mistral)

## Architecture
- A balance between tools: n8n for the orchestration layer, python (through http nodes) for the multi-agents layer through an iterative secondary workflow
  n8n handles orchestration to keep the agentic logic isolated and swappable; Python via HTTP nodes captures the agent logic, as well as for code clarity and testability
- Four specialized agents in charge of text generation in multi-agentic phase A: planner → writer → validator (scoring) → assembler
- RAG is used to extract key information from historical data stored on local drive
- Both cloud LLM (Mistral, Anthropic, OpenAI mainly) and self-hosted SLM (e.g. Mistral on Ollama) can be used, depending on the client's preferences
- Docker containers used for portability while running the workflow in a production environment; containers: n8n, agent, postgres, qdrant
- n8n workflow (green box: multi-agents layer, yellow box: human in the loop form + iterations):

### Schematic diagram
<img width="663" height="702" alt="schematic_workflow" src="https://github.com/user-attachments/assets/d5d58e21-3210-4fda-a563-d4c6624b52a2" />

### n8n workflow
<img width="1571" height="628" alt="AI_workflow_automation_v1 5" src="https://github.com/user-attachments/assets/8f8d0be9-9c27-4357-8ff9-459b42c37751" />

## Governance / Risk Management
- Two 'human in the loop' nodes are implemented for control and risk management right after both agentic parts, with feedback forms and iterative corrective loops
- Activable SLMs to fully host the process and further ensure data confidentiality (e.g. for regulated sectors)
- Container isolation
- Workflow summary, reject reasons, intermediary drafts, internal states (feedback, plan, progress) stored locally for audit purposes 

## How to run
- Required API keys (Anthropic / OpenAI / Mistral) and local Ollama
- Required documents folder mounted at /data.
- Run with docker-compose up

## Outcomes
- Time savings: 20-40h a month in operational processes, more time for other files, clients or strategic actions.
- 24-48k EUR a year at a 100 EUR hourly rate + reduced number of errors and avoided opportunity costs.
