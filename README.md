# Restrict-the-pod-to-pod-communication-in-the-EKS

#### Network Policies
* Within a Kubernetes cluster, all Pod to Pod communication is allowed by default. This may cause a major impact if one of the pods gets compromised, all other pods within the namespace can also be compromised since it is allowed to communicate [Refer here](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

#### How to restrict Inter Pod communication ?
* The solution is to use ‘Network Policies’. Networkpolicies can be used to restrict network traffic between pods and enforce security policies.
* To restrict pod-to-pod communication in Kubernetes, you can utilize Network Policies. Network Policies allow you to define rules that control traffic between pods within your Kubernetes cluster.

    1. Enable Network Policy support.
    2. Define Network Policies.
    3. Apply the Network Policies.

### Here's a step-by-step guide:
* Step 1: Enable Network Policy support (if not already enabled):
    * Ensure that your Kubernetes cluster networking solution supports Network Policies. If you're using a managed Kubernetes service like GKE (Google Kubernetes Engine), EKS (Amazon Elastic Kubernetes Service), or AKS (Azure Kubernetes Service), check their documentation for instructions on enabling Network Policies.
        * AWS EKS(Amazon Elastic Kubernetes Service) [Refer here](https://docs.aws.amazon.com/eks/latest/userguide/cni-network-policy.html).
        * AKS (Azure Kubernetes Service) [Refer here](https://learn.microsoft.com/en-us/azure/aks/use-network-policies).
        * GKE (Google Kubernetes Engine) [Refer here](https://cloud.google.com/kubernetes-engine/docs/how-to/network-policy).

* Step 2: Define Network Policies:
    * Create Network Policy YAML files to define the communication rules. Here's an example of a Network Policy that denies all traffic to pods with the label `role: backend`:
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata: 
name: anchan-deny-all
 namespace: anchan
spec: 
podSelector: {} # Applicable to all the pods in the namespace 
policyTypes:
 — Ingress # Incoming Traffic 
- Egress # outgoing traffic
```
* **The above manifest would block all the traffic within the cluster.**

* Step 3: Apply the Network Policies
    * Apply the Network Policy to your Kubernetes cluster using the kubectl apply command: `kubectl apply -f <your-network-policy.yaml>`
