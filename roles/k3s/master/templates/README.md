# kube-vip
    docker run --rm --name kube-vip --network host ghcr.io/kube-vip/kube-vip:v0.5.7 manifest daemonset --inCluster --taint --interface ethx --address x.x.x.x --controlplane --bgp  --localAS y --peerAS z --peerAddress u.u.u.u --leaderElection --servicesElection

    add manually 
    - name: bgp_routerinterface
      value: ethx

    https://raw.githubusercontent.com/kube-vip/kube-vip/v0.5.0/docs/manifests/rbac.yaml

    ---
    kind: ClusterRoleBinding
    apiVersion: rbac.authorization.k8s.io/v1
    metadata:
    name: system:kube-vip-cluster-admin-binding
    roleRef:
    apiGroup: rbac.authorization.k8s.io
    kind: ClusterRole
    name: cluster-admin
    subjects:
    - kind: ServiceAccount
    name: kube-vip
    namespace: kube-system

    https://raw.githubusercontent.com/kube-vip/kube-vip-cloud-provider/main/manifest/kube-vip-cloud-controller.yaml
