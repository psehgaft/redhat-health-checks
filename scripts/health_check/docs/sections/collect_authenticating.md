### Option A — Kubeconfig file (preferred)

If you have a kubeconfig, pass it directly:

```bash
make hc-collect KUBECONFIG=/path/to/kubeconfig
```

Or with the script directly:

```bash
bash hc_collect.sh --kubeconfig /path/to/kubeconfig --output-dir ./hc_results
```

If `KUBECONFIG` is already set in your shell environment, you can omit the flag entirely:

```bash
make hc-collect
```

A kubeconfig is a bearer credential — restrict it on disk:

```bash
chmod 600 /path/to/kubeconfig
```

### Option B — Username and password

If you were given credentials instead of a kubeconfig, log in first to generate one. You need the cluster API server URL — your contact at the customer should be able to provide it.

Prefer the interactive prompt so the password never lands in your shell history:

```bash
# Log in — this creates/updates ~/.kube/config.
# Omit --password to be prompted securely:
oc login https://api.<cluster-name>.<domain>:6443 \
  --username=<username>
```

Only pass `--password` in non-interactive contexts, sourced from a protected variable — never typed literally or committed anywhere:

```bash
oc login https://api.<cluster-name>.<domain>:6443 \
  --username="${HC_USERNAME}" \
  --password="${HC_PASSWORD}"
```

If the cluster uses a self-signed certificate, point `oc` at the cluster CA bundle instead of disabling verification:

```bash
oc login https://api.<cluster-name>.<domain>:6443 \
  --username=<username> \
  --certificate-authority=/path/to/ca.crt
```

> Avoid `--insecure-skip-tls-verify` except as a last resort on a trusted network: it disables server-identity verification and exposes your credentials to interception.

After a successful login, your kubeconfig is populated at `~/.kube/config`. Run collection normally:

```bash
make hc-collect
# or explicitly:
make hc-collect KUBECONFIG=~/.kube/config
```

### Option C — Username and password with an isolated kubeconfig

If you do not want to overwrite your existing `~/.kube/config` (e.g. you manage multiple clusters), create a separate file:

```bash
KUBECONFIG=./customer-kubeconfig \
  oc login https://api.<cluster-name>.<domain>:6443 \
  --username=<username>

chmod 600 ./customer-kubeconfig
make hc-collect KUBECONFIG=./customer-kubeconfig
```

### Option D — API token

If you have a service account token or a user token, prefer pasting the **Copy login command** from the OpenShift web console (user profile menu) directly — it avoids typing the token into your shell history:

```bash
oc login --token=sha256~<token> --server=https://api.<cluster-name>.<domain>:6443
```

Then run collection normally:

```bash
make hc-collect
```

### Credential hygiene after the engagement

Treat every kubeconfig and token as a live credential until it is revoked:

- Run `oc logout` when you are done, and delete isolated kubeconfig copies (`shred -u ./customer-kubeconfig` where available).
- Ask the cluster administrator to revoke any service-account tokens created for the engagement.
- `output/`, `project.yaml`, and kubeconfig paths are gitignored — never commit collected data or credentials.
