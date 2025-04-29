# CustomResourceDefinition

```bash
vi vehicle-crd.yaml

k apply -f vehicle-crd.yaml 
customresourcedefinition.apiextensions.k8s.io/vehicles.stable.example.com created

vi my-new-car.yaml

k apply -f my-new-car.yaml 
vehicle.stable.example.com/my-new-car created

k describe vc my-new-car 
Name:         my-new-car
Namespace:    default
Labels:       <none>
Annotations:  <none>
API Version:  stable.example.com/v1
Kind:         Vehicle
Metadata:
  Creation Timestamp:  2025-04-29T13:36:21Z
  Generation:          1
  Resource Version:    5821
  UID:                 f6f531ae-c8c7-46a5-b1db-4f85722e53f6
Spec:
  Color:         red
  Vehicle Type:  car
Events:          <none>
```
