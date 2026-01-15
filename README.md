# gendoc

Generate PDF from ODT templates with YAML variable substitution.

## Requirements

- Python 3
- PyYAML (`pip install pyyaml`)
- LibreOffice (`sudo apt install libreoffice`)

## Usage

```bash
./gendoc              # Process all matching .odt + .yaml pairs
./gendoc invoice      # Process invoice.odt + invoice.yaml → invoice.pdf
```

## Files

For each document, create matching files:

```
invoice.odt     # Template with {{placeholders}}
invoice.yaml    # Variable values
→ invoice.pdf   # Generated output
```

## YAML Format

```yaml
template: invoice     # Optional: use a different ODT template
extends: defaults.yaml  # Optional: inherit from another file

title: Welcome Document
recipient: Alice Johnson
date: January 14, 2026
company-url: https://example.com  # Variables ending in -url become hyperlinks

notes: |    # Multi-line values
  Line 1
  Line 2
```

## Multiple PDFs from One Template

Use `template:` to generate multiple PDFs from the same ODT:

```
invoice.odt              # Template
invoice-jan.yaml         # template: invoice
invoice-feb.yaml         # template: invoice
→ invoice-jan.pdf
→ invoice-feb.pdf
```

## Configuration

Create `.gendoc.yaml` in your project directory:

```yaml
output_dir: ~/Documents/output    # Where to save generated PDFs
exclude:                          # YAML files to skip in auto-discovery
  - defaults.yaml
  - example.yaml
```

| Option | Description |
|--------|-------------|
| `output_dir` | Directory for generated PDFs (supports `~`) |
| `exclude` | List of YAML files to ignore when running `./gendoc` |

## Template Placeholders

In your ODT file, use `{{variable-name}}` placeholders:

```
{{title}}

Dear {{recipient}},

Date: {{date}}
Website: {{company-url}}
```
