# ConfigMap Scenario Questions

These CKAD-style questions are designed to help students practice ConfigMap-related tasks with concrete names, values, and expected outputs.

## Scenario 1: Create a ConfigMap from Literal Values
Create a ConfigMap named `app-config` with the following entries:
- `APP_MODE=production`
- `LOG_LEVEL=info`

Then create a pod named `config-app-pod` that consumes these values as environment variables named `APP_MODE` and `LOG_LEVEL`.

---

## Scenario 2: Create a ConfigMap from a File
Create a ConfigMap named `app-settings` from a file named `app.properties`.

The file should contain at least:
- `db.host=postgres`
- `db.port=5432`

Create a pod named `settings-pod` that mounts this ConfigMap as a volume at `/etc/app-settings` and ensures the file is visible inside the container.

---

## Scenario 3: Create a ConfigMap from Multiple Files
Create a ConfigMap named `multi-file-config` from two files named `config1.txt` and `config2.txt` in the current directory.

Then create a pod named `multi-file-pod` that mounts the ConfigMap into `/etc/multi-config` and confirms both files are available.

---

## Scenario 4: Create a ConfigMap from an Env File
Create a ConfigMap named `env-config` from an env file named `.env.dev`.

The file should contain at least:
- `API_URL=http://api.internal`
- `TIMEOUT=30`

Create a pod named `env-config-pod` that uses these values as environment variables.

---

## Scenario 5: Create a ConfigMap Using a YAML Manifest
Create a ConfigMap named `app-config-yaml` using a YAML manifest with `data` entries.

The ConfigMap must contain:
- `PORT=8080`
- `HOST=0.0.0.0`

Apply the manifest and verify that the ConfigMap exists in the cluster.

---

## Scenario 6: Use a ConfigMap in a Deployment for Runtime Configuration
Create a ConfigMap named `web-config` with the key `WELCOME_MESSAGE=Hello from CKAD`.

Then create a Deployment named `web-deployment` that uses this ConfigMap as an environment variable and runs a simple web container.

---

## Scenario 7: Reference ConfigMap Keys in Container Commands and Arguments
Create a ConfigMap named `startup-config` with the key `COMMAND=echo` and `ARGUMENT=hello`.

Create a pod named `command-pod` that uses the ConfigMap values inside the container command and arguments so the container prints `hello` when it starts.

---

## Scenario 8: Update a ConfigMap Without Rebuilding the Image
Create a ConfigMap named `feature-flags` with the key `ENABLE_NEW_UI=false`.

Create a pod named `feature-pod` that reads this value from the environment.

Then update the ConfigMap value to `true` and verify that the running pod picks up the new value without restarting the image.

---

## Scenario 9: Mount a ConfigMap as a Projected Volume
Create two ConfigMaps named `config-a` and `config-b`.

Create a pod named `projected-config-pod` that uses a projected volume to mount both ConfigMaps into a single directory at `/etc/projected-config`.

Ensure that all keys from both ConfigMaps are visible inside the container.

---

## Scenario 10: Apply Labels and Annotations to a ConfigMap
Create a ConfigMap named `ops-config` with the key `ENV=production`.

Add the following labels and annotations:
- Label: `team=platform`
- Label: `env=prod`
- Annotation: `owner=devops`

Verify that the ConfigMap includes these metadata entries.

---

## Scenario 11: Use ConfigMap Data in a StatefulSet
Create a ConfigMap named `stateful-app-config` with the keys `DB_HOST=db-service` and `DB_PORT=5432`.

Create a StatefulSet named `stateful-app` that uses these values as environment variables for the container.

---

## Scenario 12: Create a ConfigMap from a Directory of Files
Create a directory named `config-dir` containing two files: `app.conf` and `logging.conf`.

Create a ConfigMap named `dir-config` from that directory.

Then create a pod named `dir-config-pod` that mounts the ConfigMap into `/etc/config-dir` and confirms the files are present.
