#Learn conventions from here

https://kubernetes.io/docs/reference/kubectl/conventions/
https://devblogs.microsoft.com/premier-developer/certified-kubernetes-application-developer-ckad-exam-tips/
https://kubernetes.io/docs/reference/kubectl/cheatsheet/
https://medium.com/@harioverhere/ckad-certified-kubernetes-application-developer-my-journey-3afb0901014

export KUBE_EDITOR=nano

alias k=kubectl
source <(kubectl completion bash)
source <(kubectl completion bash | sed 's/kubectl/k/g' )

while true; do date; sleep $TIME_FREQ;done

kubectl config set-context --current --namespace=default
kubectl explain pods --recursive | less
kubectl delete -f busybox.yaml

https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad
https://gist.github.com/veggiemonk/70d95df77029b3ebe58637d89ef83b6b
https://github.com/dgkanatsios/CKAD-exercises/blob/master/f.services.md