![kyverno-icon](kyverno.png)
# kyverno - k8s policy management engine

## Overview
Kyverno is a policy as code solution, that enables DevOps engineers manage policies through applying a k8s native manifests. Its main component - the admission controller - creates, mutates and validates k8s resources, by following each rule and specifications configured within a Policy.

## About Admission Controller
Admission Controller in k8s is component that takes part in each request for creating or updating resource within k8s. its responsability is to perform mutations (updates) and validations on a resource that's being requested. In addition, it provides a webhook for external Admission Controllers, that will do beyond the built-in admissions functionality.

## Kyverno Admission Controller
Kyverno provides an external admission controller, extending the built-in controllers via webhooks:
- MutatingAdmissionWebhook
- ValidatingAdmissionWebhook

## How Kyverno works?
By running a dynamic admission controller, kyverno can validate or mutate a request as part of a create update or delete k8s resource flow.

![flow](howkyvernoworks.jpg)
<i>source: https://kyverno.io/docs/introduction/how-kyverno-works/ </i>

### The Flow:
* K8s Admission controller receives a request for resource creation (say, an nginx deployment)
* Kyverno intercepts the addmission webhook (as it registered to receive them)
* Kyverno webhook controller forward the request to Kyverno Engine (kind of orchestrator)
* Engine will:
  * Finds policies that match the resource (both for mutation or validation)
  * Runs mutation rule (as mutation applies first always)
  * Sends the updated resource back to the k8s API Server
  * Sends "Allow" response to the API Server to create it and restore it in etcd
* Reports Controller (if enabled) - will create a PolicyReport showing the final result if the policy applied. (PASS / FAIL / WARN / ERROR / SKIP)