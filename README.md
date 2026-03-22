# @actalog/create-datetime-tag

Creates and pushes a git tag based on the current date and time (format: `YYYY-MM-DD.HH-mm-ss`).

## Features ✨

- **Precision:** Uses seconds to reduce tag collisions.
- **Idempotency:** Automatically skips tag creation and push if a tag with the same name already exists, preventing workflow failures.
- **Automated:** Configures the git user as `github-actions[bot]`.

## Usage 🚀

Create a workflow file (e.g., `.github/workflows/tag.yml`) with the following content:

```yaml
name: Generate Tag

on:
  push:
    branches:
      - main

permissions:
  contents: write # Required to push tags back to the repository

jobs:
  tag:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Create Datetime Tag
        id: create-tag
        uses: actalog/create-datetime-tag@v1

      - name: Output Tag
        run: echo "The tag created is ${{ steps.create-tag.outputs.tag }}"
```

## Outputs 📤

| Name  | Description                                        |
| :---  | :---                                               |
| `tag` | The created tag name (e.g., `2025-03-22.12-55-10`) |
