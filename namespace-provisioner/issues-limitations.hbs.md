# Known limitations and issues in Namespace Provisioner

This topic tells you about the known issues and limitations for Namespace Provisioner in
Tanzu Application Platform (commonly known as TAP).

- If you are using a GitOps repository to manage the list of namespaces, all the namespaces in the
list must exist in the cluster. The provisioner application fails to reconcile if the namespaces do
not exist on the cluster.

- To use different private repositories, the secret used for each entry must be a unique name, for
example, `gitops_install`, or `additional_sources`. Reusing the same secret is not supported due to a
limitation in kapp-controller.

    **Note** This limitation is resolved in [Tanzu Cluster Essentials v1.6.0](https://docs.vmware.com/en/Cluster-Essentials-for-VMware-Tanzu/1.6/cluster-essentials/release-notes.html#v160-2) and later.

- Before performing any operations, such as uninstalling the Namespace Provisioner or changing
from Controller mode to GitOps mode, ensure that you edit the namespaces managed by the
Namespace Provisioner in the `namespace-provisioner.apps.tanzu.vmware.com/finalizer` finalizer.
Either remove the label used to set the namespaces as managed or edit the namespace manifest and
remove the finalizer entry. For more information, see
[Manage a list of developer namespaces](provision-developer-ns.hbs.md).
