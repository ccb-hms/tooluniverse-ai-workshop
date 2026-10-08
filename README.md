# Building AI Co-Scientists with ToolUniverse

Slides and worked examples from the October 8, 2026 workshop in the Core for Computational
Biomedicine (CCB) AI Seminar & Workshop Series at Harvard Medical School, taught by members
of the Zitnik Lab, who build [ToolUniverse](https://github.com/mims-harvard/ToolUniverse).

[ToolUniverse](https://aiscientist.tools) is an open platform that gives any AI model more
than 2,700 scientific tools and 180 research skills, from Open Targets, ChEMBL, UniProt,
openFDA, ClinicalTrials.gov and PubMed to models such as Boltz-2 and ADMET-AI. Every tool
declares its purpose, a typed input and output schema, and a standard way to call it, so
no model is retrained. The workshop installs it, connects it to an AI assistant, and works
through two real problems, one clinical and one in genetics, auditing each trace.

## What's here

| File | Contents |
|---|---|
| [`slides/01-ccb-intro.pdf`](slides/01-ccb-intro.pdf) | CCB introduction and the AI Seminar & Workshop Series schedule |
| [`slides/02-tooluniverse-workshop.pdf`](slides/02-tooluniverse-workshop.pdf) | The workshop deck: why tools, installing ToolUniverse, how it works, and both examples turn by turn, with every tool call and what it returned |
| [`follow-along.md`](follow-along.md) | The two example queries, ready to paste into your own assistant |

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

3. Try the two worked examples yourself: [follow-along.md](follow-along.md).

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

## The two examples

| Field | Question | Tool calls, in order |
|---|---|---|
| [Clinical](follow-along.md#1-clinical-does-the-evidence-cover-this-patient) | Apixaban or warfarin at an eGFR of 22, and does the evidence cover this patient? | `PubMed_search_articles` twice, `PubMed_get_article_metadata`, `PubMed_search_articles` |
| [Genetics](follow-along.md#2-genetics-which-gene-does-this-variant-control) | Which gene does a non-coding variant control, and in which tissue? | `dbsnp_get_variant_by_rsid`, `GTEx_get_single_tissue_eqtls`, `UCSC_get_tf_binding_clusters`, `PubMed_search_articles` |

Every call was run against live databases on October 5, 2026; databases change, so a rerun
can return different numbers. The full runs, turn by turn, are in the
[workshop deck](slides/02-tooluniverse-workshop.pdf). All examples use public data, and the
clinical case is a hypothetical patient. Do not send PHI, PII or restricted clinical data to
tools that call external services, or to any external model.

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
