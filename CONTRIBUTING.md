# Contributing to RoleDrill Templates

## Template format

Copy `templates/_template.json` and fill in:

- **id**: kebab-case unique identifier
- **name**: clear, descriptive name
- **category**: tech / cloud / security / compliance / healthcare / sales
- **purpose**: simulation / ai-readiness / development / promotion / hiring
- **description**: the scenario description (this is what Claude uses to generate questions — be specific, 200-500 chars recommended)
- **targetAudience**: who this is for
- **tags**: searchable keywords
- **author**: your name + github handle

## Quality bar

Your template must generate specific, scenario-based questions — not generic trivia.

❌ Bad description:
"Test knowledge of Java 17"

✅ Good description:
"Assess whether backend developers can identify breaking changes when migrating from Java 8 to Java 17 — including sealed classes, record types, removal of deprecated APIs, and module system implications for existing Maven projects."

## Validation

Every PR triggers a GitHub Action that:
1. Validates JSON schema
2. Calls Claude to generate 5 sample questions
3. Scores specificity and relevance
4. Posts results as a PR comment

Score ≥ 70 → ✅ Passes validation
Score < 70 → ⚠️ Feedback provided — please refine

## PR checklist

- [ ] Template follows the schema in `templates/_template.json`
- [ ] Description is specific (200+ chars)
- [ ] Tags are relevant and lowercase
- [ ] Author fields filled in
- [ ] Added to `index.json`
