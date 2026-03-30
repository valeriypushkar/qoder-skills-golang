---
name: golang-error-handling
description: Idiomatic Go error handling — creation, wrapping with %w, errors.Is/As, errors.Join, custom error types, sentinel errors, panic/recover, the single handling rule, structured logging with slog, HTTP request logging middleware for production errors. Built to make logs usable at scale with log aggregation 3rd-party tools. Apply when creating, wrapping, inspecting, or logging errors in Go code.
---

# Go Error Handling Best Practices

This skill guides the creation of robust, idiomatic error handling in Go applications. Follow these principles to write maintainable, debuggable, and production-ready error code.

## Best Practices Summary

1. **Returned errors MUST always be checked** — NEVER discard with `_`
2. **Errors MUST be wrapped with context** using `fmt.Errorf("{context}: %w", err)`
3. **Error strings MUST be lowercase**, without trailing punctuation
4. **Use `%w` internally, `%v` at system boundaries** to control error chain exposure
5. **MUST use `errors.Is` and `errors.As`** instead of direct comparison or type assertion
6. **SHOULD use `errors.Join`** (Go 1.20+) to combine independent errors
7. **Errors MUST be either logged OR returned**, NEVER both (single handling rule)
8. **Use sentinel errors** for expected conditions, custom types for carrying data
9. **NEVER use `panic` for expected error conditions** — reserve for truly unrecoverable states
10. **SHOULD use `slog`** (Go 1.21+) for structured error logging — not `fmt.Println` or `log.Printf`
11. **Log HTTP requests** with structured middleware capturing method, path, status, and duration
12. **Use log levels** to indicate error severity
13. **Never expose technical errors to users** — translate internal errors to user-friendly messages, log technical details separately
14. **Keep error messages low-cardinality** — don't interpolate variable data (IDs, paths, line numbers) into error strings; attach them as structured attributes instead (via `slog` at the log site on the error itself) so APM/log aggregators (Datadog, Loki, Sentry) can group errors properly

## Detailed Reference

- **[Error Creation](./references/error-creation.md)** — How to create errors that tell the story: error messages should be lowercase, no punctuation, and describe what happened without prescribing action. Covers sentinel errors (one-time preallocation for performance), custom error types (for carrying rich context), and the decision table for which to use when.

- **[Error Wrapping and Inspection](./references/error-wrapping.md)** — Why `fmt.Errorf("{context}: %w", err)` beats `fmt.Errorf("{context}: %v", err)` (chains vs concatenation). How to inspect chains with `errors.Is`/`errors.As` for type-safe error handling, and `errors.Join` for combining independent errors.

- **[Error Handling Patterns and Logging](./references/error-handling.md)** — The single handling rule: errors are either logged OR returned, NEVER both (prevents duplicate logs cluttering aggregators). Panic/recover design and `slog` structured logging integration for APM tools.

## Cross-References

- → See `golang-observability` for structured logging setup, log levels, and request logging middleware
- → See `golang-safety` for nil interface trap and nil error comparison pitfalls
- → See `golang-naming` for error naming conventions (ErrNotFound, PathError)

## References

- [lmittmann/tint](https://github.com/lmittmann/tint)
- [log/slog package](https://pkg.go.dev/log/slog)
