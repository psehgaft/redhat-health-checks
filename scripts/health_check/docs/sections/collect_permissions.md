The account used for collection needs **read access** to cluster-scoped resources. `cluster-admin` is simplest; if you need a minimal role, the account must be able to `get` and `list` the following:

- All resources in `openshift-*` namespaces
- `nodes`, `namespaces`, `clusteroperators`, `clusterversion`, `infrastructure`
- `clusterrolebindings`, `rolebindings`, `scc`, `oauth`
- Custom resources for any layered products being assessed

Category `11_hardware` additionally needs permission to create the ephemeral debug pods used by `oc debug node/...` (removed automatically after each capture) — covered by `cluster-admin`, or by a role that allows debug-pod creation on nodes.
