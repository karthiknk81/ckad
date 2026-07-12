# Secret Scenario Questions

These CKAD-style questions are designed to help students practice secret-related tasks with concrete names, values, and expected outputs.

## Scenario 1: Create a Generic Secret for App Credentials
Create a secret named `app-credentials` with the following key/value pairs:
- `DB_USERNAME=admin`
- `DB_PASSWORD=Pa$$w0rd123`

Then create a pod named `app-pod` that consumes these values as environment variables named `DB_USERNAME` and `DB_PASSWORD`.

---

## Scenario 2: Create a Secret from an Env File for a Web App
Create a secret named `web-app-env` from an env file named `.env.prod`.

The file must contain at least these entries:
- `APP_PORT=8080`
- `LOG_LEVEL=debug`

Create a pod named `web-app-pod` that mounts this secret as a volume at `/etc/app-config` and ensures the files are visible inside the container.

---

## Scenario 3: Create a Docker Registry Secret for Private Image Pulls
Create a Docker registry secret named `registry-creds` for the registry `registry.example.com` using the username `devuser` and password `devpass123`.

Then create a pod named `private-image-pod` that uses this secret so the image can be pulled successfully from the private registry.

---

## Scenario 4: Create a TLS Secret for an HTTPS Service
Create a TLS secret named `nginx-tls` using the files `tls.crt` and `tls.key` provided in the environment.

Create a pod named `nginx-tls-pod` that mounts this secret and uses it for an HTTPS server configuration.

---

## Scenario 5: Create an SSH Auth Secret for Git Access
Create an SSH auth secret named `git-ssh-secret` using the private key file `id_rsa`.

Create a pod named `git-helper-pod` that mounts this secret at `/root/.ssh` so a Git client can use it for repository access.

---

## Scenario 6: Create an Opaque Secret with Binary Data
Create an opaque secret named `binary-config` using the file `certificate.bin`.

Create a pod named `binary-reader-pod` that mounts this secret as a volume and reads the file from inside the container.

---

## Scenario 7: Create a Secret Using stringData in a YAML Manifest
Create a secret named `app-secrets-yaml` using a YAML manifest with `stringData`.

The secret must contain:
- `API_KEY=sample-api-key`
- `TOKEN=sample-token`

Apply the manifest and confirm the secret exists in the cluster.

---

## Scenario 8: Create an Immutable Secret and Test Update Failure
Create an immutable secret named `immutable-db-secret` with the key `DB_PASSWORD` and value `initial-pass`.

Then attempt to update the secret value and confirm that Kubernetes rejects the change because the secret is immutable.

---

## Scenario 9: Attach a Pull Secret to a ServiceAccount
Create a Docker registry secret named `sa-registry-creds` for `registry.example.com`.

Create a ServiceAccount named `build-sa` and attach this secret to it so that pods using `build-sa` can pull images from the private registry.

---

## Scenario 10: Create a Secret from a kubeconfig File
Create a secret named `cluster-kubeconfig` from the file `config` located in the current directory.

Then create a pod named `kubeconfig-reader-pod` that mounts this secret so the application can access the kubeconfig file at `/tmp/config`.

---

## Scenario 11: Add Labels and Annotations to a Secret
Create a secret named `ops-secret` with the key `API_TOKEN` and value `ops-token-123`.

Add the following labels and annotations:
- Label: `team=platform`
- Label: `env=prod`
- Annotation: `owner=devops`

Verify that the secret includes these metadata entries.

---

## Scenario 12: Project Multiple Secret Sources into One Volume
Create two secrets named `secret-a` and `secret-b`.

Create a pod named `projected-secret-pod` that uses a projected volume to mount both secrets into a single directory at `/etc/secret-volume`.

Ensure that both secret keys are visible inside the container.
