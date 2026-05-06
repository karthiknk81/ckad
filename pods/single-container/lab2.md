**CKAD Single Container POD — Comprehensive Lab Exam**

*35 questions | Estimated time: 3.5 hours | Aim for under 6 minutes per question*

---

### Section 1 — Fundamentals (Warm Up)

**Q1.**
Create a POD named `nginx-pod` using image `nginx:1.21` in the default namespace. Verify it is running and note the node it was scheduled on.

---

**Q2.**
Create a namespace `ckad-prep`. Deploy a POD named `busybox-pod` using image `busybox` with command `sleep 3600` in that namespace. Verify it is in `Running` state.

---

**Q3.**
Create a POD named `labeled-web` using image `nginx` with labels:
- `app=web`
- `env=staging`
- `tier=frontend`

Then list all PODs with label `env=staging` across all namespaces.

---

**Q4.**
You have an existing POD named `unlabeled-pod` running in default namespace. Add a label `team=backend` to it without deleting and recreating the POD.

---

### Section 2 — Scheduling

**Q5.**
Label a node in your cluster with `disk=ssd`. Create a POD named `ssd-nginx` using image `nginx` that must only run on that node using `nodeSelector`. Verify which node it landed on.

---

**Q6.**
Create a POD named `required-affinity-pod` using image `nginx` with a **required** node affinity so it only schedules on nodes with label `env=prod`. Do NOT use `nodeSelector`. Verify.

---

**Q7.**
Create a POD named `preferred-affinity-pod` using image `busybox` with command `sleep 3600` that:
- **Requires** scheduling on nodes labeled `tier=backend`
- **Prefers** nodes labeled `zone=us-east` with weight `80`

---

**Q8.**
Taint a node with `dedicated=gpu:NoSchedule`. Create a POD named `gpu-pod` using image `nginx` that tolerates this taint. Verify it is scheduled on the tainted node.

---

**Q9.**
A node has two taints:
- `env=prod:NoSchedule`
- `type=ssd:NoExecute`

Create a POD named `multi-toleration-pod` using image `nginx` that tolerates **both** taints.

---

**Q10.**
Create a POD named `no-schedule-pod` using image `nginx` with a `nodeSelector` for `disk=nvme`. There is no such labeled node in the cluster. Observe and describe what happens to the POD. What is its status and why?

---

### Section 3 — Configuration & Environment

**Q11.**
Create a POD named `env-direct-pod` using image `busybox` with command `sleep 3600` and the following environment variables:
- `APP_COLOR=blue`
- `APP_VERSION=2.1`
- `LOG_LEVEL=debug`

Exec into the pod and verify all three are set.

---

**Q12.**
Create a ConfigMap named `db-config` in namespace `ckad-prep` with:
- `DB_HOST=postgres-svc`
- `DB_PORT=5432`
- `DB_NAME=myapp`
- `DB_SCHEMA=public`

Create a POD named `db-env-pod` in `ckad-prep` that loads **all** keys from this ConfigMap as environment variables. Verify inside the pod.

---

**Q13.**
Using the same ConfigMap `db-config` from Q12, create a POD named `db-selective-pod` that only injects:
- `DB_HOST` as `DATABASE_HOST`
- `DB_PORT` as `DATABASE_PORT`

Verify that `DB_NAME` and `DB_SCHEMA` are **not** present inside the pod.

---

**Q14.**
Create a Secret named `app-secret` in `ckad-prep` with:
- `API_KEY=abc123xyz`
- `API_SECRET=s3cr3tpass`

Create a POD named `secret-env-pod` that injects both as environment variables. Exec in and verify. Also confirm the secret values are not visible in plain text in `kubectl describe pod`.

---

**Q15.**
Create a POD named `mixed-env-pod` using image `busybox` with command `sleep 3600` that has:
- A direct ENV: `APP_ENV=production`
- `DB_HOST` from ConfigMap `db-config` (Q12) as `DATABASE_HOST`
- `API_KEY` from Secret `app-secret` (Q14) as `APP_API_KEY`

