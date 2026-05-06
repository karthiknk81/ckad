**Multi Container POD - Use Cases**

1. POD with two or more containers
2. POD with two or more containers sharing common storage (`emptyDir`)
3. POD with Init Container
4. POD with Init Container sharing volume with main container
5. POD with Sidecar Container (native, `restartPolicy: Always` in initContainers)
6. POD with Ambassador pattern (proxy sidecar)
7. POD with Adapter pattern (transform sidecar)

