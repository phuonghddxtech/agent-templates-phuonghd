---
description: Tìm và phân tích N+1 query problems trong codebase
---

## Steps

1. Scan controllers and services for missing eager loading
// turbo
```bash
grep -rn "->each\|foreach.*->load\|->map.*->" src/app/Http/Controllers/ src/app/Services/
```

2. Find relationships loaded inside loops
// turbo
```bash
grep -rn "\$.*->[a-z]*\b" src/app/Http/Controllers/ src/app/Services/ | grep -v "//\|function\|class"
```

3. Check existing with() usage
// turbo
```bash
grep -rn "->with(" src/app/Repositories/
```

4. Analyze findings
For each potential N+1 found:
- Identify the model and relationship
- Check if `with()` eager loading is missing
- Suggest the fix

5. Output report
```
## N+1 Query Analysis

### Issues Found
- [FILE:LINE] description — suggested fix: ->with('relation')

### Already Optimized
- list of files using proper eager loading

### Summary
X potential N+1 issues found
```
