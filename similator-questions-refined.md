# CKAD Exam Prep Questions

---

## ❯ Question 1

**Instance:** `ssh ckad5601`

The DevOps team would like to get the list of all Namespaces in the cluster. The list can contain other columns like STATUS or AGE.

Save the list to `/opt/course/1/namespaces` on ckad5601.

---

## ❯ Question 2

**Instance:** `ssh ckad5601`

Create a single Pod of image `httpd:2.4.41-alpine` in Namespace default. The Pod should be named `pod1` and the container should be named `pod1-container`.

Your manager would like to run a command manually on occasion to output the status of that exact Pod. Please write a command that does this into `/opt/course/2/pod1-status-command.sh` on ckad5601. The command should use kubectl.

---

## ❯ Question 3

**Instance:** `ssh ckad7326`

Team Neptune needs a Job template located at `/opt/course/3/job.yaml`. This Job should:
- Run image `busybox:1.31.0`
- Execute `sleep 2 && echo done`
- Be in namespace `neptune`
- Run a total of 3 times
- Execute 2 runs in parallel
- Label each pod with `id: awesome-job`
- Job name: `neb-new-job`
- Container name: `neb-new-job-container`

Start the Job and check its history.

---

## ❯ Question 4

**Instance:** `ssh ckad7326`

Team Mercury asked you to perform operations using Helm, all in Namespace `mercury`:

1. Delete release `internal-issue-report-apiv1`
2. Upgrade release `internal-issue-report-apiv2` to any newer version of chart `killershell/nginx`
3. Install a new release `internal-issue-report-apache` of chart `killershell/apache` with two replicas (set via Helm-values during install)
4. Find and delete a broken release stuck in `pending-install` state

---

## ❯ Question 5

**Instance:** `ssh ckad7326`

Team Neptune has a ServiceAccount named `neptune-sa-v2` in Namespace `neptune`. A coworker needs the token from the Secret that belongs to that ServiceAccount. 

Write the base64 decoded token to file `/opt/course/5/token` on ckad7326.

---

## ❯ Question 6

**Instance:** `ssh ckad5601`

Create a single Pod named `pod6` in Namespace default of image `busybox:1.31.0`. The Pod should:
- Have a readiness-probe executing `cat /tmp/ready`
- Have initial delay of 5 seconds
- Have period of 10 seconds
- Run the command `touch /tmp/ready && sleep 1d`

The readiness probe should set the container ready only if the file `/tmp/ready` exists. Create the Pod and confirm it starts.

---

## ❯ Question 7

**Instance:** `ssh ckad7326`

The board of Team Neptune decided to take over control of one e-commerce webserver from Team Saturn. The administrator who set it up is no longer in the organization. All information you have is that the e-commerce system is called `my-happy-shop`.

Search for the correct Pod in Namespace `saturn` and move it to Namespace `neptune`. It doesn't matter if you shut it down and spin it up again.

---

## ❯ Question 8

**Instance:** `ssh ckad7326`

There is an existing Deployment named `api-new-c32` in Namespace `neptune`. A developer made an update to the Deployment but the updated version never came online. 

Check the Deployment history and find a revision that works, then rollback to it. What was the error?

---

## ❯ Question 9

**Instance:** `ssh ckad9043`

In Namespace `pluto` there is a single Pod named `holy-api`. Team Pluto needs it to be more reliable.

Convert the Pod into a Deployment:
- Deployment name: `holy-api`
- 3 replicas
- Security context on container level: `allowPrivilegeEscalation: false` and `privileged: false`
- Delete the single Pod once done
- The raw Pod template file is available at `/opt/course/9/holy-api-pod.yaml`
- Save the Deployment yaml to `/opt/course/9/holy-api-deployment.yaml`

---

## ❯ Question 10

**Instance:** `ssh ckad9043`

Team Pluto needs a new cluster internal Service:
- Service name: `project-plt-6cc-svc` (ClusterIP type)
- Namespace: `pluto`
- Expose a single Pod named `project-plt-6cc-api`
- Pod image: `nginx:1.17.3-alpine`
- Pod label: `project: plt-6cc-api`
- Port redirection: `3333:80` (TCP)

Create the Service and Pod. Test it using curl from a temporary nginx:alpine Pod. 
- Write the response to `/opt/course/10/service_test.html`
- Write the pod logs to `/opt/course/10/service_test.log`

---

## ❯ Question 11

**Instance:** `ssh ckad9043`

There are files to build a container image located at `/opt/course/11/image`. The container will run a Golang application which outputs information to stdout.

Tasks:
- Change the Dockerfile: set ENV variable `SUN_CIPHER_ID` to `5b9c1065-e39d-4a43-a04a-e59bcea3e03f`
- Build with Docker, tag `registry.killer.sh:5000/sun-cipher:v1-docker` and push
- Build with Podman, tag `registry.killer.sh:5000/sun-cipher:v1-podman` and push
- Run a container using Podman, detached, named `sun-cipher` with image `registry.killer.sh:5000/sun-cipher:v1-podman`
- Write the container logs to `/opt/course/11/logs`

**Note:** Run all Docker and Podman commands as root. Use `sudo docker`, `sudo podman` or `sudo -i`

---

## ❯ Question 12

**Instance:** `ssh ckad5601`

Create the following in order:

1. **PersistentVolume** named `earth-project-earthflower-pv`:
   - Capacity: `2Gi`
   - Access mode: `ReadWriteOnce`
   - Host path: `/Volumes/Data`
   - No storage class defined

