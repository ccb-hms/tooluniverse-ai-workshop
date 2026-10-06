# Building AI Co-Scientists with ToolUniverse

Slides and worked examples from a hands-on workshop in the Core for Computational
Biomedicine (CCB) AI Seminar & Workshop Series at Harvard Medical School, taught by members of the Zitnik Lab who build
[ToolUniverse](https://github.com/mims-harvard/ToolUniverse).

[ToolUniverse](https://aiscientist.tools) is an open platform that gives any AI model more
than 2,700 scientific tools and 130 research skills, from Open Targets, ChEMBL, UniProt,
openFDA, ClinicalTrials.gov and PubMed to models such as Boltz-2 and ADMET-AI. Every tool
declares its purpose, a typed input and output schema, and a standard way to call it, so
no model is retrained. The workshop installs it, connects it to an AI assistant, and works
through three real problems in genetics, biology and clinical therapeutics, auditing each
trace.

## What's here

| Folder | Contents |
|---|---|
| [`slides/`](slides/) | The workshop deck, as PowerPoint and PDF |
| [`applications/`](applications/README.md) | The three worked examples, one page each: the question, what every term in it means, and the run turn by turn, with each tool call, what it returned, and the reasoning between them |

## Quickstart

You need a laptop and an AI assistant that can run commands on it: Claude Desktop, Claude
Code, the ChatGPT app or Codex CLI. Python is not required; the installer brings its own.

1. Paste this into your assistant. It takes about ten minutes, mostly downloading.

   ```text
   Read https://aiscientist.tools/setup.md and set up ToolUniverse for me.
   ```

2. Check that it is connected:

   ```text
   Using ToolUniverse, tell me how many tools are loaded and name five tool categories. Then run PubMed_search_articles with query "CRISPR" and max_results 1, and show me the PMID.
   ```

   You should see a call to `find_tools` or `list_tools`, then `execute_tool`, then a real
   PMID and title. The first call after install takes 30 to 60 seconds while packages load.

<details>
<summary>Set it up from a terminal instead</summary>

```bash
# Install uv, the one prerequisite (Windows: astral.sh/uv/install.ps1)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Register ToolUniverse with Claude Code
claude mcp add -s user tooluniverse -e PYTHONIOENCODING=utf-8 -- uvx tooluniverse

# Or with Codex CLI and the Codex app, which share one config
codex mcp add tooluniverse --env PYTHONIOENCODING=utf-8 -- uvx tooluniverse

# Check it with no assistant involved
tu status && tu run PubMed_search_articles '{"query": "CRISPR", "max_results": 1}'
```

Claude Desktop needs no terminal: Settings → Extensions → Browse → ToolUniverse → Install.
Every other client is covered in the
[ToolUniverse guide](https://zitniklab.hms.harvard.edu/ToolUniverse/guide/building_ai_scientists/).

</details>

<details>
<summary>If something goes wrong</summary>

| Symptom | Likely cause | Fix |
|---|---|---|
| `uvx: command not found` | `uv` installed, but the terminal was not reopened | Reopen it. In a desktop app's config, use the absolute path to `uvx`; GUI apps do not see your shell's PATH. |
| The app shows no tools | It was closed, not quit | Quit with Cmd+Q (macOS) or from the tray (Windows), then relaunch |
| The first call hangs | It is still downloading | Wait a minute. On slow Wi-Fi, warm the cache once: `uvx tooluniverse --help` |
| `externally-managed-environment` | System `pip` was used | `uv pip install tooluniverse` |

Or paste the error into the chat that did the install and say "fix it."
`tooluniverse-doctor` prints what is missing and why.

</details>

## The three applications

| Field | Question | Tool calls, in order |
|---|---|---|
| [Genetics](applications/genetics/README.md) | Which gene does a non-coding variant control, and in which tissue? | `dbsnp_get_variant_by_rsid`, `GTEx_get_single_tissue_eqtls`, `UCSC_get_tf_binding_clusters` |
| [Biology](applications/biology/README.md) | What changes after a TP53 knockout, and in which direction? | `OmniPath_get_dorothea_regulon`, `STRING_get_interaction_partners` |
| [Clinical](applications/clinical/README.md) | Apixaban or warfarin at an eGFR of 22, and does the evidence cover this patient? | `PubMed_search_articles` twice, `PubMed_get_article_metadata`, `PubMed_search_articles` |

Every call was run against live databases on October 5, 2026; databases change, so a rerun
can return different numbers. All examples use public data, and the clinical case is a
hypothetical patient. Do not send PHI, PII or restricted clinical data to tools that call
external services, or to any external model.

## Credits

- **ToolUniverse** is built by the [Zitnik Lab](https://zitniklab.hms.harvard.edu/),
  Department of Biomedical Informatics, Harvard Medical School, led by Marinka Zitnik, with
  Shanghua Gao as lead creator. Code:
  [mims-harvard/ToolUniverse](https://github.com/mims-harvard/ToolUniverse).
- **Instructors:** Reza Shamji (Associate in Biomedical Informatics), Yepeng Huang (PhD
  Student, Biological and Biomedical Sciences) and Xiaorui Su (Postdoctoral Fellow in
  Biomedical Informatics), all of the Zitnik Lab.
- **Organizer:** Grey Kuling, Curriculum Fellow, Core for Computational Biomedicine,
  Department of Biomedical Informatics, Harvard Medical School.

## Citation

If you use ToolUniverse in your work, please cite the paper in *Nature Methods*:

> Gao, S., Zhu, R., Sui, P., Kong, Z., Aldogom, S., Huang, Y., Noori, A., Shamji, R.,
> Parvataneni, K., Tsiligkaridis, T., & Zitnik, M. (in press). Democratizing AI scientists
> using ToolUniverse. *Nature Methods*.

```bibtex
@article{gao2025democratizingaiscientistsusing,
  title   = {Democratizing AI scientists using ToolUniverse},
  author  = {Shanghua Gao and Richard Zhu and Pengwei Sui and Zhenglun Kong and Sufian Aldogom and Yepeng Huang and Ayush Noori and Reza Shamji and Krishna Parvataneni and Theodoros Tsiligkaridis and Marinka Zitnik},
  journal = {Nature Methods},
  year    = {in press},
}
```

Until it is published, the preprint is
[arXiv:2509.23426](https://arxiv.org/abs/2509.23426).

Questions: ccb_help@hms.harvard.edu
