# Qoder Skills for Go Development

A collection of Qoder-compatible skills for building production-ready Go applications. These skills provide domain-specific expertise for the Qoder AI assistant, covering language features, testing, security, observability, performance, and more.

## What are Qoder Skills

Skills are reusable instruction sets that extend Qoder with specialized knowledge. They are loaded on-demand when you ask about relevant topics, so they don't bloat your context window. Each skill is a directory containing a `SKILL.md` file with instructions, examples, and optional reference materials.

## Installation

### Option 1: Clone to Qoder Skills Directory

```bash
# macOS/Linux
mkdir -p ~/.qoder/skills/
git clone https://github.com/valeriypushkar/qoder-skills-golang.git ~/.qoder/skills/golang-skills

# Copy individual skills
cp -r ~/.qoder/skills/golang-skills/skills/golang-* ~/.qoder/skills/
```

### Option 2: Copy to Project Workspace

For project-specific skills, copy to your workspace:

```bash
cp -r skills/golang-testing /path/to/your/project/.qoder/skills/
```

## Available Skills

### Core Language & Best Practices

| Skill | Description |
|-------|-------------|
| `golang-code-style` | Go code style, formatting and conventions |
| `golang-naming` | Go naming conventions — packages, constructors, structs, interfaces, constants, enums, errors, booleans, receivers |
| `golang-error-handling` | Idiomatic Go error handling — creation, wrapping, errors.Is/As, custom error types, panic/recover, structured logging |
| `golang-concurrency` | Go concurrency patterns — goroutines, channels, select, locks, sync primitives, errgroup, worker pools, pipelines |
| `golang-context` | Idiomatic context.Context usage — creation, propagation, cancellation, timeouts, deadlines, values, tracing |
| `golang-structs-interfaces` | Struct and interface design patterns — composition, embedding, type assertions, interface segregation |
| `golang-data-structures` | Go data structures — slices, maps, arrays, container packages, generics, pointers |

### Testing & Quality

| Skill | Description |
|-------|-------------|
| `golang-testing` | Production-ready Go tests — table-driven tests, testify, mocks, integration tests, fuzzing, coverage |
| `golang-benchmark` | Go benchmarking, profiling, and performance measurement with pprof, benchstat, and CI regression detection |
| `golang-stretchr-testify` | Comprehensive guide to stretchr/testify — assert, require, mock, and suite packages |
| `golang-safety` | Defensive Go coding — nil safety, numeric conversions, resource lifecycle, defer patterns |
| `golang-linter` | Linting best practices and golangci-lint configuration |

### Performance & Debugging

| Skill | Description |
|-------|-------------|
| `golang-performance` | Performance optimization patterns — allocation reduction, CPU efficiency, memory layout, GC tuning, pooling |
| `golang-troubleshooting` | Systematic troubleshooting — debugging methodology, Delve, race detection, GODEBUG tracing |
| `golang-modernize` | Modernize Go code to use latest language features, standard library improvements, and idiomatic patterns |

### Architecture & Design

| Skill | Description |
|-------|-------------|
| `golang-design-patterns` | Idiomatic Go design patterns — functional options, resource management, graceful shutdown, resilience |
| `golang-dependency-injection` | Dependency injection patterns — manual DI, google/wire, uber-go/fx |
| `golang-project-layout` | Go project layout and workspace organization |
| `golang-cli` | CLI application development with Cobra and Viper |

### Infrastructure & Operations

| Skill | Description |
|-------|-------------|
| `golang-database` | Database access patterns — SQL, sqlx, pgx, transactions, connection pooling, migrations |
| `golang-observability` | Production observability — structured logging with slog, Prometheus metrics, OpenTelemetry tracing, profiling |
| `golang-security` | Security best practices — injection prevention, cryptography, filesystem safety, secrets management |
| `golang-continuous-integration` | CI/CD pipeline configuration — GitHub Actions, testing, linting, security scanning, GoReleaser |
| `golang-dependency-management` | Dependency management — go.mod, versioning, vulnerability scanning, automated updates |
| `golang-grpc` | gRPC services and clients — protobuf organization, interceptors, TLS/mTLS, streaming RPCs |

### Documentation & Maintenance

| Skill | Description |
|-------|-------------|
| `golang-documentation` | Documentation guide — godoc comments, README, CHANGELOG, Go Playground, Example tests |
| `golang-stay-updated` | Resources to stay updated with Go news, communities, and learning materials |
| `golang-popular-libraries` | Recommendations for production-ready Go libraries and frameworks |

## Skill Structure

Each skill follows this structure:

```
skill-name/
├── SKILL.md              # Required - main instructions
├── references/           # Optional - detailed documentation
│   └── topic.md
├── assets/               # Optional - templates, examples, configs
│   ├── templates/
│   └── examples/
└── scripts/              # Optional - utility scripts
    └── helper.sh
```

### SKILL.md Format

```markdown
---
name: skill-name
description: What this skill does and when to use it. Use when...
---

# Skill Title

## Instructions
Step-by-step guidance for the agent.

## Examples
Concrete examples of using this skill.

## Additional Resources
- For details, see [reference.md](reference.md)
```

## How Skills Work

1. **Trigger Detection**: Qoder reads the `description` field to decide when to load a skill
2. **Lazy Loading**: Only the description is loaded initially; full content loads when triggered
3. **Reference Files**: Detailed content in `references/` is loaded on-demand via links
4. **Context Budget**: Keep SKILL.md under 500 lines; total skill under 10k tokens

## Usage Examples

Once installed, Qoder automatically uses skills when you ask:

- "Help me write a benchmark for this function" → loads `golang-benchmark`
- "Review this code for security issues" → loads `golang-security`
- "How should I structure this project?" → loads `golang-project-layout`
- "Set up CI for this Go project" → loads `golang-continuous-integration`

## Creating New Skills

1. Create a directory: `mkdir ~/.qoder/skills/my-skill`
2. Write `SKILL.md` with YAML frontmatter
3. Add optional reference files
4. Test by asking Qoder about the skill's topic

### Best Practices

- **Description**: Write in third person, include trigger terms, explain what AND when
- **Concise**: Challenge every paragraph — does the agent need this?
- **Progressive Disclosure**: Put essentials in SKILL.md, details in references
- **One-Level References**: Link directly from SKILL.md to reference files
- **Consistent Terminology**: Pick one term and stick with it

## Contributing

### Skill Size Guidelines

- **Description**: ~100 tokens — what and when to use
- **SKILL.md**: 1,000–2,500 tokens — essential instructions
- **Full skill**: Up to 10,000 tokens including references
- **Simultaneous load**: 2–4 skills typical, ~10k tokens total

### Quality Checklist

- [ ] Description is specific with trigger terms
- [ ] Written in third person
- [ ] SKILL.md under 500 lines
- [ ] Consistent terminology
- [ ] Examples are concrete
- [ ] File references are one level deep
- [ ] No time-sensitive information

## License

MIT License — see [LICENSE](./LICENSE)
