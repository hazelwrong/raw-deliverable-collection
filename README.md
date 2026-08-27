# raw-deliverable-collection

Codex skill for collecting authentic, publicly accessible everyday-work deliverable attachments against a validated industry-and-occupation matrix.

This repository contains the skill instructions, inventory contract, bundled 33-task-type by 9-industry matrix, and the GDPval 44-occupation taxonomy sourced from the official OpenAI page. It does not contain collected source files, candidate inventories, or client data.

## Authoritative Sources

- [OpenAI GDPval: 9 industries and 44 occupations](https://openai.com/zh-Hans-CN/index/gdpval/)
- [Bundled task-industry matrix](references/cross_matrix_tasks.md)
- [Bundled GDPval occupation taxonomy](references/gdpval-occupation-taxonomy.md)

## Install

Clone the repository into the global Codex skills directory:

```bash
git clone https://github.com/hazelwrong/raw-deliverable-collection.git ~/.codex/skills/raw-deliverable-collection
```

Existing installations can be updated with:

```bash
git -C ~/.codex/skills/raw-deliverable-collection pull --ff-only
```
