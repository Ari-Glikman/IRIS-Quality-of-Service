# IRIS Quality of Service

The purpose of this repo is to show how to upgrade your IRIS deployment from Burstable QoS to Guaranteed QoS.

Note the additions in Guaranteed.yaml (Guaranteed QoS) and compare to vanillaIRIS.yaml (Burstable QoS).

For an example with sidecars see GuaranteedMirrored.yaml.

Per [Kubernetes Docs](https://kubernetes.io/docs/concepts/workloads/pods/pod-qos/) on QoS:
For a Pod to be given a QoS class of Guaranteed:

   * Every Container in the Pod must have a memory limit and a memory request.
   * For every Container in the Pod, the memory limit must equal the memory request.
   * Every Container in the Pod must have a CPU limit and a CPU request.
   * For every Container in the Pod, the CPU limit must equal the CPU request.

Note that this includes initContainers and sidecars. Assuming we deploy with *useIrisFsGroup: false* in IKO values.yaml this means that initContainers will be present.

Hence we must set their limits & requests for both memory & cpu.

You can confirm your QoS Class on the pod of your choice with the following:

*kubectl describe pod <pod name<pod name>> -n <namespace<namespace>>*

and towards the bottom note:

QoS Class: {BestEffort|Burstable|Guaranteed}

