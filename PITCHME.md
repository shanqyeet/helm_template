## CI/CD with Jenkins + Helm Chart
---
##### Current Deployment Process
1. Pull latest Develop branch
2. Update deployment.yaml and configmap.yaml 
3. Compile MS to jib into Harbor
4. If no changes to yaml files:
	- run `kubectl get rs` to retrieve replicasets 
	- kill the existing pods to retrieve update image
+++
5. If changes is made to yaml files 
	- run `kubectl apply -f files` to deploy the MS
6. Check status of deployment 
	- run `kubectl get pods` to retrive deployed pods
	- run `kubectl logs pod` to check deployment status
---
##### New Deployment Process
1. Update value.yaml file before submitting merge request to develop
2. Upon merge, pipeline will be executed to deploy app to kubernetes with deployment status report 

---
##### Changes Required To Adapt
1. No major change required, can keep existing kubernetes folders structure
2. Remove deployment.yaml and configmap.yaml file
3. Replace with value.yaml file for each respective env
4. Possible challenge is templatize configmap 
