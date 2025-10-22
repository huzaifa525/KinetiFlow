# Contributing to KinetiFlow

First off, thank you for considering contributing to KinetiFlow! 🎉

It's people like you that make KinetiFlow such a great tool. We welcome contributions from everyone, whether you're fixing a typo, adding a feature, or building a custom agent.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Building Custom Agents](#building-custom-agents)
- [Commit Message Guidelines](#commit-message-guidelines)

---

## Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to support@KinetiFlow.com.

---

## How Can I Contribute?

### 🐛 Reporting Bugs

Before creating bug reports, please check the [existing issues](https://github.com/huzaifa525/KinetiFlow/issues) to avoid duplicates.

When creating a bug report, include:
- **Clear title and description**
- **Steps to reproduce** the issue
- **Expected behavior** vs **actual behavior**
- **Screenshots** if applicable
- **Environment details** (OS, Docker version, browser)
- **Logs** from Docker containers if relevant

### 💡 Suggesting Features

Feature requests are welcome! Before submitting:
- Check if the feature already exists or is planned
- Provide a clear use case for the feature
- Explain how it would benefit other users

Open a [GitHub Issue](https://github.com/huzaifa525/KinetiFlow/issues/new) with the label `enhancement`.

### 📝 Improving Documentation

Documentation improvements are always appreciated:
- Fix typos or clarify existing docs
- Add examples and tutorials
- Translate documentation to other languages
- Create video tutorials or guides

### 🤖 Building Custom Agents

One of the best ways to contribute is by building custom agents! See the [Building Custom Agents](#building-custom-agents) section below.

### 🔧 Code Contributions

We welcome code contributions! See the [Development Setup](#development-setup) section to get started.

---

## Development Setup

### Prerequisites

- **Node.js 20+**
- **Python 3.11+**
- **Docker & Docker Compose**
- **pnpm** (frontend package manager)
- **Poetry** (Python package manager)
- **Git**

### Setup Instructions

```bash
# 1. Fork the repository on GitHub

# 2. Clone your fork
git clone https://github.com/YOUR_USERNAME/KinetiFlow.git
cd KinetiFlow

# 3. Add upstream remote
git remote add upstream https://github.com/huzaifa525/KinetiFlow.git

# 4. Install backend dependencies
cd backend
poetry install
poetry shell

# 5. Install frontend dependencies
cd ../frontend
pnpm install

# 6. Start infrastructure (Postgres, Redis, Weaviate)
cd ..
docker-compose up -d postgres redis weaviate

# 7. Run database migrations
cd backend
alembic upgrade head

# 8. Create admin user
python -m app.cli create-admin --email admin@test.com --password admin123

# 9. Start backend (in one terminal)
cd backend
uvicorn app.main:app --reload

# 10. Start Celery worker (in another terminal)
cd backend
celery -A app.worker worker --loglevel=info

# 11. Start frontend (in another terminal)
cd frontend
pnpm dev

# 12. Open browser
# Frontend: http://localhost:3000
# Backend API: http://localhost:8000/docs
```

### Running Tests

```bash
# Backend tests
cd backend
pytest

# Frontend tests
cd frontend
pnpm test

# E2E tests
pnpm test:e2e
```

---

## Pull Request Process

1. **Create a feature branch** from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes** following our [Coding Standards](#coding-standards)

3. **Write tests** for your changes (if applicable)

4. **Run tests** to ensure nothing breaks:
   ```bash
   # Backend
   cd backend && pytest

   # Frontend
   cd frontend && pnpm test
   ```

5. **Commit your changes** following [Commit Message Guidelines](#commit-message-guidelines)

6. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```

7. **Open a Pull Request** on GitHub with:
   - Clear title and description
   - Reference to related issue (if any)
   - Screenshots/GIFs for UI changes
   - Test results

8. **Address review feedback** if requested

9. **Wait for approval** - Maintainers will review and merge

### PR Checklist

- [ ] Code follows project style guidelines
- [ ] Tests added/updated and passing
- [ ] Documentation updated (if needed)
- [ ] Commit messages follow guidelines
- [ ] No merge conflicts
- [ ] Self-reviewed the code

---

## Coding Standards

### Python (Backend)

- **Style Guide:** PEP 8
- **Linting:** Use `black`, `isort`, `ruff`
- **Type Hints:** Use type hints for all functions
- **Docstrings:** Use Google-style docstrings

```python
# Example
from typing import List, Optional

def get_contacts(
    user_id: str,
    limit: int = 10,
    offset: int = 0
) -> List[Contact]:
    """
    Retrieve contacts for a user.

    Args:
        user_id: The unique user identifier
        limit: Maximum number of contacts to return
        offset: Number of contacts to skip

    Returns:
        List of Contact objects

    Raises:
        ValueError: If limit is negative
    """
    if limit < 0:
        raise ValueError("Limit must be non-negative")

    # Implementation...
    return contacts
```

**Format your code:**
```bash
cd backend
black .
isort .
ruff check .
```

### TypeScript/React (Frontend)

- **Style Guide:** Airbnb + Prettier
- **Linting:** ESLint + Prettier
- **Type Safety:** Use TypeScript, avoid `any`
- **Components:** Use functional components with hooks

```typescript
// Example
import { useState, useEffect } from 'react'

interface Contact {
  id: string
  name: string
  email: string
}

interface ContactListProps {
  userId: string
}

export function ContactList({ userId }: ContactListProps) {
  const [contacts, setContacts] = useState<Contact[]>([])
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    fetchContacts()
  }, [userId])

  async function fetchContacts() {
    // Implementation...
  }

  return (
    <div>
      {/* JSX */}
    </div>
  )
}
```

**Format your code:**
```bash
cd frontend
pnpm lint
pnpm format
```

### General Guidelines

- **Keep it simple** - Prefer clarity over cleverness
- **DRY** - Don't repeat yourself
- **SOLID principles** - Follow good OOP practices
- **Comments** - Explain "why", not "what"
- **Error handling** - Always handle errors gracefully
- **Security** - Never commit secrets or API keys

---

## Building Custom Agents

Agents are at the heart of KinetiFlow! Here's how to build one:

### Agent Structure

```python
# backend/app/agents/my_custom_agent.py

from app.agents.base import BaseAgent
from langgraph.graph import StateGraph, END
from typing import TypedDict, List

class MyCustomAgentState(TypedDict):
    input_data: str
    result: str

class MyCustomAgent(BaseAgent):
    """
    Description of what your agent does.

    This agent processes input and returns a result.
    """

    def _initialize_tools(self) -> List:
        """Initialize tools/functions the agent can use"""
        return [
            self._process_data,
            self._validate_result,
        ]

    def _build_graph(self) -> StateGraph:
        """Build the agent's state machine using LangGraph"""
        graph = StateGraph(MyCustomAgentState)

        # Add nodes
        graph.add_node("process", self._process)
        graph.add_node("validate", self._validate)

        # Add edges
        graph.add_edge("process", "validate")
        graph.add_edge("validate", END)

        # Set entry point
        graph.set_entry_point("process")

        return graph.compile()

    async def execute(self, input_data: dict) -> dict:
        """
        Main execution method called by KinetiFlow.

        Args:
            input_data: Input parameters for the agent

        Returns:
            dict: Results from agent execution
        """
        state = MyCustomAgentState(
            input_data=input_data.get("data", ""),
            result=""
        )

        result = await self.graph.ainvoke(state)
        return result

    async def _process(self, state: MyCustomAgentState) -> MyCustomAgentState:
        """Process the input data"""
        # Your logic here
        state["result"] = f"Processed: {state['input_data']}"
        return state

    async def _validate(self, state: MyCustomAgentState) -> MyCustomAgentState:
        """Validate the result"""
        # Your validation logic here
        return state
```

### Register Your Agent

```python
# backend/app/agents/registry.py

from app.agents.my_custom_agent import MyCustomAgent

AGENT_REGISTRY = {
    "email_parser": EmailParserAgent,
    "enrichment": EnrichmentAgent,
    "followup": FollowupAgent,
    "my_custom_agent": MyCustomAgent,  # Add your agent
}
```

### Test Your Agent

```python
# backend/tests/agents/test_my_custom_agent.py

import pytest
from app.agents.my_custom_agent import MyCustomAgent

@pytest.mark.asyncio
async def test_my_custom_agent():
    config = {
        "name": "test_agent",
        "use_local_llm": True,
    }

    agent = MyCustomAgent(config)

    result = await agent.execute({
        "data": "test input"
    })

    assert result["result"] == "Processed: test input"
```

### Submit Your Agent

Once your agent is ready:
1. Add documentation to `docs/agents/your-agent.md`
2. Add tests
3. Submit a Pull Request
4. (Optional) Publish to Agent Marketplace

---

## Commit Message Guidelines

We follow [Conventional Commits](https://www.conventionalcommits.org/) for clear commit history.

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks
- `perf`: Performance improvements
- `ci`: CI/CD changes

### Examples

```bash
# Feature
feat(agents): add voice AI agent for outbound calls

Added Twilio integration and voice transcription capabilities.
Supports 50+ languages with sentiment detection.

Closes #123

# Bug fix
fix(api): resolve contact duplicate issue on email import

Fixed race condition in email parser agent that caused
duplicate contacts when processing emails in parallel.

Fixes #456

# Documentation
docs(readme): update installation instructions

Added troubleshooting section for Docker Desktop on Windows.

# Refactoring
refactor(agents): extract common LLM logic to base class

Reduced code duplication across agents by moving shared
LLM initialization logic to BaseAgent class.
```

---

## Questions?

- **Discord:** [Join our community](https://discord.gg/KinetiFlow) (Coming soon)
- **GitHub Discussions:** [Ask questions](https://github.com/huzaifa525/KinetiFlow/discussions)
- **Email:** support@KinetiFlow.com (Coming soon)

---

## License

By contributing to KinetiFlow, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for contributing to KinetiFlow! 🚀**
