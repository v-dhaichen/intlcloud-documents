## Introduction
When creating Ingress using the HTTPS listening protocol, please choose a suitable server certificate to ensure access security. This document describes content related to the use of Ingress certificates. Certificate-related annotations are as follows:

- `kubernetes.io/ingress.http-rules`
- `kubernetes.io/ingress.https-rules`
- `kubernetes.io/ingress.rule-mix`
- `qcloud_cert_id` (Read only)

## Considerations

- `qcloud_cert_id` in Ingress annotation is read-only. It lets you quickly see the corresponding certificate ID for the current Ingress.
- The Secret certificate resource must be put in the same namespace as the Ingress resource.
- When creating the Ingress, a Secret certificate resource with name will be created automatically. If the Secret resource name already exists, the Ingress cannot be created.
- By default, the TKE Ingress will not use a Secret that is in use. However, a Secret can be used by multiple Ingresses. Note that updating a Secret will update all related Ingress certificates. 

## Directions

### Using certificates in the console

1. Log in to the CLB Console, and select [**Certificate Management**](https://console.cloud.tencent.com/clb/cert) in the left sidebar. In the **Certificate Management** page, create a certificate.
2. See [Creating an Ingress](https://intl.cloud.tencent.com/document/product/457/30673) for more information about completing the creation of an Ingress.
In this step, select **Http:443** in the listening port and select the suitable server certificate.

>
> -  When HTTPS service is enabled for an Ingress created in the console, a Secret resource with the same name will be created to store the certificate ID. Then, this Secret is used and listened to in the Ingress.
> - When you modifies a certificate in console, the certificate of the current Ingress is modified. Please note that, if there are multiple Ingresses using the same Secret, then the certificates of the CLBs corresponding to these Ingresses will be modified together.


### Kubectl guide

#### Configuring a certificate and creating an HTTPS service<span id="CreatingSecret"></span>
1. Create Secret resources
 - Base64 manual encoding. The YAML example is as follows:
```yaml
apiVersion: v1
data:
       qcloud_cert_id: XczRzegn ## Configures the certificate ID to be XczRzegn
kind: Secret
metadata:
       name: tencent-com-cert
       namespace: default
type: Opaque
```
 - Base64 automatic encoding: when creating, use `stringData` for declaration, avoiding manual Base64 encoding. The YAML example is as follows:
```yaml
apiVersion: v1
stringData:
       qcloud_cert_id: XczRzegn
kind: Secret
metadata:
       name: tencent-com-cert
       namespace: default
type: Opaque
```
2. Create an Ingress resource.
When creating an Ingress resource, specify the backend Service as `sample-service:80`, and the specify `secretName` as `tencent-com-cert`. The YAML example is as follows:
<pre>
<span class="hljs-section">apiVersion: extensions/v1beta1</span>
<span class="hljs-section">kind: Ingress</span>
<span class="hljs-section">metadata:</span>
     annotations:
       kubernetes.io/ingress.class: qcloud
       qcloud_cert_id: XczRzegn
     name: sample-ingress
     namespace: default
<span class="hljs-section">spec:</span>
     rules:
     - http:
         paths:
         - backend:
             serviceName: sample-service
             servicePort: 80
         path: /
     tls:
     - secretName: tencent-com-cert
</pre>


#### Modifying certificates

1. Execute the following command to use the default editor to open the Secret that needs to be modified.
```
kubectl edit secrets
```
This document takes the Secret in [Creating a Secret Resource](#CreatingSecret) as an example. Execute the following command:
```
kubectl edit secrets tencent-com-cert
```
2. Modify the Secret resource, and change the value of `qcloud_cert_id` to the new certificate ID.
> Similar to the creation of a Secret, modifying a Secret certificate ID requires Base64 encoding. Select Base64 manual encoding or specify `stringData` to perform Base64 automatic encoding according to your actual requirements.


#### Mixed Rule Configuration

TKE Ingress Controller supports mixed configuration of HTTP/HTTPS rules. The steps are as follows:
1. Enable mixed rules
Set `kubernetes.io/ingress.rule-mix` to True.
When the Ingress template does not have TLS configured, no certificate resources are provided. All rules are exposed as HTTP services, and the preceding annotations do not take effect.
2. Match rules
Match each rule in Ingress with `kubernetes.io/ingress.http-rules` and `kubernetes.io/ingress.https-rules`, and add them to the corresponding rule set. If the rules in Ingress are not matched, they are added to the HTTPS rule set by default.
3. Verify matches
When matching, verify the Host, Path, ServiceName, ServicePort (in these, Host is `VIP` by default, and Path is `/` by default).
Note that **IPv6**CLBs do not have the feature for providing default domain names.

#### YAML sample

Refer to the following YAML sample to enable mixed rules and to configure the backend service to be open to HTTP/HTTPS services.
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.http-rules: '[{"host":"www.tencent.com","path":"/","backend":{"serviceName":"sample-service","servicePort":"80"}}]'
    kubernetes.io/ingress.https-rules: '[{"host":"www.tencent.com","path":"/","backend":{"serviceName":"sample-service","servicePort":"80"}}]'
    kubernetes.io/ingress.rule-mix: "true"
    kubernetes.io/ingress.class: qcloud
    qcloud_cert_id: XczRzegn
  name: sample-ingress
  namespace: default
spec:
  rules:
  - host: www.tencent.com
    http:
      paths:
      - backend:
          serviceName: sample-service
          servicePort: 80
        path: /
  tls:
  - secretName: tencent-com-cert
```

## FAQs
- Can I modify `tls.secretName` in an Ingress to point to a different Secret resource?
Yes. After updating, the new certificate specified in the Secret will be quickly synchronized to the CLB corresponding to the Ingress.

- How do I obtain the certificate ID?
Log in to the CLB Console, and select **[Certificate Management](https://console.cloud.tencent.com/clb/cert)** in the left sidebar. You can obtain the ID in the **Certificate Management** page.

## Reference

For more information, see the official Kubernetes documentation [Secret](https://kubernetes.io/docs/concepts/configuration/secret/).



