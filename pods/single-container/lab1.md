**Single Container POD — CKAD Practice Lab Questions**

---

**1. Plain POD Deployment**
Create a POD named `web` using the image `nginx:latest` in the default namespace. Verify the POD is running.

---

**2. POD in a Specific Namespace**
Create a namespace called `dev-ns`. Deploy a POD named `app-pod` using image `busybox:latest` with command `sleep 3600` in the `dev-ns` namespace. Verify it is running in the correct namespace.

---

**3. POD with Specific Labels**
Create a POD named `labeled-pod` using image `nginx` with the following labels:
- `env=production`
- `tier=frontend`
- `app=webapp`

After creating, retrieve all PODs that have label `env=production`.

---

**4. POD with `nodeSelector`**
A node in your cluster has the label `disktype=ssd`. Create a POD named `ssd-pod` using image `nginx` that must only schedule on that node using `nodeSelector`. Verify on which node it is scheduled.

---

**5. POD with Node Affinity**
Create a POD named `affinity-pod` using image `nginx` with a **required** node affinity rule so it only schedules on nodes labeled `environment=prod`. Also add a **preferred** rule to prefer nodes labeled `zone=us-east`. Verify scheduling.

---

**6. POD with Tolerations**
A node has the taint `dedicated=backend:NoSchedule`. Create a POD named `toleration-pod` using image `nginx` that tolerates this taint and can schedule on that node.

---

**7. POD with `command` and `args` Override**
Create a POD named `cmd-pod` using image `busybox` that overrides the default entrypoint to run:
```
echo "CKAD Practice" && sleep 3600
```
Verify the output by checking the pod logs.

---

**8. POD with ENV Variable**
Create a POD named `env-pod` using image `nginx` with the following environment variables set directly:
- `APP_ENV=staging`
- `APP_VERSION=1.0.0`

Exec into the pod and verify both variables are set.

---

**9. POD with ENV from ConfigMap — All Keys**
Create a ConfigMap named `app-config` in namespace `dev-ns` with the following data:
- `DB_HOST=mysql-service`
- `DB_PORT=3306`
- `DB_NAME=appdb`

Create a POD named `cm-env-pod` that loads **all keys** from this ConfigMap as environment variables. Verify inside the pod.

---

**10. POD with ENV from ConfigMap — Selected Key**
Using the same ConfigMap `app-config` from above, create a POD named `cm-selected-pod` that only injects `DB_HOST` as an environment variable named `DATABASE_HOST`. Verify inside the pod.

---

**11. POD with ENV from Secret**
Create a Secret named `db-secret` with:
- `DB_USER=admin`
- `DB_PASSWORD=s3cr3t`

Create a POD named `secret-env-pod` using image `nginx` that injects both secret values as environment variables. Verify inside the pod.

---

**12. POD with Resource Limits and Requests**
Create a POD named `resource-pod` using image `nginx` with the following resource constraints:
- Requests: CPU `100m`, Memory `128Mi`
- Limits: CPU `250m`, Memory `256Mi`

Verify the resource settings are applied using `kubectl describe`.

---

**13. POD with Security Context — Container Level**
Create a POD named `sec-container-pod` using image `busybox` with command `sleep 3600` and the following container-level security context:
- Run as user `1000`
- Disallow privilege escalation
- Read-only root filesystem

Verify by exec-ing into the pod and attempting to write to the filesystem.

---

**14. POD with Security Context — POD Level**
Create a POD named `sec-pod` using image `busybox` with command `sleep 3600` and the following pod-level security context:
- `runAsGroup: 3000`
- `fsGroup: 2000`

Exec into the pod and verify the group IDs using `id` command.

---

**15. POD with Service Account**
Create a ServiceAccount named `app-sa` in namespace `dev-ns`. Create a POD named `sa-pod` using image `nginx` that uses this ServiceAccount. Verify the correct ServiceAccount is assigned.

---

**16. POD with `imagePullSecrets`**
Create a Secret named `registry-secret` of type `kubernetes.io/dockerconfigjson` for a private registry. Create a POD named `private-pod` that uses this secret to pull an image from the private registry.

---

**17. POD with Volume Mount: `emptyDir`**
Create a POD named `emptydir-pod` using image `nginx` with an `emptyDir` volume named `cache-vol` mounted at `/cache` inside the container. Exec into the pod, create a file at `/cache/test.txt`, and verify it exists.

---

**18. POD with Volume Mount: `hostPath`**
Create a POD named `hostpath-pod` using image `nginx` that mounts the host directory `/tmp/hostdata` into the container at `/data` using a `hostPath` volume. Verify by writing a file from inside the pod and checking it appears on the node.

---

**19. POD with Volume Mount: ConfigMap**
Create a ConfigMap named `html-config` with a key `index.html` containing the value `<h1>Hello CKAD</h1>`. Create a POD named `cm-vol-pod` using image `nginx` that mounts this ConfigMap as a volume at `/usr/share/nginx/html`. Verify by curling the nginx endpoint.

---

**20. POD with Volume Mount: Secret**
Create a Secret named `tls-secret` with two keys: `tls.crt` and `tls.key` with dummy values. Create a POD named `secret-vol-pod` using image `nginx` that mounts this secret as a volume at `/etc/tls`. Verify the files are present inside the pod.

---

**21. POD with Persistent Storage**
Create a PersistentVolume named `local-pv` of `1Gi` using `hostPath` at `/tmp/pvdata`. Create a PersistentVolumeClaim named `local-pvc` requesting `500Mi`. Create a POD named `pv-pod` using image `nginx` that mounts this PVC at `/data`. Verify the volume is bound and mounted.

---

**22. POD with Probes**
Create a POD named `probe-pod` using image `nginx` with:
- **Liveness probe**: HTTP GET on `/` port `80`, initial delay `5s`, period `10s`
- **Readiness probe**: HTTP GET on `/` port `80`, initial delay `3s`, period `5s`
- **Startup probe**: HTTP GET on `/` port `80`, failure threshold `30`, period `10s`

Verify all probes are configured using `kubectl describe`.

---

**23. POD with `restartPolicy`**
Create a POD named `job-pod` using image `busybox` that runs the command `echo "done" && exit 0` with `restartPolicy: OnFailure`. Observe its lifecycle. Then create another POD with the same command but `restartPolicy: Never` and compare behavior.

---

**Tips for CKAD lab conditions:**
- Practice using `kubectl run` for speed wherever possible
- Use `kubectl run --dry-run=client -o yaml` to generate base YAML then edit
- Know how to use `kubectl explain pod.spec.containers.securityContext` to look up fields fast without memorizing
- Time yourself — aim for under 5 minutes per scenario