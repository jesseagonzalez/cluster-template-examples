# rke2 cluster template

Helm chart that can be used as rke2 cluster template

### how to deploy standalone instance

```bash
# generate random id to build multiple clusters for testing
export INSTANCE_PREFIX=rke2-vsphere-helm-standalone-${RANDOM}

helm upgrade --install ${INSTANCE_PREFIX} ./charts \
  --namespace fleet-default \
  --values ./charts/values-vsphere-standalone.yaml \
  --set cluster.name=${INSTANCE_PREFIX} \
  --set nodepools[0].name=${INSTANCE_PREFIX}-standalone \
  --set nodepools[0].quantity=1
  # --debug --dry-run
```

### how to deploy multi-node instance

```bash
# generate random id to build multiple clusters for testing
export INSTANCE_PREFIX=rke2-vsphere-helm-multi-${RANDOM}

helm upgrade --install ${INSTANCE_PREFIX} ./charts \
  --namespace fleet-default \
  --values ./charts/values-vsphere-multi.yaml \
  --set cluster.name=${INSTANCE_PREFIX} \
  --set nodepools[0].name=${INSTANCE_PREFIX}-server \
  --set nodepools[0].quantity=1 \
  --set nodepools[1].name=${INSTANCE_PREFIX}-agent \
  --set nodepools[1].quantity=1
  # --debug --dry-run
```

### how to scale cluster

helm get values > increase quantity

```bash
# generate random id to build multiple clusters for testing
# generate random id to build multiple clusters for testing
export INSTANCE_PREFIX=rke2-vsphere-helm-demo-${RANDOM}

helm upgrade --install ${INSTANCE_PREFIX} ./charts \
  --namespace fleet-default \
  --values ./charts/values-vsphere-multi.yaml \
  --set cluster.name=${INSTANCE_PREFIX} \
  --set nodepools[0].name=${INSTANCE_PREFIX}-server \
  --set nodepools[0].quantity=2 \
  --set nodepools[1].name=${INSTANCE_PREFIX}-agent \
  --set nodepools[1].quantity=1
  # --debug --dry-run
```

General cluster options are available through [values.yaml](./values.yaml)

For different cloud provider drivers:

[Amazonec2](./values-aws.yaml)

[Vsphere](./values-vsphere.yaml)

[Digitalocean](./values-do.yaml)

[Azure](./values-azure.yaml)