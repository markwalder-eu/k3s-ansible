# kube-vip
    docker run --rm --name kube-vip --network host ghcr.io/kube-vip/kube-vip:v0.5.0 manifest daemonset --inCluster --taint --interface ethx --address x.x.x.x --controlplane --arp --leaderElection

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

# metallb
    https://raw.githubusercontent.com/metallb/metallb/v0.13.3/config/manifests/metallb-native.yaml

    ---
    apiVersion: metallb.io/v1beta1
    kind: IPAddressPool
    metadata:
    name: ip-address-pool-fix
    namespace: metallb-system
    spec:
    addresses:
    - x.x.x.x-y.y.y.y
    autoAssign: false
    ---
    apiVersion: metallb.io/v1beta1
    kind: IPAddressPool
    metadata:
    name: ip-address-pool-auto
    namespace: metallb-system
    spec:
    addresses:
    - x.x.x.x-y.y.y.y
    autoAssign: auto
    ---
    apiVersion: metallb.io/v1beta1
    kind: L2Advertisement
    metadata:
    name: advertisement
    namespace: metallb-system
    spec:
    ipAddressPools:
    - ip-address-pool-fix
    - ip-address-pool-auto
