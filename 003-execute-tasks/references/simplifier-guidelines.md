# Code Simplifier Guidelines

After a subagent completes a task, the main session applies these simplification principles to the modified files.

---

## Core Principles

### 1. Preserve Functionality

**Never change what the code does — only how it does it.**

- All original features, outputs, and behaviors must remain intact
- Test the code after simplification to verify nothing broke
- When in doubt, don't simplify — preserve the working code

### 2. Apply Project Standards

Draw coding standards from the project's context modules:

- **`.claude/ARCHITECTURE.md`** — Tech stack, file structure, patterns to follow
- **`.claude/DECISIONS.md`** — Architectural choices already made
- **`.claude/CONTEXT.md`** — Current project state and conventions

Look for:
- Import sorting and module style
- Function declaration style (function vs arrow)
- Type annotation patterns
- Component patterns (React, etc.)
- Error handling patterns
- Naming conventions

If context modules don't specify, apply sensible defaults for the language/framework.

### 3. Enhance Clarity

Simplify code structure by:

| Do | Don't |
|----|-------|
| Reduce unnecessary nesting | Over-flatten to the point of confusion |
| Eliminate redundant code | Remove helpful abstractions |
| Improve variable/function names | Rename things that are already clear |
| Consolidate related logic | Combine unrelated concerns |
| Remove obvious comments | Remove helpful documentation |

**Critical rules:**
- **Avoid nested ternary operators** — prefer switch statements or if/else chains
- **Choose clarity over brevity** — explicit code > clever one-liners
- Three similar lines is often better than a premature abstraction

### 4. Maintain Balance

Avoid over-simplification that could:

- Reduce code clarity or maintainability
- Create overly clever solutions that are hard to understand
- Combine too many concerns into single functions
- Remove helpful abstractions that improve organization
- Make the code harder to debug or extend

**The goal is readable, maintainable code — not the fewest lines.**

---

## What to Simplify

Focus on files listed in the completion signal's `files_created` and `files_modified`:

```yaml
files_created:
  - src/models/User.ts
  - src/api/userRoutes.ts

files_modified:
  - prisma/schema.prisma
```

Read each file and apply the principles above.

---

## What NOT to Do

- Don't touch files not listed in the completion signal
- Don't refactor unrelated code you happen to notice
- Don't add features or "improvements" beyond simplification
- Don't change public APIs or interfaces
- Don't optimize for performance (that's a separate concern)

---

## Simplification Checklist

For each file in scope:

- [ ] **Nesting** — Can any deeply nested code be flattened?
- [ ] **Duplication** — Is there repeated code that should be extracted?
- [ ] **Naming** — Are variable/function names clear and descriptive?
- [ ] **Comments** — Are there obvious comments that can be removed?
- [ ] **Ternaries** — Are there nested ternaries that should be if/else?
- [ ] **Complexity** — Is there unnecessary complexity that can be simplified?
- [ ] **Standards** — Does the code follow project conventions?

---

## Example Simplifications

### Before: Nested Ternaries
```typescript
const status = isLoading ? 'loading' : hasError ? 'error' : data ? 'success' : 'idle';
```

### After: Clear Switch
```typescript
function getStatus() {
  if (isLoading) return 'loading';
  if (hasError) return 'error';
  if (data) return 'success';
  return 'idle';
}
const status = getStatus();
```

---

### Before: Overly Compact
```typescript
const filtered = items.filter(x => x.active && x.type === 'user').map(x => ({ ...x, processed: true })).slice(0, 10);
```

### After: Readable Chain
```typescript
const filtered = items
  .filter(item => item.active && item.type === 'user')
  .map(item => ({ ...item, processed: true }))
  .slice(0, 10);
```

---

### Before: Redundant Abstraction
```typescript
function processItem(item: Item): ProcessedItem {
  return processItemInternal(item);
}

function processItemInternal(item: Item): ProcessedItem {
  return { ...item, processed: true };
}
```

### After: Direct Implementation
```typescript
function processItem(item: Item): ProcessedItem {
  return { ...item, processed: true };
}
```
