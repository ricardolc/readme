Let's create a simple deployment using nginx, as we do so we'll tee the yaml to a file and we'll apply it, at the same time, we're going to revisit this yaml later -

kubectl create deployment nginx --image=nginx --dry-run=client -o yaml | tee nginx-deployment.yaml | kubectl apply -f -

If we query deployments, we will see our nginx deployment -

kubectl get deployment

We will now have a replicaSet, with a unique identifier, note the name of the identifier, make a reference to this for comparison later on -

kubectl get replicaset

If we query our pods, these will be named with the name of the deployment, replicaSet and a unique identifier -

kubectl get pods -o wide

Deployments have a history, lets check the initial rollout history -

kubectl rollout history deployment/nginx

At the moment there is only 1 section in our history, we can annote this to make use of this record -

kubectl annotate deployment/nginx kubernetes.io/change-cause="initial deployment"

And if we check again, we can see our annotation -

kubectl rollout history deployment/nginx

Currently our deployment has a single replica and it's using the nginx image, verify this using get deployment -

kubectl get deployment -o wide

Let's scale the number of replicas, we will run a watch command straight after to see this as it progresses, press ctrl-c to exit -

kubectl scale deployment/nginx --replicas=10; watch kubectl get pods -o wide