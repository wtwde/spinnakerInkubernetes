kubectl create  -f quick-install-spinnaker.yml

# hal-yard pod include the config file 

安装prometheus

kubectl apply   --filename https://raw.githubusercontent.com/giantswarm/kubernetes-prometheus/master/manifests-all.yaml

安装canary 

kubectl exec $(kubectl get po -n spinnaker -l "stack=halyard" -o jsonpath="{.items[0].metadata.name}") -n spinnaker -c halyard-daemon -i -t -- bash -il

    1  hal config canary enable
    2  hal config canary edit --default-metrics-store prometheus
    3  hal config canary prometheus enable
    4  hal config canary prometheus account add prom --base-url=http://10.233.44.61:9090/
        set the Spinnaker version to v1.7.0 or higher:
    5 hal config version edit --version 1.7.0

设置hal-yard pod中的config和库中的cong类似
    6  hal deploy apply


hal config canary prometheus account list
configure canary
link: https://www.spinnaker.io/guides/user/canary/config/


