# Kubernetes kube-controller-manager

## Overview
The Kube Controller Manager, is the component responsible of implementing the core logic of the "control loop".
Whenever we want to make changes into our kuberenetes system, we need a mechanism that will "control" those changes. Meaning, move the system from the current state to the desired state.

## Responsibilities
- Monitoring </br>
  Constantly monitors the state of the system through the API Server. Tracking the current configs of resources in it.
- State Reconciliation </br>
  Compare the desired state as defined in the user request manifest with the actual state, it identified differences.
- Corrective Actions </br>
  When the controller detects deviations it perform the necessary actions to bring the system back to a non-deviative state.
  This would include: </br>
  - restart failed containers</br>
  - scale pods </br>
  - recreate resources. 

## Example 
When executing: 
`kubectl create namespace test-ns`
Namespace controller will look if this namespace already exists, if it does, it would inform us - otherwise it will inform us that this ns already exist.