Verify all three inside the pod.

---

**Q16.**
Create a POD named `cmd-pod` using image `busybox` that:
- Overrides the entrypoint to run `/bin/sh`
- Passes args `-c` and `echo "Hello from CKAD" && sleep 3600`

Check the logs to confirm the echo output.

---

**Q17.**
Create a POD named `cmd-env-pod` using image `busybox` that:
- Sets ENV `GREETING=HelloCKAD`
- Runs command `echo $(GREETING)` then sleeps 3600

Verify via logs that the ENV variable was expanded in the command.

---

### Section 4 — Resources & Security

**Q18.**
Create a POD named `resource-pod` in `ckad-prep` using image `nginx` with:
- Requests: CPU `100m`, Memory `128Mi`
- Limits: CPU `500m`, Memory `256Mi`

Verify using `kubectl describe`. What happens if you set memory limit lower than request?

---

**Q19.**
Create a POD named `sec-user-pod` using image `busybox` with command `sleep 3600` and container-level security context:
- Run as user `1000`
- Run as group `1000`
- Disallow privilege escalation

Exec into the pod and run `id` to verify.

---

**Q20.**
Create a POD named `readonly-pod` using image `busybox` with command `sleep 3600` and:
- Read-only root filesystem
- Run as non-root user `2000`

Exec into the pod and try to create a file at `/tmp/test.txt`. What happens and why?

---

**Q21.**
Create a POD named `fsgroup-pod` using image `busybox` with command `sleep 3600` with pod-level security context:
- `runAsUser: 1000`
- `runAsGroup: 3000`
- `fsGroup: 2000`

Mount an `emptyDir` volume at `/data`. Exec in, create a file at `/data/test.txt` and check its ownership using `ls -la`.

---

**Q22.**
Create a ServiceAccount named `pod-sa` in `ckad-prep`. Create a POD named `sa-pod` using image `nginx` in `ckad-prep` that uses this ServiceAccount. Verify using `kubectl describe pod` that the correct SA is mounted.

---

**Q23.**
Create a POD named `no-sa-pod` using image `nginx` that explicitly **disables** automounting of the default service account token. Verify no token is mounted inside the pod.

---

### Section 5 — Volumes & Storage

**Q24.**
Create a POD named `emptydir-pod` using image `busybox` with command `sleep 3600` that:
- Mounts an `emptyDir` volume named `scratch` at `/scratch`

Exec into the pod, create a file `/scratch/hello.txt` with content `CKAD`. Verify it exists. Then delete and recreate the pod — what happens to the file?

---

**Q25.**
Create a POD named `hostpath-pod` using image `busybox` with command `sleep 3600` that mounts host path `/tmp/ckad-data` at `/data` inside the container. Exec into the pod, write a file `/data/from-pod.txt`. SSH into the node and verify the file exists at `/tmp/ckad-data/from-pod.txt`.

---

**Q26.**
Create a ConfigMap named `nginx-html` with key `index.html` and value:
```
<html><body><h1>CKAD Lab</h1></body></html>
```
Create a POD named `cm-vol-pod` using image `nginx` that mounts this ConfigMap as a volume at `/usr/share/nginx/html`. Verify by running `curl localhost` inside the pod.

---

**Q27.**
Create a Secret named `app-tls` with:
- `tls.crt=CERTDATA`
- `tls.key=KEYDATA`

Create a POD named `secret-vol-pod` using image `nginx` that mounts this secret as a volume at `/etc/ssl/app`. Exec in and verify both files exist with correct names.

---

**Q28.**
Create a PersistentVolume named `task-pv` with:
- Capacity: `1Gi`
- AccessMode: `ReadWriteOnce`
- HostPath: `/tmp/task-data`
- StorageClass: `manual`

