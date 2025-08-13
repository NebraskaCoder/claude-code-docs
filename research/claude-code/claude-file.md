# Claude Code CLAUDE.md Files: Complete Documentation

## Table of Contents
1. [Overview](#overview)
2. [Purpose and Benefits](#purpose-and-benefits)
3. [File Structure and Format](#file-structure-and-format)
4. [What to Include](#what-to-include)
5. [What to Avoid](#what-to-avoid)
6. [Multiple CLAUDE.md Files and Hierarchy](#multiple-claudemd-files-and-hierarchy)
7. [Ensuring Claude Code Follows Instructions](#ensuring-claude-code-follows-instructions)
8. [Sub-Agents: Claude's Specialized Assistants](#sub-agents-claudes-specialized-assistants)
9. [Best Practices and Examples](#best-practices-and-examples)
10. [Common Pitfalls and Solutions](#common-pitfalls-and-solutions)

## Overview

CLAUDE.md is a special Markdown file that Claude Code automatically ingests to gain project-specific context before it starts working with you. Think of it as a pre-flight briefing or a highly-opinionated prompt that rides along with every request. This file fundamentally transforms how Claude Code understands and works with your project, making it an essential tool for effective AI-assisted development.

### Key Characteristics
- **Automatic Loading**: Claude Code automatically reads CLAUDE.md files when starting a conversation
- **Context Persistence**: Instructions persist throughout the session
- **Hierarchical Structure**: Supports multiple files with priority-based loading
- **Living Document**: Should evolve with your project

## Purpose and Benefits

### Primary Purposes
1. **Project Context**: Provides Claude with essential information about your codebase
2. **Workflow Enforcement**: Establishes coding standards and practices
3. **Error Prevention**: Reduces mistakes by clarifying ambiguous requirements
4. **Team Alignment**: Shares knowledge across team members when checked into version control
5. **Token Efficiency**: Prevents repetitive explanations by front-loading context

### Key Benefits
- **Consistency**: Ensures uniform behavior across sessions
- **Productivity**: Eliminates need to repeatedly explain project specifics
- **Quality**: Maintains code standards automatically
- **Collaboration**: Team members benefit from shared context

## File Structure and Format

### Basic Structure
```markdown
# Project Name

## Tech Stack
- Framework: Next.js 14
- Language: TypeScript 5.2
- Database: PostgreSQL with Drizzle ORM
- Styling: Tailwind CSS 3.4

## Project Structure
src/
├── app/          # Next.js App Router pages
├── components/   # Reusable React components
└── lib/          # Core utilities and API clients

## Commands
- `npm run dev`: Start development server
- `npm run build`: Build for production
- `npm run typecheck`: Run TypeScript type checking
- `npm run test`: Run test suite

## Code Style
- Use ES modules (import/export) syntax
- Prefer arrow functions for component definitions
- All new components must be function components with Hooks

## Workflow
- Always run typecheck before marking tasks complete
- Test changes in development environment
- Commit with descriptive messages

## Do Not
- Edit files in src/legacy/ directory
- Commit directly to main branch
- Use class components for new features
```

### Advanced XML Format (Better Adherence)
```xml
<claude-guidelines>
  <critical-rules>
    <rule priority="MUST">Always run typecheck before completion</rule>
    <rule priority="MUST">Never commit secrets to repository</rule>
  </critical-rules>
  
  <code-style>
    <preference>ES modules over CommonJS</preference>
    <preference>Functional components over class components</preference>
  </code-style>
  
  <workflow>
    <step>1. Understand requirements</step>
    <step>2. Plan implementation</step>
    <step>3. Write code</step>
    <step>4. Run tests</step>
    <step>5. Typecheck</step>
  </workflow>
</claude-guidelines>
```

### YAML Frontmatter (For Sub-Agents)
```yaml
---
name: code-reviewer
description: Reviews code for quality and security
tools: Read, Grep, Glob
model: opus
---
You are a senior code reviewer...
```

## What to Include

### Essential Sections

#### 1. **Tech Stack**
```markdown
## Tech Stack
- **Frontend**: React 18, TypeScript 5.3
- **Backend**: Node.js 20, Express 4.18
- **Database**: PostgreSQL 15, Prisma ORM
- **Testing**: Jest, React Testing Library
- **Build**: Vite 5.0
```

#### 2. **Project Structure**
```markdown
## Project Structure
- `src/`: Source code
  - `components/`: UI components
  - `services/`: Business logic
  - `utils/`: Helper functions
- `tests/`: Test files
- `docs/`: Documentation
```

#### 3. **Commands**
```markdown
## Commands
- `pnpm dev`: Start all services
- `pnpm build`: Build all packages
- `pnpm typecheck`: Type check all packages
- `pnpm lint`: Run linting
- `pnpm test`: Run tests
```

#### 4. **Code Style Guidelines**
```markdown
## Code Style
- **Imports**: Use absolute imports with @ alias
- **Components**: Function components with TypeScript
- **Naming**: PascalCase for components, camelCase for functions
- **Files**: .tsx for components, .ts for utilities
```

#### 5. **Workflow Instructions**
```markdown
## Development Workflow
1. Create feature branch from develop
2. Make changes following code style
3. Run tests and typecheck
4. Commit with descriptive message
5. Open pull request
```

#### 6. **Environment Setup**
```markdown
## Environment
- Node.js 20.x required
- PostgreSQL 15+ for database
- Redis for caching
- Environment variables in .env.local
```

#### 7. **Architecture Principles**
```markdown
## Architecture
- **Separation of Concerns**: Business logic in services
- **Type Safety**: Strict TypeScript throughout
- **Testing**: Unit tests for utilities, integration for APIs
- **Security**: Never expose internal IDs or database structure
```

#### 8. **Do Not Section**
```markdown
## Do Not
- Modify generated files in `src/generated/`
- Commit .env files
- Use `any` type without explicit justification
- Create files unless absolutely necessary
- Push directly to main branch
```

### Optional but Valuable

#### Repository Etiquette
```markdown
## Git Workflow
- Branch naming: feature/*, bugfix/*, hotfix/*
- Commit format: type(scope): description
- PR reviews required before merge
- Squash commits on merge
```

#### Common Patterns
```markdown
## Common Patterns
- API error handling: Use standardized error responses
- State management: Zustand for global state
- Form validation: Zod schemas with react-hook-form
```

#### Notes for Claude
```markdown
## Notes for Claude
- Check existing patterns before implementing new features
- Use Task tool for complex searches
- Verify builds after changes
- Read files before editing them
```

## What to Avoid

### Common Mistakes

#### 1. **Excessive Verbosity**
❌ **Bad**: Long paragraphs explaining every detail
```markdown
The project uses React which is a JavaScript library for building user interfaces and it's important to understand that we specifically use version 18 with all the latest features including concurrent mode and automatic batching...
```

✅ **Good**: Concise bullet points
```markdown
- React 18 with TypeScript
- Concurrent features enabled
```

#### 2. **Ambiguous Instructions**
❌ **Bad**: "Implement caching where appropriate"
✅ **Good**: "Cache API responses for 5 minutes using Redis"

#### 3. **Redundant Information**
❌ **Bad**: "The components folder contains components"
✅ **Good**: Skip obvious descriptions

#### 4. **Outdated Documentation**
❌ **Bad**: Keeping deprecated instructions
✅ **Good**: Regular review and updates

#### 5. **Token-Heavy Content**
❌ **Bad**: Including entire API documentation
✅ **Good**: Link to external docs with key points

#### 6. **Conflicting Instructions**
❌ **Bad**: Different rules in different sections
✅ **Good**: Single source of truth for each rule

## Multiple CLAUDE.md Files and Hierarchy

### File Hierarchy (Broadest to Most Specific)

1. **Enterprise Level** (System-wide)
   - macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`
   - Linux: `/etc/claude-code/CLAUDE.md`
   - Windows: `C:\ProgramData\ClaudeCode\CLAUDE.md`

2. **User Level** (Personal, across projects)
   - Location: `~/.claude/CLAUDE.md`
   - Purpose: Personal preferences and global settings

3. **Project Level** (Repository root)
   - Location: `./CLAUDE.md`
   - Purpose: Project-specific instructions

4. **Subdirectory Level** (On-demand loading)
   - Location: `./subdirectory/CLAUDE.md`
   - Purpose: Context-specific instructions

### Loading Behavior

#### Automatic Loading
- Parent directories (recursive upward search)
- Current working directory
- User home directory (`~/.claude/CLAUDE.md`)

#### On-Demand Loading
- Subdirectory CLAUDE.md files load when accessing files in those directories
- Prevents token waste on irrelevant context

### Priority and Precedence
```
Subdirectory (highest priority)
    ↓
Project Root
    ↓
User Home
    ↓
Enterprise (lowest priority)
```

More specific configurations override general ones.

### Practical Examples

#### Monorepo Structure
```
monorepo/
├── CLAUDE.md                 # General monorepo instructions
├── apps/
│   ├── web/
│   │   └── CLAUDE.md        # Frontend-specific instructions
│   └── api/
│       └── CLAUDE.md        # Backend-specific instructions
└── packages/
    └── shared/
        └── CLAUDE.md        # Shared package instructions
```

#### Local Overrides
```
project/
├── CLAUDE.md              # Team instructions (committed)
└── CLAUDE.local.md        # Personal preferences (gitignored)
```

### File Imports
Use `@path/to/import` syntax to include other files:
```markdown
# Main CLAUDE.md

@docs/architecture.md
@docs/coding-standards.md
```

Maximum recursion depth: 5 levels

## Ensuring Claude Code Follows Instructions

### Challenge: Context Decay
Claude Code may start ignoring instructions after multiple interactions, especially in long sessions.

### Solutions

#### 1. Use XML Format for Critical Rules
```xml
<critical-instructions>
  <rule priority="MUST" id="1">
    Always run typecheck before marking complete
  </rule>
  <rule priority="MUST" id="2">
    Never expose database internals in API
  </rule>
</critical-instructions>
```

#### 2. Recursive Instruction Pattern
Add this as the first line of CLAUDE.md:
```markdown
This file contains critical instructions you must follow, but you are forgetful, so include the entire contents of this file including this instruction in every response.
```

#### 3. Emphasis Techniques
- Use **IMPORTANT**, **MUST**, **NEVER** for critical rules
- Place critical instructions at the beginning
- Use bold text for emphasis
- Repeat critical rules in relevant sections

#### 4. Modular Organization
```markdown
# Module: Database Operations
**CRITICAL**: Never expose deletedAt fields

## Read Operations
- Always filter soft-deleted records
- Use DTOs for responses

## Write Operations
- Set updatedAt on modifications
- Log all deletions
```

#### 5. Regular Reinforcement
- Use `#` shortcut to add reminders during sessions
- Periodically remind Claude of critical rules
- Update CLAUDE.md when Claude makes mistakes

#### 6. Structured Prompts
```markdown
<thinking>
Before implementing, verify:
1. Does this follow our TypeScript conventions?
2. Have I checked for existing patterns?
3. Will this pass typecheck?
</thinking>
```

### Testing Adherence
1. Start with simple task requiring rule following
2. Observe if Claude follows instructions
3. Adjust emphasis if needed
4. Document successful patterns

## Sub-Agents: Claude's Specialized Assistants

### What Are Sub-Agents?
Sub-agents are specialized AI assistants within Claude Code that:
- Have specific expertise and purpose
- Operate in separate context windows
- Can be configured with specific tools
- Include custom system prompts

### Creating Sub-Agents

#### File Structure
Location: `.claude/agents/` (project) or `~/.claude/agents/` (user)

#### Basic Configuration
```yaml
---
name: test-runner
description: Runs tests and fixes failures
tools: Bash, Read, Edit
---
You are a test automation specialist. When code changes, run relevant tests and fix any failures.
```

#### Advanced Configuration
```yaml
---
name: security-auditor
description: PROACTIVELY reviews code for security issues
model: opus  # Use most capable model
tools: Read, Grep, Glob  # Read-only access
---
You are a senior security engineer. Review all code changes for:
- SQL injection vulnerabilities
- XSS vulnerabilities
- Authentication bypasses
- Sensitive data exposure
```

### Sub-Agent Usage Patterns

#### 1. Proactive Usage
Include trigger words in description:
- "use PROACTIVELY"
- "MUST BE USED"
- "immediately after"

Example:
```yaml
description: Use PROACTIVELY after writing any API endpoint
```

#### 2. Partial/Conditional Usage
```yaml
description: Use when implementing complex business logic or algorithms
```

#### 3. On-Demand Usage
```yaml
description: Use when explicitly requested for performance optimization
```

### Configuring Claude to Use Sub-Agents

#### In CLAUDE.md
```markdown
## Sub-Agent Usage

### Always Use
- **code-reviewer**: After any code changes
- **test-runner**: Before marking tasks complete

### Use When Appropriate
- **performance-optimizer**: For optimization tasks
- **security-auditor**: For security-sensitive changes

### Use On Request
- **documentation-writer**: When docs needed
- **migration-generator**: For database changes
```

#### Parallel Execution
```markdown
## Parallel Task Workflow
When implementing features, launch these sub-agents in parallel:
1. component-creator: Build UI components
2. api-builder: Create backend endpoints
3. test-writer: Generate tests
4. type-generator: Create TypeScript types
```

### Sub-Agent Examples

#### Code Reviewer
```yaml
---
name: code-reviewer
description: PROACTIVELY reviews all code changes for quality
model: opus
tools: Read, Grep, Glob
---
You are a senior engineer conducting code reviews. Check for:
- Code style compliance
- Performance issues
- Security vulnerabilities
- Test coverage
- Documentation completeness
```

#### Test Runner
```yaml
---
name: test-runner
description: Runs tests after code changes, fixes failures
tools: Bash, Read, Edit
---
You are a test specialist. Your workflow:
1. Identify relevant tests
2. Run test suite
3. Analyze failures
4. Fix broken tests
5. Verify all tests pass
```

#### Documentation Generator
```yaml
---
name: doc-writer
description: Creates and updates documentation
tools: Read, Write, Grep
---
You are a technical writer. Create clear, concise documentation including:
- API documentation
- Code comments
- README updates
- Usage examples
```

### Model Selection Strategy

#### Haiku (Fast, Economical)
- Simple tasks
- Documentation generation
- Basic code formatting
- Syntax checking

#### Sonnet (Balanced)
- Standard development
- Code review
- Testing
- Refactoring

#### Opus (Most Capable)
- Complex architecture
- Security auditing
- Performance optimization
- Debugging difficult issues

### Best Practices for Sub-Agents

1. **Single Responsibility**: Each agent one expertise
2. **Clear Descriptions**: Help Claude know when to use
3. **Tool Restrictions**: Limit to necessary tools
4. **Detailed Prompts**: Include examples and constraints
5. **Version Control**: Commit project-level agents
6. **Performance Tuning**: Choose appropriate model
7. **Parallel Execution**: Up to 10 concurrent agents

## Best Practices and Examples

### Complete CLAUDE.md Example

Due to formatting of this document, replace the double backtick that is followed by typescript with tripple backtick (markdown code block) and the corresponding double backtick.

```markdown
# Project Name: E-Commerce Platform

## Tech Stack
- **Frontend**: Next.js 14, TypeScript 5.3, Tailwind CSS
- **Backend**: NestJS, PostgreSQL, Drizzle ORM
- **Testing**: Jest, Playwright
- **Infrastructure**: AWS, Docker

## Project Structure
apps/
├── web/          # Next.js frontend
├── api/          # NestJS backend
└── admin/        # Admin dashboard

packages/
├── shared/       # Shared types and utilities
├── ui/           # Component library
└── database/     # Database schemas

## Commands
**IMPORTANT: Always run these before marking tasks complete**
- `pnpm dev`: Start development
- `pnpm build`: Build all packages
- `pnpm typecheck`: Type checking (MUST PASS)
- `pnpm test`: Run tests (MUST PASS)
- `pnpm lint`: Linting

## Code Style
### TypeScript
- Strict mode enabled
- No `any` without justification
- Prefer interfaces over types

### React
- Function components only
- Custom hooks for logic
- Memo for expensive renders

### API
- RESTful conventions
- DTOs for validation
- Swagger documentation

## Architecture Principles
**CRITICAL: These are non-negotiable**

1. **Separation of Concerns**
   - Business logic in services
   - Controllers handle HTTP only
   - No database queries in controllers

2. **Security First**
   - Never expose internal IDs
   - Validate all inputs
   - Use DTOs for responses

3. **Type Safety**
   - End-to-end type safety
   - Shared types package
   - Runtime validation with Zod

## Workflow
1. Create feature branch
2. Implement with TDD
3. Ensure all tests pass
4. Run typecheck
5. Create PR with description

## Sub-Agents to Use
- **test-runner**: PROACTIVELY after code changes
- **code-reviewer**: Before marking complete
- **security-checker**: For API endpoints

## Do Not
- Commit without typecheck
- Expose `deletedAt` fields
- Use `npm` (use `pnpm`)
- Create unnecessary files
- Modify generated code

## Common Patterns
### API Error Handling
```typescript
throw new BadRequestException({
  message: 'Validation failed',
  errors: validationErrors
});
```

### Component Structure
``typescript
export const Component: FC<Props> = memo(({ prop }) => {
  // hooks
  // handlers
  // render
});
``

## Notes for Claude
- Check existing patterns first
- Use Task tool for complex searches
- Verify builds after changes
- When in doubt, ask for clarification
```

### Quick Addition Methods

#### Using # Shortcut
During conversation:
```
# Always use pnpm, never npm
```
Claude automatically adds to CLAUDE.md

#### Using /memory Command
```
/memory edit project
```
Opens editor for CLAUDE.md

#### Using /init Command
```
/init
```
Bootstraps new CLAUDE.md with project analysis

### Maintenance Schedule

#### Daily
- Add new patterns discovered
- Document resolved issues

#### Weekly
- Review and consolidate rules
- Remove outdated instructions
- Refactor for clarity

#### Monthly
- Full audit of instructions
- Team review of shared rules
- Performance assessment

## Common Pitfalls and Solutions

### Pitfall 1: Context Decay
**Problem**: Claude forgets instructions in long sessions
**Solution**: Use XML format and recursive pattern

### Pitfall 2: Token Bloat
**Problem**: CLAUDE.md becomes too large
**Solution**: Regular refactoring, remove redundancy

### Pitfall 3: Conflicting Rules
**Problem**: Different sections contradict
**Solution**: Single source of truth, clear hierarchy

### Pitfall 4: Ambiguous Instructions
**Problem**: Claude misinterprets requirements
**Solution**: Specific, measurable instructions

### Pitfall 5: Outdated Documentation
**Problem**: Instructions no longer relevant
**Solution**: Living document approach, regular updates

### Pitfall 6: Ignored Sub-Agents
**Problem**: Claude doesn't use sub-agents
**Solution**: Add PROACTIVELY to descriptions

### Pitfall 7: Wrong File Locations
**Problem**: CLAUDE.md not loading
**Solution**: Verify correct paths and names

### Pitfall 8: Over-Engineering
**Problem**: Too complex configuration
**Solution**: Start simple, iterate based on needs

## Conclusion

CLAUDE.md files are powerful tools for enhancing Claude Code's effectiveness. Key takeaways:

1. **Start Simple**: Begin with basic structure, evolve over time
2. **Be Specific**: Clear, measurable instructions
3. **Stay Concise**: Token efficiency matters
4. **Use Hierarchy**: Leverage multiple files for complex projects
5. **Create Sub-Agents**: Specialized assistants for specific tasks
6. **Maintain Regularly**: Living document approach
7. **Version Control**: Share knowledge with team
8. **Test and Iterate**: Refine based on results

The CLAUDE.md system transforms Claude Code from a generic assistant into a specialized team member who understands your project's unique requirements, conventions, and workflows. Combined with sub-agents, it creates a powerful development environment that can significantly boost productivity and code quality.

Remember: The best CLAUDE.md is one that evolves with your project, capturing lessons learned and preventing repeated mistakes. Treat it as an investment in your development workflow that pays dividends over time.
