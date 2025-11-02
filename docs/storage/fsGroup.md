# Reading Material

- https://kubernetes.io/blog/2020/12/14/kubernetes-release-1.20-fsgroupchangepolicy-fsgrouppolicy/
- https://kubernetes.io/blog/2022/12/23/kubernetes-12-06-fsgroup-on-mount/

The `fsGroup` setting in a `securityContext` will cause kubernetes to attempt to modify permissions on a mounted volume, so that the group of the files contained within the volume matches that of the `fsGroup` value. Apparently, only the topmost directory is checked, and anything else is recursively modified based on the result of that check. This behaviour can be influenced by the `fsGroupChangePolicy` value in the `securityContext`, but to fully deacivate this functionality, the `fsGroup` value needs to be unset.

It is also possible to modify the `fsGroupPolicy` value on the `CSIDriver`, modifying it for all volumes. Here, there is a `None` setting, that will  prevent any permission modifications for volumes using that driver. Nothing stops us from starting multiple CSI-Driver-plugins that announce support for different CSIdrivers via the `--drivername` option. But it seems like this is only possible by duplicating the csi-plugin pods with the changed option.


- https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/csi-driver-v1/#CSIDriverSpec
- https://kubernetes-csi.github.io/docs/support-fsgroup.html
- https://kubernetes-csi.github.io/docs/support-fsgroup.html#supported-modes
