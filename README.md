## Kubernetes plugin instruction
`kubeplugin` could be run either as script or as Kubernetes plugin

### Singleton script
Before running ensure that `kubeplugin` file is executable. Or just run

```bash
sudo chmod +x ./scripts/kubeplugin
./scripts/kubeplugin pod kube-system
```
Script is written for two types of K8s resources. Either `pod` or `node`

Example of response
```
Resource: pod
Namespace: kube-system
Name: coredns-597584b69b-7qtbb
CPU: 6m
Memory: 26Mi

Resource: pod
Namespace: kube-system
Name: local-path-provisioner-79f67d76f8-677d6
CPU: 1m
Memory: 17Mi

Resource: pod
Namespace: kube-system
Name: metrics-server-5f9f776df5-gxq9k
CPU: 11m
Memory: 30Mi

Resource: pod
Namespace: kube-system
Name: svclb-traefik-ee299a72-kcqxd
CPU: 0m
Memory: 0Mi

Resource: pod
Namespace: kube-system
Name: traefik-66c46d954f-pfkrz
CPU: 1m
Memory: 42Mi
```

### `kubectl` plugin
Official documentation how to extend kubectl with plugins you can find
[here](https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/)

Create a folder for your `kubectl` plugins 
```bash
mkdir ~/kubectl_plugins
 ```

Edit `.bashrc` in your home directory and add the following line
```
export PATH="~/kubectl_plugins:$PATH"
```

Source your `.bashrc` file or restart the terminal
```bash
source ~/.bashrc
```

Copy the script into the plugins folder and prefix plugin name with `kubectl-`
```bash
cp ./scripts/kubeplugin ~/kubectl_plugins/kubectl-info
```

Make all plugins executable
```bash
sudo chmod +x ~/kubectl_plugins/*
```

Ensure that the plugin is in the list
```bash
kubectl plugin list
```

Run the plugin
```bash
kubectl info pod kube-system
```
