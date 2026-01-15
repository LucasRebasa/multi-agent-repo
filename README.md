# Multi-Agent Repository

This repository demonstrates the organization of multiple Copilot agents for different purposes and technologies.

## Repository Structure

```
multi-agent-repo/
├── technologies/
│   ├── java/
│   │   └── .github/
│   │       ├── agents/
│   │       │   └── java-expert.agent.md
│   │       ├── instructions/
│   │       │   └── java-coding-standards.md
│   │       ├── examples/
│   │       │   └── spring-boot-example.md
│   │       └── docs/
│   │           └── java-patterns.md
│   └── node/
│       └── .github/
│           ├── agents/
│           │   └── node-expert.agent.md
│           ├── instructions/
│           │   └── node-best-practices.md
│           ├── examples/
│           │   └── express-server-example.md
│           └── docs/
│               └── node-architecture.md
└── use-cases/
    ├── planning/
    │   └── .github/
    │       ├── agents/
    │       │   └── project-planner.agent.md
    │       ├── instructions/
    │       │   └── planning-frameworks.md
    │       ├── examples/
    │       │   └── project-roadmap.md
    │       └── docs/
    │           └── planning-templates.md
    └── testing/
        └── .github/
            ├── agents/
            │   └── qa-specialist.agent.md
            ├── instructions/
            │   └── testing-methodologies.md
            ├── examples/
            │   └── test-automation.md
            └── docs/
                └── testing-frameworks.md
```

## Available Agents

### Technology-Specific Agents

#### Java Expert Agent
- **Location**: `technologies/java/.github/agents/java-expert.agent.md`
- **Purpose**: Java development, Spring Boot, enterprise patterns
- **Skills**: Maven/Gradle, JUnit 5, Spring ecosystem, design patterns

#### Node.js Expert Agent
- **Location**: `technologies/node/.github/agents/node-expert.agent.md`
- **Purpose**: Node.js development, TypeScript, microservices
- **Skills**: Express.js, MongoDB, testing frameworks, Docker

### Use-Case-Specific Agents

#### Project Planner Agent
- **Location**: `use-cases/planning/.github/agents/project-planner.agent.md`
- **Purpose**: Project planning, architecture design, agile methodology
- **Skills**: Roadmap creation, risk assessment, team coordination

#### QA Specialist Agent
- **Location**: `use-cases/testing/.github/agents/qa-specialist.agent.md`
- **Purpose**: Quality assurance, test automation, performance testing
- **Skills**: Unit testing, E2E testing, CI/CD integration

## How to Use

1. **Select the appropriate agent** based on your technology stack or use case
2. **Review the instructions** in the corresponding folder to understand best practices
3. **Check examples** for implementation patterns and code samples
4. **Reference documentation** for in-depth guidance and templates

## Organization Benefits

- **Modular Structure**: Each agent is self-contained with supporting materials
- **Consistent Layout**: All agents follow the same `.github` folder structure
- **Comprehensive Support**: Instructions, examples, and documentation for each domain
- **Scalable Design**: Easy to add new technologies or use cases following the same pattern

## Contributing

When adding new agents:

1. Follow the established folder structure
2. Include all four required subfolders: `agents`, `instructions`, `examples`, `docs`
3. Provide comprehensive examples and documentation
4. Maintain consistency in naming and formatting