2. **PersistentVolumeClaim** named `earth-project-earthflower-pvc` in Namespace `earth`:
   - Request: `2Gi` storage
   - Access mode: `ReadWriteOnce`
   - No storage class defined
   - Should bound to the PV correctly

3. **Deployment** named `project-earthflower` in Namespace `earth`:
   - Mount the volume at `/tmp/project-data`
   - Pod image: `httpd:2.4.41-alpine`

---

## ❯ Question 13

**Instance:** `ssh ckad9043`

Team Moonpie needs more storage. Create:

1. **StorageClass** named `moon-retain`:
   - Provisioner: `moon-retainer`
   - Reclaim policy: `Retain`

2. **PersistentVolumeClaim** named `moon-pvc-126` in Namespace `moon`:
   - Storage: `3Gi`
   - Access mode: `ReadWriteOnce`
   - Use the `moon-retain` StorageClass

The provisioner `moon-retainer` will be created by another team, so the PVC won't boot. Write the event message from the PVC to `/opt/course/13/pvc-126-reason`.

---

## ❯ Question 14

**Instance:** `ssh ckad9043`

Make changes to Pod `secret-handler` in Namespace `moon`:

1. Create Secret `secret1` with `user=test` and `pass=pwd`
2. Mount Secret1 as env vars: `SECRET1_USER` and `SECRET1_PASS` in the Pod
3. There's existing Secret yaml at `/opt/course/14/secret2.yaml` - create it
4. Mount Secret2 inside the Pod at `/tmp/secret2`
5. Original Pod yaml is at `/opt/course/14/secret-handler.yaml`
6. Save updated yaml to `/opt/course/14/secret-handler-new.yaml`

Both Secrets should only be available in Namespace `moon`.

---

## ❯ Question 15

**Instance:** `ssh ckad9043`

Team Moonpie has an incomplete nginx Deployment `web-moon` in Namespace `moon`:

1. Create ConfigMap `configmap-web-moon-html` with the content of `/opt/course/15/web-moon.html` under the data key `index.html`
2. The Deployment `web-moon` is already configured to work with this ConfigMap
3. Test the nginx configuration using curl from a temporary nginx:alpine Pod

---

## ❯ Question 16

**Instance:** `ssh ckad7326`

There is an existing Deployment `cleaner` in Namespace `mercury` with container `cleaner-con`. The yaml is at `/opt/course/16/cleaner.yaml`.

Tasks:
1. Add a sidecar container named `logger-con`:
   - Image: `busybox:1.31.0`
   - Mount the same volume as `cleaner-con`
   - Write the content of `cleaner.log` to stdout using `tail -f`
2. Save updated yaml to `/opt/course/16/cleaner-new.yaml`
3. Make sure the Deployment is running
4. Check the logs - what do they reveal?

---

## ❯ Question 17

**Instance:** `ssh ckad5601`

There is a Deployment yaml at `/opt/course/17/test-init-container.yaml` that spins up a single Pod of image `nginx:1.17.3-alpine` serving files from a mounted volume.

Tasks:
1. Create an InitContainer named `init-con`:
   - Image: `busybox:1.31.0`
   - Mount the same volume
   - Create file `index.html` with content `check this out!` in the root of the mounted volume
2. Test your implementation using curl from a temporary nginx:alpine Pod

---

## ❯ Question 18

**Instance:** `ssh ckad5601`

There is an issue in Namespace `mars`. The ClusterIP Service `manager-api-svc` should make the Pods of Deployment `manager-api-deployment` available inside the cluster.

Test this with: `curl manager-api-svc.mars:4444` from a temporary nginx:alpine Pod

Check for the misconfiguration and apply a fix.

---

## ❯ Question 19

**Instance:** `ssh ckad5601`

In Namespace `jupiter` you'll find:
- Apache Deployment `jupiter-crew-deploy` (one replica)
- ClusterIP Service `jupiter-crew-svc` exposing it

Tasks:
1. Change the Service to NodePort type on port `30100`
2. Test the Service using the internal IP of all available nodes and port `30100` with curl
3. Answer: On which nodes is the Service reachable? On which node is the Pod running?

---

## ❯ Question 20

**Instance:** `ssh ckad7326`

In Namespace `venus` you'll find two Deployments: `api` and `frontend`, both exposed via Services.

Create NetworkPolicy `np1` that:
1. Restricts outgoing TCP connections from Deployment `frontend`
2. Only allows TCP connections to Deployment `api`
3. Still allows outgoing DNS traffic on UDP/TCP port 53

Test with:
- `wget www.google.com` from a Pod of Deployment `frontend` (should fail)
- `wget api:2222` from a Pod of Deployment `frontend` (should work)

---

## ❯ Question 21

**Instance:** `ssh ckad7326`

Team Neptune needs a Deployment:
- Name: `neptune-10ab`
- Namespace: `neptune`
- Image: `httpd:2.4-alpine`
- Replicas: 3
- Container name: `neptune-pod-10ab`
- Memory request: `20Mi`
- Memory limit: `50Mi`
- Run under ServiceAccount: `neptune-sa-v2`

---

## ❯ Question 22

**Instance:** `ssh ckad9043`

Team Sunny needs to identify Pods in Namespace `sun`:

1. Add label `protected: true` to all Pods with existing label `type: worker` OR `type: runner`
2. Add annotation `protected: do not delete this pod` to all Pods that have the new label `protected: true`

