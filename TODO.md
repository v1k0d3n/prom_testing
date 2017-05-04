# TODO LIST:

* "Containerize" the Kubelet service using a model similar to "rkt-fly". Details below.

## Containerizing the Kubelet

We may want to use chroot to essentially "containerize" the Kubelet service safely. An approach that CoreOS uses is described in the following [documentation](https://coreos.com/rkt/docs/latest/running-fly-stage1.html). In this approach, the Kubelet is executed via a wrapper script (i.e. the [kubelet-wrapper](https://github.com/coreos/coreos-overlay/blob/master/app-admin/kubelet-wrapper/files/kubelet-wrapper). From an operator perspective, the `kubelet.service` can be created per usual, with the exception of calling the [kubelet-wrapper](https://github.com/kubernetes-incubator/bootkube/blob/master/hack/quickstart/kubelet.master#L15-L30) rather than the Kubelet itself. This ensures that all dependancies are included out of the box, and the only requirement for upgrading the Kubelet would be modifying the environment variable for the `[KUBELET_IMAGE_TAG](https://github.com/kubernetes-incubator/bootkube/blob/master/hack/quickstart/kubelet.master#L3)`.
