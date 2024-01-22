# CKA

## Learning Path:

Read the book `Certified Kubernetes Administrator (CKA) Study Guide`.

Take a strong leg on practice!

1. do 17 exercises in ./cka-crash-course/exercises
2. do practice exam https://killer.sh/ (included in exam purchase)

## Seting up k3d in devcontainer

```bash
k3d cluster create
```

## New commands

```bash
kubectl expose ... --name=super-store-service


openssl x509  -noout -text -in /etc/kubernetes/pki/apiserver.crt | grep Validity -A2


find /etc/cni/net.d/ ->
4: Weave, /etc/cni/net.d/10-weave.conflist


    command: ["sh", "-c", "while true; do date >> /vol/date.log; sleep 1; done"]


      affinity:                                             # add
        podAntiAffinity:                                    # add
          requiredDuringSchedulingIgnoredDuringExecution:   # add
          - labelSelector:                                  # add
              matchExpressions:                             # add
              - key: id                                     # add
                operator: In                                # add
                values:                                     # add
                - very-important                            # add
            topologyKey: kubernetes.io/hostname             # add


        resources:
          requests:                                 # add
            cpu: 10m                                # add
            memory: 10Mi                            # add
      tolerations:                                  # add
      - effect: NoSchedule                          # add
        key: node-role.kubernetes.io/control-plane  # add


root@cluster1-controlplane1:~# cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep range
    - --service-cluster-ip-range=10.96.0.0/12


To change IP range of service CIDR, you need to change the kube-apiserver.yaml file on the control plane node. The file is located at /etc/kubernetes/manifests/kube-apiserver.yaml. You need to change the --service-cluster-ip-range parameter to the new range. After that, you need change the settings in kube-scheduler and restart it.


k api-resources --namespaced -o name > /opt/course/16/resources.txt


k -n project-c14 get role --no-headers | wc -l


crictl ps
crictl logs


nano /etc/systemd/system/kubelet.service.d/10-kubeadm.conf


kubeadm token create --print-join-command


curl -k https://kubernetes.default/api/v1/secrets
CACERT=/var/run/secrets/kubernetes.io/serviceaccount/ca.crt
curl --cacert ${CACERT} https://kubernetes.default/api/v1/secrets -H "Authorization: Bearer ${TOKEN}"
```
