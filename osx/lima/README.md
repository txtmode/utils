# Lima usage examples
# Docker
Create the default docker instance with:
```
brew install lima
limactl create --name=default docker.yaml
docker context create --docker host=unix://$HOME/.lima/default/sock/docker.sock lima
docker context use lima
```
## Kubernetes
Create a Kubernetes instance with:
```
limactl create --name=k3s k3s.yaml
```
If you don't have any existing Kubernetes config file, copy the generated config to `$HOME/.kube/config`.
If you do, merge both configs into one:
```
mv $HOME/.kube/config $HOME/.kube/config-old
KUBECONFIG=$HOME/.kube/config-old:$HOME/.lima/k3s/copied-from-guest/kubeconfig.yaml kubectl config view --flatten > $HOME/.kube/config
kubectl config use-context lima
```
