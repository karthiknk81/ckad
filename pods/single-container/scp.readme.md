**Single Container POD - Use Cases**

1. Plain POD Deployment
2. POD in a specific namespace
3. POD with specific labels
4. POD with `nodeSelector`
5. POD with Node Affinity / Node preference
6. POD with Tolerations
7. POD with `command` and `args` override
8. POD with ENV variable
9. POD with ENV from ConfigMap — All keys as ENV variables
10. POD with ENV from ConfigMap — Selected key only
11. POD with ENV from Secret
12. POD with Resource Limits and Requests
13. POD with Security Context — Container level (`runAsUser`, `readOnlyRootFilesystem`, `allowPrivilegeEscalation`)
14. POD with Security Context — POD level (`runAsGroup`, `fsGroup`)
15. POD with Service Account assigned
16. POD with `imagePullSecrets` (private registry)
17. POD with Volume Mount: `emptyDir`
18. POD with Volume Mount: `hostPath`
19. POD with Volume Mount: ConfigMap
20. POD with Volume Mount: Secret
21. POD with Persistent Storage — PersistentVolume + PVC
22. POD with Probes: Liveness, Readiness, Startup
23. POD with `restartPolicy` (`Always`, `OnFailure`, `Never`)

