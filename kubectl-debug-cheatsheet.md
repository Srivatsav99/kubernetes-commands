# Kubernetes kubectl Debug & Troubleshoot Cheat Sheet

A single-file reference for essential `kubectl` commands to debug, monitor, and troubleshoot Kubernetes clusters.

```bash
# --------------------------
# Cluster Info
# --------------------------
kubectl cluster-info               # Show master and services info
kubectl get nodes                  # List all nodes in the cluster
kubectl describe node <node-name>  # Detailed info about a node
kubectl get componentstatuses      # Check cluster components health
kubectl version --short            # Show client & server version

# --------------------------
# Namespaces
# --------------------------
kubectl get namespaces             # List all namespaces
kubectl describe namespace <namespace>  # Show details of a namespace

# --------------------------
# Pods
# --------------------------
kubectl get pods --all-namespaces          # List all pods across all namespaces
kubectl get pods -n <namespace>            # List pods in a specific namespace
kubectl describe pod <pod-name> -n <namespace>  # Detailed info about a pod
kubectl logs <pod-name> -n <namespace>     # Show logs of a pod
kubectl logs <pod-name> -c <container-name> -n <namespace>  # Logs of specific container
kubectl logs -f <pod-name> -n <namespace>  # Follow logs in real-time
kubectl exec -it <pod-name> -n <namespace> -- /bin/bash  # Start interactive shell in pod

# --------------------------
# Deployments & ReplicaSets
# --------------------------
kubectl get deployments -n <namespace>                   # List deployments
kubectl describe deployment <deployment-name> -n <namespace>  # Detailed deployment info
kubectl rollout status deployment/<deployment-name> -n <namespace>  # Check rollout status
kubectl rollout undo deployment/<deployment-name> -n <namespace>    # Rollback deployment
kubectl get rs -n <namespace>                             # List ReplicaSets

# --------------------------
# Services
# --------------------------
kubectl get svc -n <namespace>                 # List services
kubectl describe svc <service-name> -n <namespace>  # Detailed service info
kubectl get endpoints -n <namespace>          # Show service endpoints

# --------------------------
# ConfigMaps & Secrets
# --------------------------
kubectl get configmaps -n <namespace>          # List ConfigMaps
kubectl describe configmap <configmap-name> -n <namespace>  # Describe ConfigMap
kubectl get secrets -n <namespace>             # List secrets
kubectl describe secret <secret-name> -n <namespace>       # Describe a secret

# --------------------------
# Resources & Metrics
# --------------------------
kubectl top nodes                              # Show CPU/memory usage of nodes
kubectl top pods -n <namespace>               # Show CPU/memory usage of pods
kubectl get --raw "/apis/metrics.k8s.io/v1beta1/nodes"  # Raw metrics API call
kubectl get all -n <namespace>                # List all resources in namespace

# --------------------------
# Events & Troubleshooting
# --------------------------
kubectl get events -n <namespace> --sort-by=.metadata.creationTimestamp  # Recent events
kubectl get pods -n <namespace> -w          # Watch pods in real-time
kubectl get pods -l app=<app-label> -n <namespace>  # Filter pods by label
kubectl delete pod <pod-name> -n <namespace>       # Delete pod (it may restart if in deployment)
kubectl describe node <node-name>                   # Node issues
kubectl describe pod <pod-name> -n <namespace>     # Pod issues

# --------------------------
# Networking & Connectivity
# --------------------------
kubectl exec -it <pod-name> -n <namespace> -- ping <service-or-pod-ip>  # Test connectivity
kubectl exec -it <pod-name> -n <namespace> -- nslookup <service-name>   # DNS resolution test
kubectl port-forward pod/<pod-name> <local-port>:<pod-port> -n <namespace>  # Port forward
kubectl get networkpolicies -n <namespace>          # List network policies
kubectl describe networkpolicy <policy-name> -n <namespace>  # Describe network policy

# --------------------------
# Shortcuts & Misc
# --------------------------
kubectl api-resources                         # List all resource types in cluster
kubectl get pods -n <namespace> -o wide       # Get detailed pod info (IP, node, etc.)
kubectl apply -f <file.yaml>                  # Apply a manifest file
kubectl delete -f <file.yaml>                 # Delete resources from a manifest
