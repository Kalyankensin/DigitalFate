
![banner](https://github.com/user-attachments/assets/eecc3b3f-313c-41aa-a28f-0c10b64d61b6)

# What is DigitalFate?

DigitalFate provides an advanced, enterprise-ready framework for orchestrating LLM calls, agents, and computer-based tasks in a cost-efficient manner. It delivers reliable systems, scalability, and a task-oriented architecture to handle real-world applications effectively.

**Key Features:**

- **Scalable for Production**: Effortlessly deploy on AWS, GCP, or locally via Docker.
- **Task-Focused Architecture**: Execute tasks at varying levels of complexity:
  - Simple tasks through LLM calls.
  - Intermediate tasks using V1 agents.
  - Advanced automation with V2 agents and MCP integration.
- **MCP Server Compatibility**: Leverage multi-client processing for high-performance operations.
- **Secure Tool-Calling Server**: Manage tools with robust API interactions.
- **Computer Use Integration**: Perform human-like tasks with Anthropic's ‘Computer Use’ capabilities.
- **Easy Tool Integration**: Add custom or MCP tools with a single line of code.
- **Client-Server Architecture**: A stateless, enterprise-ready system designed for production.

<br>
<br>

# 🛠️ Getting Started

### Prerequisites

- Python 3.10 or newer
- OpenAI or Anthropic API keys (supports Azure and Bedrock)

## Installation

### Installing via Smithery

To install DigitalFate for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@koducoder/DigitalFate):

```bash
npx -y @smithery/cli install @koducoder/DigitalFate --client claude
```

### Manual Installation
```bash
pip install digitalfate
```

## Basic Example

```python
from digitalfate import digitalfateClient, ObjectResponse, Task, AgentConfiguration
from digitalfate.client.tools import Search

# Initialize Client and Configure
client = digitalfateClient("localserver")
client.set_config("OPENAI_API_KEY", "YOUR_API_KEY")

# Define Task and Agent
task1 = Task(description="Research latest news in Anthropic and OpenAI", tools=[Search])

product_manager_agent = AgentConfiguration(
    job_title="Product Manager",
    company_url="https://digitalfate.ai",
    company_objective="To build an AI agent framework that helps people accomplish tasks",
)

# Execute Task with Agent
client.agent(product_manager_agent, task1)

result = task1.response

print(result)
```

# Advanced Example

```python
from digitalfate import digitalfateClient, ObjectResponse, Task, AgentConfiguration
from digitalfate.client.tools import Search

# Create a DigitalFate client instance
client = digitalfateClient("localserver")
client.set_config("OPENAI_API_KEY", "YOUR_API_KEY")
client.default_llm_model = "openai/gpt-4o"

# DeepSeek Chat

client.set_config("DEEPSEEK_API_KEY", "YOUR_DEEPSEEK_API_KEY")
client.default_llm_model = "deepseek/deepseek-chat"

# Claude-3.5-Sonnet

client.set_config("ANTHROPIC_API_KEY", "YOUR_ANTHROPIC_API_KEY")
client.default_llm_model = "claude/claude-3-5-sonnet"

# GPT 4o on Azure
client.set_config("ANTHROPIC_API_KEY", "YOUR_ANTHROPIC_API_KEY")
client.default_llm_model = "claude/claude-3-5-sonnet"

# Claude 3.5 Sonnet on AWS
client.set_config("AWS_ACCESS_KEY_ID", "YOUR_AWS_ACCESS_KEY_ID")
client.set_config("AWS_SECRET_ACCESS_KEY", "YOUR_AWS_SECRET_ACCESS_KEY")
client.set_config("AWS_REGION", "YOUR_AWS_REGION")
client.default_llm_model = "bedrock/claude-3-5-sonnet"
```

# Task Definition

Tasks are defined by their descriptions. High-level tasks are broken into manageable sub-tasks automatically. For example, the task "Research latest news in Anthropic and OpenAI" may result in subtasks like:

"Search for Anthropic and OpenAI news on Google."
"Read relevant blogs."
"Review official announcements."

# Define Task Description

```python
description = "Research latest news in Anthropic and OpenAI"
```

# Task Execution

Combine agents and tasks, then run them using the DigitalFate server. This approach simplifies task execution in SaaS applications or vertical AI systems.

```python
client.agent(product_manager_agent, task1)

result = task1.response

for item in result.news_list:
    print("\nNews")
    print("Title: ", item.title)
    print("Body: ", item.body)
    print("URL: ", item.url)
    print("Tags: ", item.tags)
```

<br> <br>

# Additional Features (Beta)

## Single LLM Call

Optimize cost and latency by deciding when to directly call an LLM instead of deploying agents.

```python
client.call(task1)
```

## Memory System

Enable personalized, context-aware interactions by leveraging memory settings in AgentConfiguration.

```python
product_manager_agent = AgentConfiguration(
    agent_id="product_manager_agent",
    memory=True,
)
```

## Knowledge Base

Provide agents with context through private or public content, such as PDFs or URLs.

```python
from digitalfate import KnowledgeBase

kb = KnowledgeBase(files=["sample.pdf", "https://digitalfate.ai"])

task1 = Task(context=[kb])
```

## Task Chaining

Link tasks together by using the output of one as the input for another.

```python
task2 = Task(context=[task1])
```

## Multi-Agent Collaboration

Distribute tasks across multiple agents for collaborative problem-solving.

```python
client.multi_agent([agent1, agent2], [task1, task2])
```

## Human-Like Agents

Configure agents with names and contact information for tasks requiring personal interaction.

```python
product_manager_agent = AgentConfiguration(
    name="John Walk",
    contact="john@digitalfate.ai",
)
```

## Computer Use

Perform tasks that require human-like interactions, such as mouse movements and clicks.

```python
from digitalfate.client.tools import ComputerUse

tools = [ComputerUse]
```

## Reflection Mechanism

Ensure high-quality outputs by validating results and providing feedback for improvements.

```python
product_manager_agent = AgentConfiguration(
    reflection=True,
)
```

## Context Compression

Handle context overflow scenarios by compressing system messages and inputs automatically.

```python
product_manager_agent = AgentConfiguration(
    compress_context=True,
)
```

## Telemetry

Disable anonymous telemetry by setting an environment variable.

```python
import os
os.environ["digitalfate_TELEMETRY"] = "False"
```

# License

DigitalFate is licensed under the MIT License. See the full license text below:

---

## MIT License

Copyright (c) 2025 DigitalFate

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---

