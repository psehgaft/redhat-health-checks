| Variable | Default / example | Purpose |
|---|---|---|
| `KUBECONFIG` | — | Path to kubeconfig (live cluster collection) |
| `HC_COLLECT_OUT` | `output/hc_collect` | Collection results directory |
| `HC_REPORT_OUT` | `output/Health_Check_Report` | Final report output |
| `HC_SSH_HOST` | `user@host` | Remote support shell server |
| `HC_SSH_RESULTS` | `/home/remote/<username>/hc_results` | Results path on remote (set explicitly — `~` does not resolve reliably; use `/home/remote/<username>/hc_results.<cluster>` for a salvage tarball) |
| `HC_SSH_SCRIPTS` | `/home/remote/<username>/hc_supportshell` | Scripts path on remote (same `~` caveat — set explicitly) |
| `HC_MG_INPUT` | `/home/remote/<username>/<case-number>` | Must-gather/case path on remote for `hc-collect-remote` — always set explicitly, not `~/<case-number>` |
| `HC_FETCH_STAGE` | `output/hc_collect/<date>` | Dated staging dir for supportshell fetches (auto-computed) |
| `MERGE_INPUTS` | `"dir1 dir2 ..."` | Inputs for `hc-merge` |
| `HC_TSR_HTML` | — | Repo-relative path to a TSR HTML export (overrides auto-discovery) |
| `HC_TSR_HTML_DIR` | `output/tsr_html` | Directory for TSR HTML auto-discovery |
| `HC_CHECK_PROFILE` | `advisory` | Check expansion profile: `core` \| `extended` \| `advisory` |
| `HC_OMIT_CHECK_IDS` | — | Repo-relative path to a check-ID omit list (writes `{stem}_pruned.md`) |
| `HC_OMIT_STRICT` | `1` | Fail if an omit ID is not on a Chapter 6 finding |
| `HC_CCX_RULES_FILE` | `/path/to/ccx_rules.json` | Optional CCX runtime payload for collection |
| `HC_DOCS_ROOT` | — | Local OpenShift docs tree for `make hc-link-review` |
| `HC_LINK_REVIEW_OUT` | — | Output dir for `kb_link_review.md` / `.csv` |
| `ENGINE` | auto (`podman` when on `PATH`) | Container engine: `podman` or `docker` |
| `IMAGE` | `redhat-health-checks` | Container image name |
| `CLIENT` | — | Client name for `make setup` |
| `PROJECT` | `HC` | Engagement code (default) |
| `FORCE` | `1` | Replace files setup already created, or overwrite an `hc-html`/`hc-pdf` basename dest |
| `REPORT` | — | One markdown file for `hc-html`, `hc-pdf`, `hc-summary-conclusion`, `hc-update-loi`, `hc-renumber-findings` |
| `DRY_RUN` | `1` | Preview `hc-update-loi` or `hc-renumber-findings` |
| `HC_DRY_RUN` | `1` | Pass `--dry-run` on `hc-report` (placeholder executive summary) |
| `HC_SUMMARY_CONCLUSION` | `1` | Draft Chapter 3 and Chapter 8 after `hc-report` |
| `RESULTS_DIR` | — | Collected JSON directory for `hc-investigate` |
| `FINDING_ID` | — | Finding id for `hc-investigate` (`CHECK_ID=` or `QUERY=` also work) |
| `LEDGER` | — | `skipped_commands.jsonl` path for `hc-skip-summary` (`RESULTS_DIR=` also works) |
| `TSR_HTML` | — | TSR HTML export for `make hc-build-catalog` |
| `AI_TOOL` | — | Optional tool name passed into the Chapter 3/8 draft |
