# 📍 PROJECT CHECKPOINTS

## Purpose
Track stable versions of the project that can be used as rollback points.
Each checkpoint represents a fully working state with all tests passing.

## How to Create a Checkpoint

```bash
# 1. Ensure all tests pass
npm test

# 2. Commit all changes
git add .
git commit -m "feat: completed [feature name]"

# 3. Create checkpoint tag
git tag checkpoint-v[X.Y] -m "Checkpoint: [description]"

# 4. Push to remote
git push origin checkpoint-v[X.Y]

# 5. Update this file
```

---

## CHECKPOINT LOG

### CHECKPOINT v1.0 ([DATE])
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- 💾 Commit: [commit-hash]

### CHECKPOINT v1.1 ([DATE])
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- 💾 Commit: [commit-hash]

### CHECKPOINT v1.2 ([DATE])
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ⚠️ Known issue: [description of known issue]
- 💾 Commit: [commit-hash]

### CHECKPOINT v1.3 ([DATE])
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- 💾 Commit: [commit-hash]

### CHECKPOINT v2.0 ([DATE])
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- 💾 Commit: [commit-hash]

### CHECKPOINT v2.1 ([DATE])
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- ✅ [Feature/Component completed]
- 💾 Commit: [commit-hash]

---

## How to Rollback

### To specific checkpoint:
```bash
# View all checkpoints
git tag -l "checkpoint-*"

# Checkout specific checkpoint
git checkout checkpoint-v2.0

# Create new branch from checkpoint
git checkout -b fix-from-v2.0
```

### Emergency rollback:
```bash
# If current changes are broken
git stash
git checkout checkpoint-v[X.Y]
```

---

## Checkpoint Standards

### ✅ Requirements for new checkpoint:
- All tests must pass (unit, integration, e2e)
- No console errors or warnings
- Code review completed
- Documentation updated
- No known critical bugs

### 📋 Checkpoint Checklist:
```markdown
- [ ] npm test passes
- [ ] npm run lint passes
- [ ] npm run type-check passes
- [ ] Manual smoke test completed
- [ ] MASTER.md updated
- [ ] PROJECT_MAP.md current
- [ ] CODE_REGISTRY.md current
- [ ] No merge conflicts
- [ ] Performance acceptable
- [ ] Security review done
```

### ⚠️ When NOT to checkpoint:
- Work in progress features
- Failing tests
- Known security vulnerabilities
- Performance regressions
- Incomplete migrations

---

## Recovery Procedures

### From checkpoint after failed feature:
```bash
# 1. Stash or discard current changes
git stash

# 2. Return to last checkpoint
git checkout checkpoint-v2.1

# 3. Create new feature branch
git checkout -b feature-retry

# 4. Apply selective changes from stash if needed
git stash pop
git add -p  # selective staging
```

### From checkpoint after data corruption:
```bash
# 1. Backup current database
pg_dump myapp > backup_corrupted.sql

# 2. Checkout checkpoint
git checkout checkpoint-v2.0

# 3. Reset database to checkpoint migration
npm run db:reset
npm run db:migrate
npm run db:seed

# 4. Restore selective data if needed
```

---

## Metrics

- Total Checkpoints: [COUNT - update as you create checkpoints]
- Average Days Between Checkpoints: [NUMBER - calculate from your checkpoints]
- Rollbacks Performed: [COUNT - track when you rollback]
- Current Stability Score: [PERCENTAGE]% - [assess project stability]

---

## Notes

- Keep checkpoint messages descriptive
- Tag major feature completions
- Don't checkpoint experimental branches
- Archive old checkpoints after 6 months
- Document any special rollback procedures
