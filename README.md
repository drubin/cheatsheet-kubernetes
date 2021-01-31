My cheatshet and command line guide.

Start env use a clean bash env to practise

```sh
docker run --name=ubuntu --rm -d ubuntu tail -f /dev/null
docker exec -it ubuntu /bin/bas
docker kill ubuntu
```

```sh
#install kubectl 
apt-get update && apt-get install -y apt-transport-https gnupg2 curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
apt-get update
apt install -y kubectl
# bash completion
apt install bash-completion
apt install vim
apt install tmux
```


```sh
# might need on docker
source /etc/bash_completion
# enable code completion
source <(kubectl completion bash)
# enable code completion with alias k
complete -F __start_kubectl k
alias k="kubectl "

# get alias
alias kgd="k get deploy "
alias kgp="k get pods "
alias kgn="k get nodes "
alias kgs="k get svc "
alias kcf='kubectl create -f'
alias kaf='kubectl apply -f'
alias kctx="k use-context production"
alias kns="k config set-context --current --namespace="
# Updates namespace in context but doesn't use it
#  k config set-context production --namespace=david



# List all API resources
kubectl api-resources

# List API versions
kubectl api-versions

kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > mypod.yaml 
kubectl apply -f mypod.yaml

# Check environment variables in a Pod
kubectl exec <pod> -- env
kubectl exec -it ubuntu -- ls -l /etc/hosts
kubectl explain deploy.spec
kubectl explain pod --recursive

kubectl get <resource> --sort-by=.metadata.name

kubectl run nginx --image=nginx --restart=Never --dry-run=client -o yaml
kubectl run nginx --image=nginx --restart=Never --limits='cpu=300m,memory=512Mi' --dry-run=client -o yaml
kubectl run nginx --image=nginx --restart=Never --limits='cpu=300m,memory=512Mi' --dry-run=client -o yaml


k create cm config --from-literal=foo=lala --from-literal=foo2=lolo
echo -e "foo3=lili\nfoo4=lele" > config.txt
k create cm configmap2 --from-file=config.txt

k create secret generic mysecret --from-literal=password=mypass
echo -n admin > username
k create secret generic mysecret2 --from-file=username


k label po nginx1 app=v1
k label po nginx1 app=v2 --overwrite 
# remove label
k label po nginx1 app-
k annotate po description='my description'

k scale deploy nginx --replicas=5
k rollout status deploy nginx
k set image deploy nginx nginx=nginx:1.7.9
k rollout history deploy nginx
k rollout undo deploy nginx --to-revision=2
k autoscale deploy nginx --min=5 --max=10 --cpu-percent=80

k create job pi  --image=perl -- perl -Mbignum=bpi -wle 'print bpi(2000)'
k create job busybox --image=busybox -- /bin/sh -c 'echo hello;sleep 30;echo world'

# job.spec.activeDeadlineSeconds=30
# job.spec.completions=5
# job.spec.parallelism=5

k logs pods -c container | grep WARN > txt
k delete po busybox --force --grace-period=0
kubectl top nodes

# 
k expose po nginx --name=nginx-service --port=80 --target-port=8000 --type=NodePort

# https://kubernetes.io/docs/concepts/services-networking/network-policies/
# https://kubernetes.io/docs/tasks/configure-pod-container/configure-volume-storage/ 
# https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/ 
```

vim examples / rc files

```sh

```

```
'dG' - Deletes contents from cursor to end of file. This is very useful when editing YAML files.
'ZZ' - Save and exit quickly.
```

Tmux cheat sheet

```yaml
# Note:- (= prefix ctrl +b)

# Display help not inredibly useful
prefix + ?

#vertical split
prefix + %

# Horizontal split 
prefix + "

# To navigate between pane use
prefix + arrow-keys

# to exit a pan 
ctrl + d 
# To make pane full size just hit 
prefix + z

# To toggle between different pane
prefix + o

# Also to display clock in pane hit 
prefix + t


Ctrl+b c Create a new window (with shell)
Ctrl+b w Choose window from a list
Ctrl+b 0 Switch to window 0 (by number )
Ctrl+b , Rename the current window
Ctrl+b % Split current pane horizontally into two panes
Ctrl+b " Split current pane vertically into two panes
Ctrl+b o Go to the next pane
Ctrl+b ; Toggle between the current and previous pane
Ctrl+b x Close the current pane
```

 Tmux useful comands
```sh
# List running tmux sessions
tmux ls

# start a new tmux session
tmux new -s david

# attach to sessions
tmux a -t 0

```