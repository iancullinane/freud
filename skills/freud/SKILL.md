---
name: freud
description: "Deep technical analysis of code with comprehensive documentation including architecture diagrams, database schemas, sequence flows, and critical reviews."
---

# Freud
Deep technical analysis of services with code documentation including architecture diagrams, database schemas, sequence flows, and critical reviews.

## Triggers
- "analyze this service"
- "analyze service"
- "create service documentation"
- "document this codebase"
- "service deep dive"

## Instructions

When asked to analyze a service, create comprehensive technical documentation with visual diagrams and critical reviews.

The result is a `.html` named `ANALYSIS.html`. If this file already exists read it first. 

Start from `assets/template.html` — copy it to `ANALYSIS.html` and fill in each section per the Analysis Process below, following the HTML comments in the template for what varies per repeating block.

**Page Styling**
- Use a "Gruvbox" style theme

### Analysis Process

1. **Discovery Phase**
   - Explore directory structure
   - Read README, go.mod/package.json, Dockerfile
   - Read `vendor/github.turbine.com/MGP-Server/bos-protos/`
     - This is the imported API monorepo
   - Start from `main.go`
   - Map configuration files and environment variables
   - List dependencies and external services

2. **Architecture Analysis**
   - Document service purpose and key features
   - Identify architectural patterns
   - Map HTTP endpoints and handlers
   - Analyze middleware and request flow
   - Document concurrency patterns
   - Review error handling strategy

3. **Database Deep Dive**
   - Read all migration files in db/, migrations/, or similar
   - Extract complete table DDL
   - Document columns with types and constraints
   - Create visual HTML tables with constraint badges (PK, FK, UNIQUE, NOT NULL)
   - Generate entity relationship diagram
   - Document stored procedures with business logic
   - Identify indexes and performance concerns

4. **Flow Visualization**
   - Create 3-6 focused sequence diagrams (one per domain)
   - Build state machines for stateful entities (jobs, orders, workflows)
   - Design decision trees for complex conditional logic
   - **CRITICAL**: Never use HTML tags in Mermaid diagrams
   - Keep each sequence diagram to 6-8 participants max

4a. **Linking to code**
   - When making diagrams where possible link to the code
   - Check the local .git config file for the remote location
   - If github build a link and use it in the diagram

5. **Code Review**
   - Document architectural strengths
   - Identify concerns and code smells
   - Provide specific, actionable recommendations
   - Assess operational risk level (Low/Medium/High)
   - Review test coverage

### Output Format

Generate a single self-contained HTML file: `ANALYSIS.html`

Structure:
```
1. Header with service name and description
2. API & Endpoints Section
3. Architecture & Dependencies Section
4. Flow Diagrams Section
   - Multiple focused sequence diagrams
   - State machines
   - Decision trees
5. Database Schema Section
   - Visual table represent
   ations
   - Entity relationship diagram
   - Stored procedure documentation
6. Technical Review Section
   - Strengths (green box)
   - Concerns (yellow box)
   - Recommendations (blue box)
   - Risk assessment
```

### Visual Design Requirements

**Components:**
- Professional gradient header
- Card-based layouts with hover effects
- Syntax-highlighted code blocks
- Database tables with visual badges
- Info/warning/success boxes with left border
- Responsive CSS for mobile

**Mermaid Diagrams:**
See `assets/template.html` for the exact Mermaid CDN script tag and `initialize()` config — copy it as-is.

### Database Table Template

See `assets/template.html` for the exact markup — copy the `.db-table-container` block as-is, one per table.

### Sequence Diagram Best Practices

**DO:**
- Break into multiple focused diagrams (Build Flow, Deploy Flow, Monitor Flow)
- Use clear, concise labels without HTML
- Show error paths with `alt` blocks
- Keep to 6-8 participants per diagram

**DON'T:**
- Use `<br/>` or any HTML tags in Mermaid
- Create mega-diagrams with 15+ participants
- Skip error handling flows

**Good Example:**
```mermaid
sequenceDiagram
    participant API as API Server
    participant DB as Database
    API->>DB: Query data
    DB-->>API: Return results
```

**Bad Example (DO NOT DO):**
```mermaid
sequenceDiagram
    API->>DB: Query<br/>with params  ❌ NO HTML
```

### Technical Review Framework

**Strengths to Highlight:**
- Clear separation of concerns
- Interface-based design
- Comprehensive error handling
- Good observability (logging, metrics, tracing)
- Graceful degradation patterns
- Circuit breakers and retries
- Distributed locking (if applicable)

**Concerns to Flag:**
- Missing error handling
- Potential race conditions
- Resource leaks (goroutines, connections)
- Missing timeouts or retries
- Single points of failure
- Unbounded operations
- Magic numbers
- Missing tests

**Risk Assessment Criteria:**
- **Low**: Well-tested, handles errors, no obvious issues
- **Medium**: Some concerns but core logic is sound
- **High**: Critical issues, potential data loss, production incidents likely

### Quality Checklist

Before finalizing, ensure:
- [ ] All Mermaid diagrams render without syntax errors
- [ ] Database tables are visual HTML tables (not text)

- [ ] Multiple focused sequence diagrams (not one mega-diagram)
- [ ] State machines for stateful entities
- [ ] Decision trees for complex logic
- [ ] Technical review has both strengths AND concerns
- [ ] Recommendations are specific and actionable
- [ ] Risk level clearly stated
- [ ] Code examples have syntax highlighting

if `./db` exists
- [ ] ERD shows all table relationships

- [ ] All sections complete

## Example Usage

**User Input:**
```
Analyze this service
```

**Expected Behavior:**
1. Explore codebase systematically
2. Read key files (main.go, migrations, config, etc.)
3. Create comprehensive HTML documentation
4. Save as cd-service-analysis.html
5. Report: "Analysis complete. Key findings: [summary]"

## Tips for Success

- Start with README and main entry point
- For Go services, look for main.go and server setup
- Database migrations are usually in db/, migrations/, or schema/
- Look for .drone.yml, .github/workflows, or Dockerfile for deployment
- Check go.mod, package.json, or requirements.txt for dependencies
- State machines are common for: jobs, orders, workflows, state machines
- Always provide specific line numbers or file references in reviews
