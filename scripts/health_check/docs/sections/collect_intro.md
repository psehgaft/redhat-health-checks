Zero-dependency data collection for OpenShift Health Check engagements.

**Requirements:** `oc` CLI. No `jq`. `python3` is required for categories `10_metrics` and `11_hardware`; the shared capture helper (`lib/common.sh`) also uses `python3` opportunistically in every category for empty-list detection (it degrades gracefully when absent, but full result fidelity needs it).  
**Cluster access:** Collection is read-only by design — with one exception: `11_hardware.sh` runs `oc debug node/...`, which creates short-lived debug pods that are removed automatically after each capture. Nothing else is created, modified, or deleted.  
**Support matrix:** Targets OpenShift 4.x (active versions tracked in `scripts/health_check/hc_report/kb/versions.toml`, currently 4.18–4.22). Use an `oc` client within one minor version of the cluster (Kubernetes version-skew policy).
