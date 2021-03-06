# The Cheat Sheet Resources

## k8s:

```bash
# Watch/get pods 
kubectl get pod -o wide -n <my-namespace> --watch

# show logs 
kubectl logs -f  -n <my-namespace>

# Get pod info	
kubectl describe pod -n <my-namespace>

# Get all services	
kubectl get service --all-namespaces

# Get resources with json output
kubectl get pods --all-namespaces -o json

# Start a temporary pod for testing
kubectl run --rm -i -t --image=alpine test-$RANDOM -- sh

# Watch pods	
kubectl get pods -n <my-namespace> --watch

# Get pods sorted by restart count	
kubectl get pods –sort-by=’.status.containerStatuses[0].restartCount’

# List pods and images	
kubectl get pods -o=’custom-columns=PODS:.metadata.name,Images:.spec.containers[*].image’

# Get pod hpa info
kubectl describe hpa -n <my-namespace>

# Get node resource usage	
kubectl top node

# Get pod resource usage	
kubectl top pod

# Get resource usage for a given pod	
kubectl top -n <my-namespace> <podname> --containers

# Delete pod by force	
kubectl delete <pod-name> -n <my-namespace> --grace-period=0 --force

# Delete resources under a namespace	
kubectl -n my-ns delete po,svc --all

# Delete persist volumes
kubectl delete pvc -n <my-namespace> 


```

## docker

```bash
# kill all running containers
docker kill $(docker ps -q)

# delete all stopped containers 
docker rm $(docker ps -a -q)

# delete all images
docker rmi $(docker images -q)
```

## Git
* Workflow

```bash
- Git stash (if any local changes made).
- Create new branch / checkout  checkout -b JIRA-XXX-comment
- Pull rebase
- Git stash pop
- git status
- Git add
- git commit -am "JIRA-XXX-comment"
- git push origin JIRA-XXX-comment
- Create new pull request for it.
- Merge if accepted :)

```

* Combining the commits, To squash the last 2 commits into one:


```bash
- git reset --soft HEAD~2
- git commit -m "New message for the combined commit"

```

```bash
# Pushing the squashed commit, If the commits have been pushed to the remote:
git push origin +name-of-branch
# The plus sign forces the remote branch to accept your rewritten history, otherwise, you will end up with divergent branches
# If the commits have NOT yet been pushed to the remote:
git push origin name-of-branch
```


* If you are reusing a branch which current behind master: 

```bash

git fetch && git rebase origin/master OR git pull --rebase origin master

To avoid fast forward 
git push --force-with-lease
```