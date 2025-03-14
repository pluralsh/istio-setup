# Istio Setup
Setup manual for Istio in Ambient mode.

1. Use `kubectl get crd gateways.gateway.networking.k8s.io` to check if Gateway API CRDs are deployed on the cluster and if it is not the case then use manifests from `gateway-api.yaml` to deploy them.
2. Deploy Istio using manifests from `istio.yaml`.
3. Deploy sample app using manifests from `sample-app.yaml`.
4. Use `kubectl port-forward -n istio-sample-app svc/bookinfo-gateway-istio 8080:80` and then navigate to http://localhost:8080/productpage to access the sample app. If you refresh the page, you should see the display of the book ratings changing as the requests are distributed across the different versions of the reviews service.

> [!IMPORTANT]  
> To make Istio work on EKS cluster is it needed to add a rule for port 15017 between the primary cluster security group and the node security group.
>
> See: https://github.com/istio/istio/issues/46746.

> [!NOTE]  
> `name: ztunnel` can be removed from `istio-ztunnel` service deployment in `istio.yaml` once https://github.com/istio/istio/pull/55360 will be released.
