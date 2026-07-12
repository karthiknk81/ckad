# Secrets

## Creations
- Create a generic secret from literal key/value pairs: `kubectl create secret generic NAME --from-literal=key=value`
- Create a secret from an env file: `kubectl create secret generic NAME --from-env-file=.env`
- Create a Docker registry secret for image pulls: `kubectl create secret docker-registry NAME --docker-username=... --docker-password=... --docker-server=...`
- Create a TLS secret from cert and key files: `kubectl create secret tls NAME --cert=path/to/cert --key=path/to/key`
- Create an SSH auth secret from a private key file for Git access: `kubectl create secret generic NAME --from-file=ssh-privatekey=path/to/key --type=kubernetes.io/ssh-auth`
- Create an opaque secret with binary data using `--from-file` or `--type=kubernetes.io/opaque`
- Create a secret using `stringData` in manifests to avoid manual base64 encoding
- Create an immutable secret using `immutable: true` in metadata or `--immutable` when supported

## Usage
- Mount a secret as a volume in a pod
- Reference secret keys as environment variables in a pod
- Add a secret to a ServiceAccount via `imagePullSecrets` for image pulls
- Create a secret from a kubeconfig file for cluster access
- Apply labels and annotations for selection and management
- Project multiple secret sources into a single projected volume