Create a PersistentVolumeClaim named `task-pvc` requesting `500Mi` with StorageClass `manual`. Create a POD named `pv-pod` using image `nginx` mounting the PVC at `/usr/share/nginx/html`. Verify the PVC is `Bound`.

---

**Q29.**
Create a POD named `multi-vol-pod` using image `busybox` with command `sleep 3600` that has:
- An `emptyDir` volume mounted at `/cache`
- A ConfigMap volume (use `db-config` from Q12) mounted at `/config`
- A Secret volume (use `app-secret` from Q14) mounted at `/secrets`

Verify all three mount points exist inside the pod.

---

### Section 6 — Probes & Lifecycle

**Q30.**
Create a POD named `probe-pod` using image `nginx` with:
- Liveness probe: HTTP GET `/` on port `80`, initial delay `5s`, period `10s`, failure threshold `3`
- Readiness probe: HTTP GET `/` on port `80`, initial delay `3s`, period `5s`

Verify both probes are configured. Then exec into the pod and stop nginx (`nginx -s stop`) — observe what happens.

---

**Q31.**
Create a POD named `startup-probe-pod` using image `nginx` with:
- Startup probe: HTTP GET `/` on port `80`, failure threshold `30`, period `10s`
- Liveness probe: HTTP GET `/` on port `80`, period `10s`

Explain why the startup probe is needed alongside the liveness probe for slow-starting applications.

---

**Q32.**
Create a POD named `restart-onfailure` using image `busybox` with:
- Command: `sh -c "exit 1"`
- `restartPolicy: OnFailure`

Observe the pod status and restart count. Then create a second POD named `restart-never` with same command but `restartPolicy: Never`. Compare the behavior of both.

---

### Section 7 — Mixed Bag (Hard)

**Q33.**
Create a POD named `hardened-pod` in namespace `ckad-prep` using image `nginx:1.21` with ALL of the following:
- Labels: `app=hardened`, `env=prod`
- Resource requests: CPU `100m`, memory `128Mi`; limits: CPU `300m`, memory `256Mi`
- Container security context: run as user `1000`, read-only root filesystem, no privilege escalation
- ENV: `APP_MODE=production` set directly
- `DB_HOST` from ConfigMap `db-config` as `DATABASE_HOST`
- `API_KEY` from Secret `app-secret` as `APP_KEY`
- Liveness probe: HTTP GET `/` port `80`, initial delay `10s`
- ServiceAccount: `pod-sa`

Verify everything is applied correctly.

---

**Q34.**
A POD named `broken-pod` has been deployed but is stuck in `Pending` state. Without deleting it, diagnose **why** it is pending and describe the steps you would take to identify the root cause. List at least 3 possible reasons and the exact commands to investigate each.

---

**Q35.**
Create a POD named `full-stack-pod` in `ckad-prep` using image `busybox` with command `sleep 3600` combining:
- NodeSelector: `disk=ssd` (label the node first)
- Toleration for taint `dedicated=gpu:NoSchedule`
- Pod-level security context: `runAsUser: 1000`, `fsGroup: 2000`
- `emptyDir` volume at `/tmp/workdir`
- ENV directly: `RUNTIME=k8s`
- `DB_PORT` from ConfigMap `db-config` as `PORT`
- Resource limits: CPU `200m`, memory `128Mi`
- Readiness probe: exec command `ls /tmp/workdir`, initial delay `5s`

Verify the pod is running and all configurations are applied.

---

**Scoring Guide**

| Score | Level |
|---|---|
| 30–35 correct | CKAD ready |
| 23–29 correct | Close — revisit weak sections |
| 15–22 correct | Need more practice on combined scenarios |
| Below 15 | Go back to individual scenarios first |

**Time targets per section:**
- Section 1–2 (Fundamentals + Scheduling): 40 min
- Section 3 (Config & ENV): 45 min
- Section 4 (Resources & Security): 35 min
- Section 5 (Volumes): 40 min
- Section 6 (Probes): 25 min
- Section 7 (Mixed): 35 min