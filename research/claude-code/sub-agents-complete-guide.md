# Claude Code Sub Agents: Complete Guide (2025)

## Table of Contents

1. [Introduction](#introduction)
2. [Core Concepts](#core-concepts)
3. [Architecture & Technical Implementation](#architecture--technical-implementation)
4. [Best Practices](#best-practices)
5. [Anti-Patterns & Common Mistakes](#anti-patterns--common-mistakes)
6. [Input/Output Patterns](#inputoutput-patterns)
7. [Agent Orchestration Patterns](#agent-orchestration-patterns)
8. [Creating Sub Agents](#creating-sub-agents)
9. [Meta Agents & Agent Generators](#meta-agents--agent-generators)
10. [Performance & Optimization](#performance--optimization)
11. [Real-World Examples](#real-world-examples)

## Introduction

Claude Code Sub Agents, introduced in 2025, represent a revolutionary advancement in AI-assisted development. These specialized AI assistants operate as independent instances of Claude Code, each with their own context window, custom system prompt, and specific tool permissions. This feature transforms single-threaded AI assistance into a distributed, self-coordinating agent network capable of handling tasks of arbitrary complexity and scale.

### Key Benefits

- **Parallel Processing**: Run up to 10+ agents simultaneously
- **Context Isolation**: Each agent has its own context window
- **Task Specialization**: Dedicated agents for specific domains
- **Improved Performance**: Multi-agent systems outperform single agents by 90.2%
- **Cost Optimization**: 40-60% cost savings in enterprise deployments

## Core Concepts

### What Are Sub Agents?

Sub agents are lightweight instances of Claude Code that can be invoked to handle specific types of tasks. They enable:

- **Task-specific configurations** with customized system prompts
- **Independent context windows** preventing context pollution
- **Specialized tool access** for security and efficiency
- **Automatic delegation** based on task requirements

### Key Components

Each sub agent consists of three core components:

1. **System Prompt**: Defines the agent's role, capabilities, and approach
2. **Context Window**: Stores task-specific information independently
3. **Toolset**: Equipped with utilities tailored to its purpose

## Architecture & Technical Implementation

### File Structure

Sub agents are implemented as Markdown files with YAML frontmatter:

```markdown
---
name: your-sub-agent-name
description: Description of when this subagent should be invoked
tools: tool1, tool2, tool3 # Optional - inherits all tools if omitted
model: haiku | sonnet | opus # Optional - defaults to sonnet
color: Cyan # Optional - visual identifier in terminal
priority: high # Optional - delegation preference
environment: production # Optional - environment-specific
team: backend # Optional - team-specific usage
---

Your subagent's system prompt goes here.
This can be multiple paragraphs and should clearly define:

- The subagent's role and expertise
- Specific capabilities and limitations
- Approach to solving problems
- Best practices to follow
- Any constraints or guardrails
```

### Storage Locations

```bash
# User-level agents (global across all projects)
~/.claude/agents/
├── security-code-reviewer.md
├── api-test-generator.md
├── performance-optimizer.md
└── tech-doc-generator.md

# Project-level agents (specific to current project)
.claude/agents/
├── project-code-reviewer.md
├── deployment-specialist.md
└── data-migration-expert.md
```

**Important**: When names conflict, project-level agents take precedence over user-level agents.

### Available Tools

These are all of the available tools in each category. You may mix and matc=
h as needed, but ensure you only include the minimal necessary tools for th=
e task.

- **Read-only tools**: Glob, Grep, LS, Read, WebFetch, TodoWrite, WebSearch, ListMcpResourcesTool, ReadMcpResourceTool
- **Edit tools**: Edit, MultiEdit, Write, NotebookEdit
- **Execution tools**: Bash
- **MCP tools**: (available tools depend on available MCP resources)

#### Tools Overview

| Tool | Description | Permission Required |
| ------------ | ---------------------------------------------------- | ------------------- |
| Bash | Executes shell commands in your environment | Yes |
| Edit | Makes targeted edits to specific files | Yes |
| Glob | Finds files based on pattern matching | No |
| Grep | Searches for patterns in file contents | No |
| LS | Lists files and directories | No |
| MultiEdit | Performs multiple edits on a single file atomically | Yes |
| NotebookEdit | Modifies Jupyter notebook cells | Yes |
| NotebookRead | Reads and displays Jupyter notebook contents | No |
| Read | Reads the contents of files | No |
| Task | Runs a sub-agent to handle complex, multi-step tasks | No |
| TodoWrite | Creates and manages structured task lists | No |
| WebFetch | Fetches content from a specified URL | Yes |
| WebSearch | Performs web searches with domain filtering | Yes |
| Write | Creates or overwrites files | Yes |

#### Note about MCP tools

MCP tools are only available if the agent has access to the MCP resources. =
Some examples of MCP tools (for GitHub Enterprise MCP and Playwright Browse=
r MCP) include:
mcp**github_enterprise**add*issue_comment, mcp**github_enterprise**add_pull=
\_request_review_comment_to_pending_review, mcp**github_enterprise**assign_c=
opilot_to_issue, mcp**github_enterprise**cancel_workflow_run, mcp**github_e=
nterprise**create_and_submit_pull_request_review, mcp**github_enterprise**c=
reate_branch, mcp**github_enterprise**create_issue, mcp**github_enterprise*=
*create_or_update_file, mcp**github_enterprise**create_pending_pull_request=
\_review, mcp**github_enterprise**create_pull_request, mcp**github_enterpris=
e**create_repository, mcp**github_enterprise**delete_file, mcp**github_ente=
rprise**delete_pending_pull_request_review, mcp**github_enterprise\*\*delete*=
workflow*run_logs, mcp**github_enterprise**dismiss_notification, mcp**githu=
b_enterprise**download_workflow_run_artifact, mcp**github_enterprise**fork*=
repository, mcp**github_enterprise**get*code_scanning_alert, mcp**github_en=
terprise**get_commit, mcp**github_enterprise**get_file_contents, mcp**githu=
b_enterprise**get_issue, mcp**github_enterprise**get_issue_comments, mcp**g=
ithub_enterprise**get_job_logs, mcp**github_enterprise**get_me, mcp**github=
\_enterprise**get_notification_details, mcp**github_enterprise**get_pull_req=
uest, mcp**github_enterprise**get_pull_request_comments, mcp**github_enterp=
rise**get_pull_request_diff, mcp**github_enterprise**get_pull_request_files=
, mcp**github_enterprise**get_pull_request_reviews, mcp**github_enterprise*=
*get_pull_request_status, mcp**github_enterprise**get_secret_scanning_alert=
, mcp**github_enterprise**get_tag, mcp**github_enterprise**get_workflow_run=
, mcp**github_enterprise**get_workflow_run_logs, mcp**github_enterprise**ge=
t_workflow_run_usage, mcp**github_enterprise**list_branches, mcp**github_en=
terprise**list_code_scanning_alerts, mcp**github_enterprise**list_commits, =
mcp**github_enterprise**list_issues, mcp**github_enterprise**list_notificat=
ions, mcp**github_enterprise**list_pull_requests, mcp**github_enterprise**l=
ist_secret_scanning_alerts, mcp**github_enterprise**list_tags, mcp**github*=
enterprise**list_workflow_jobs, mcp**github_enterprise**list_workflow_run_a=
rtifacts, mcp**github_enterprise**list_workflow_runs, mcp**github_enterpris=
e**list_workflows, mcp**github_enterprise**manage_notification_subscription=
, mcp**github_enterprise**manage_repository_notification_subscription, mcp*=
*github_enterprise**mark_all_notifications_read, mcp**github_enterprise**me=
rge_pull_request, mcp**github_enterprise**push_files, mcp**github_enterpris=
e**request_copilot_review, mcp**github_enterprise**rerun_failed_jobs, mcp**=
github_enterprise**rerun_workflow_run, mcp**github_enterprise**run_workflow=
, mcp**github_enterprise**search_code, mcp**github_enterprise**search_issue=
s, mcp**github_enterprise**search_orgs, mcp**github_enterprise**search_pull=
\_requests, mcp**github_enterprise**search_repositories, mcp**github_enterpr=
ise**search_users, mcp**github_enterprise**submit_pending_pull_request_revi=
ew, mcp**github_enterprise**update_issue, mcp**github_enterprise**update_pu=
ll_request, mcp**github_enterprise**update_pull_request_branch, mcp**playwr=
ight**browser_close, mcp**playwright**browser_resize, mcp**playwright**brow=
ser_console_messages, mcp**playwright**browser_handle_dialog, mcp**playwrig=
ht**browser_evaluate, mcp**playwright**browser_file_upload, mcp**playwright=
**browser_install, mcp**playwright**browser_press_key, mcp**playwright**bro=
wser_type, mcp**playwright**browser_navigate, mcp**playwright**browser_navi=
gate_back, mcp**playwright**browser_navigate_forward, mcp**playwright**brow=
ser_network_requests, mcp**playwright**browser_take_screenshot, mcp**playwr=
ight**browser_snapshot, mcp**playwright**browser_click, mcp**playwright**br=
owser_drag, mcp**playwright**browser_hover, mcp**playwright**browser_select=
\_option, mcp**playwright**browser_tab_list, mcp**playwright**browser_tab_ne=
w, mcp**playwright**browser_tab_select, mcp**playwright**browser_tab_close,=
mcp**playwright**browser_wait_for

### Model Selection

Choose models based on task complexity:

- **Haiku**: Simple tasks (data analysis, documentation, standard responses)
- **Sonnet**: Development tasks (code review, testing, standard engineering)
- **Opus**: Critical tasks (security auditing, architecture review, AI/ML engineering)

## Best Practices

### 1. Use Test-Driven Development (TDD)

```markdown
Ask Claude to:

1. Write tests based on expected input/output pairs
2. Run tests to confirm they fail
3. Write code that passes the tests
4. Iterate until all tests pass
```

### 2. Strategic Thinking with Extended Processing

Use trigger words for different thinking levels:

- `"think"` - Basic extended thinking
- `"think hard"` - More thorough evaluation
- `"think harder"` - Deep analysis
- `"ultrathink"` - Maximum computation time

### 3. Early and Strong Delegation

Delegate to sub agents early in conversations to:

- Preserve main context
- Investigate specific questions
- Verify details independently
- Handle exploration tasks

### 4. Leverage Parallel Processing

```markdown
# Example: Parallel codebase exploration

"Explore the codebase using 4 tasks in parallel.
Each agent should explore different directories."
```

### 5. Separate Read and Write Operations

```markdown
1. First: "Read the relevant files but don't write code yet"
2. Then: "Now implement the solution based on what you learned"
```

### 6. Clear Task Boundaries

Define:

- Specific objectives
- Expected output format
- Available tools and sources
- Clear completion criteria

### 7. Use Shared Workspaces for Communication

```markdown
# Agent communication pattern

Agent A writes to: /tmp/agent_a_output.md
Agent B reads from: /tmp/agent_a_output.md
Agent B writes to: /tmp/agent_b_output.md
```

## Anti-Patterns & Common Mistakes

### 1. DON'T Let Conversations Run Too Long

- Call `/clear` frequently
- Start fresh conversations for new topics
- Long contexts lead to unpredictable behavior

### 2. DON'T Over-specify Parallelism

- Let Claude Code decide parallelism levels
- System caps at 10 parallel tasks
- Automatic queuing handles overflow

### 3. DON'T Modify Tests During Implementation

- Write tests first
- Keep tests immutable
- Only modify code to pass tests

### 4. DON'T Use Sub Agents for Simple Tasks

Skip sub agents when:

- Single straightforward task
- Can be completed in <3 steps
- Purely conversational/informational
- No benefit from specialization

### 5. DON'T Ignore Context Window Limits

- Monitor token usage
- Use sub agents to offload context
- Clear unnecessary history regularly

## Input/Output Patterns

### Communication Flow

1. **Main Agent → Sub Agent**
   - Task description via system prompt
   - Specific objectives and constraints
   - Tool permissions
   - Expected output format

2. **Sub Agent → Main Agent**
   - Final report with results
   - No ongoing communication
   - Stateless execution
   - Structured output

### Standardized Protocol

```yaml
input:
  task: "Analyze performance bottlenecks"
  context: "React application with Redux"
  tools: [file_read, search_code]
  output_format: "markdown_report"

output:
  status: "completed"
  findings: [...]
  recommendations: [...]
  code_changes: [...]
```

### File System as Shared State

- Agents communicate through files
- Persistent across agent invocations
- Acts as shared workspace
- Enables complex coordination

## Agent Orchestration Patterns

### 1. Orchestrator-Worker Pattern

```markdown
Lead Agent (Orchestrator)
├── Analyzes user query
├── Develops strategy
└── Spawns 3-5 parallel workers
├── Worker 1: Frontend
├── Worker 2: Backend
└── Worker 3: Database
```

### 2. Sequential Pipeline

```markdown
requirements-analyst → system-architect → implementer → tester → reviewer
```

### 3. Parallel Execution

```markdown
Simultaneous execution:

- ui-engineer
- api-designer
- database-schema-designer
```

### 4. Hub-and-Spoke Pattern

```markdown
Central Hub (routing-agent)
├── Graph-based semantic analysis
├── JIT context loading
└── Routes to specialists
├── security-auditor
├── performance-optimizer
└── code-reviewer
```

### 5. Pipeline with Quality Gates

```markdown
Planning → Infrastructure → Implementation → Testing → Polish → Completion
(Each phase has mandatory quality checks)
```

### 6. Test-Implementation Separation

```markdown
Agent A: Write comprehensive tests
Agent B: Implement code to pass tests
(Separation prevents test modification during implementation)
```

## Creating Sub Agents

### Method 1: Interactive Creation (Recommended)

```bash
# In Claude Code
/agents

# Follow prompts to:
1. Select scope (project/personal)
2. Enter agent name
3. Choose tools
4. Define system prompt
```

### Method 2: Manual Creation

```bash
# Create agent file
touch ~/.claude/agents/my-agent.md

# Edit with your preferred editor
vim ~/.claude/agents/my-agent.md
```

### Method 3: Generate with Claude

```markdown
"Create a sub agent for security code review
that focuses on OWASP top 10 vulnerabilities"

Claude will generate:

- Appropriate name
- Detailed description
- Relevant tools
- Comprehensive system prompt
```

### Agent Template

```markdown
---
name: security-auditor
description: Performs security audits focusing on OWASP vulnerabilities
tools: file_read, search_code, terminal
model: opus # High complexity task
---

You are a security auditing specialist focused on identifying vulnerabilities.

## Your Expertise:

- OWASP Top 10 vulnerabilities
- Secure coding practices
- Dependency scanning
- Authentication/authorization issues

## Your Approach:

1. Scan for SQL injection vulnerabilities
2. Check for XSS attack vectors
3. Review authentication mechanisms
4. Identify exposed secrets/credentials
5. Analyze dependency vulnerabilities

## Output Format:

Provide a structured security report with:

- Critical findings (immediate action required)
- High priority issues
- Medium priority issues
- Recommendations for remediation
```

## Meta Agents & Agent Generators

### Concept

Meta agents are specialized agents that create other agents. They act as "agent architects" that generate complete, ready-to-use sub agent configurations from user descriptions.

### Meta Agent Template

```markdown
---
name: agent-generator
description: Creates new Claude Code sub agents from descriptions
tools: file_write
model: opus
---

You are an expert agent architect specializing in creating Claude Code sub agents.

## Your Process:

1. Analyze the user's requirements
2. Determine appropriate:
   - Agent name (kebab-case)
   - Action-oriented description
   - Required tools
   - Optimal model selection
3. Generate comprehensive system prompt
4. Create agent configuration file

## Agent Design Principles:

- Single responsibility principle
- Clear task boundaries
- Minimal tool permissions
- Detailed instructions
- Error handling guidance

## Output:

Generate a complete .md file with:

- YAML frontmatter
- Detailed system prompt
- Usage examples
- Best practices for the domain
```

### Usage Example

```markdown
User: "Create an agent that excels at creating other agents"

## Meta Agent generates:

name: meta-agent-creator
description: Generates specialized Claude Code sub agents from requirements
tools: file_write, file_read
model: opus

---

You are a meta-agent creation specialist...
[Complete configuration]
```

## Performance & Optimization

### Metrics

- **90.2% improvement** over single-agent systems
- **72.5% SWE-bench performance**
- **10 parallel agents** maximum concurrency
- **40-60% cost savings** in enterprise deployments

### Optimization Strategies

#### 1. Model Selection Optimization

```yaml
# Match model to task complexity
simple_task: haiku # $0.25/1M tokens
standard_task: sonnet # $3/1M tokens
complex_task: opus # $15/1M tokens
```

#### 2. Parallel vs Sequential Trade-offs

```markdown
Parallel: Fast but higher cost
Sequential: Slower but cost-effective
Hybrid: Parallel for independent tasks, sequential for dependent
```

#### 3. Context Window Management

```markdown
- Each agent: Independent 200K token window
- Main agent: Preserve for coordination
- Sub agents: Handle exploration/details
```

#### 4. Caching and Reuse

```markdown
- 15-minute cache for web fetches
- Shared file system state
- Reusable agent configurations
```

## Real-World Examples

### Example 1: Full-Stack Feature Development

```markdown
/task Create a user authentication system with JWT

Orchestrator spawns:

1. database-designer: Schema for users/sessions
2. api-developer: Auth endpoints
3. frontend-developer: Login/register UI
4. security-auditor: Review implementation
5. test-writer: E2E and unit tests
```

### Example 2: Performance Optimization

```markdown
/task Optimize React app performance

Sequential pipeline:

1. performance-analyzer: Identify bottlenecks
2. optimizer: Implement fixes
3. test-runner: Verify improvements
4. documenter: Update docs
```

### Example 3: Code Migration

```markdown
/task Migrate from JavaScript to TypeScript

Parallel agents:

- type-definition-creator
- code-converter
- test-updater
- documentation-updater
```

### Example 4: Security Audit

```markdown
/task Perform security audit

Hub-and-spoke:
Hub: security-orchestrator
├── vulnerability-scanner
├── dependency-checker
├── secrets-scanner
└── compliance-validator
```

## Advanced Patterns

### 1. Recursive Agent Networks

Agents that spawn other agents dynamically based on discovered complexity.

### 2. Consensus Mechanisms

Multiple agents vote on solutions, with majority or weighted voting.

### 3. Agent Specialization Trees

Hierarchical specialization from general to specific domains.

### 4. Adaptive Orchestration

Dynamic adjustment of agent allocation based on task complexity.

### 5. Cross-Project Agent Sharing

Centralized agent repositories for organization-wide reuse.

## Troubleshooting

### Common Issues

1. **Agent Not Found**
   - Check file location and naming
   - Verify YAML frontmatter syntax
   - Ensure proper file extension (.md)

2. **Tool Access Denied**
   - Verify tool names in configuration
   - Check MCP server connectivity
   - Confirm tool permissions

3. **Context Overflow**
   - Use more sub agents
   - Clear conversation history
   - Optimize prompts for brevity

4. **Parallel Execution Limits**
   - Maximum 10 concurrent agents
   - Use queuing for larger batches
   - Consider sequential for non-critical paths

## Future Considerations

As Claude Code Sub Agents continue to evolve in 2025, key areas of development include:

1. **Enhanced Agent Communication**: Direct agent-to-agent messaging protocols
2. **Dynamic Agent Generation**: Agents that create and modify other agents on-the-fly
3. **Improved Orchestration**: More sophisticated coordination patterns
4. **Cross-Platform Integration**: Agents working across different development environments
5. **Learning and Adaptation**: Agents that improve based on usage patterns

## Conclusion

Claude Code Sub Agents represent a paradigm shift in AI-assisted development. By understanding and applying these patterns, developers can create sophisticated multi-agent systems that dramatically improve productivity, code quality, and development velocity. The key to success lies in thoughtful agent design, appropriate orchestration patterns, and continuous optimization based on specific use cases.

---

_Last Updated: August 2025_
_Version: 1.0_
_Based on Claude Code v1.0.64+_
