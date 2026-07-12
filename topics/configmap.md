# ConfigMaps

## Creations
- Create a generic ConfigMap from literal key/value pairs: `kubectl create configmap NAME --from-literal=key=value`
- Create a ConfigMap from a file: `kubectl create configmap NAME --from-file=path/to/file`
- Create a ConfigMap from multiple files: `kubectl create configmap NAME --from-file=dir/`
- Create a ConfigMap from an env file: `kubectl create configmap NAME --from-env-file=.env`
- Create a ConfigMap from a manifest using `data:` entries
- Create a ConfigMap with multiple keys and values for app configuration
- Create a ConfigMap from a directory of files for grouped settings

## Usage
- Mount a ConfigMap as a volume in a pod
- Inject ConfigMap values as environment variables in a pod
- Reference ConfigMap keys inside container commands and args
- Update application behavior by changing ConfigMap data without rebuilding images
- Use a ConfigMap with a Deployment or StatefulSet for runtime configuration
- Combine multiple ConfigMap sources in a projected volume
- Apply labels and annotations for selection and management
