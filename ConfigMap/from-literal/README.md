# from-literal

```bash
k create cm exam-config-map --from-literal=EXAM_CODE=CKAD
configmap/exam-config-map created

k get cm
NAME               DATA   AGE
exam-config-map    1      3s

k run exam --image=busybox $do --command -- sh -c "echo \$EXAM_CODE > /etc/examcode.txt; sleep 3600;" > exam.yaml

vi exam.yaml 
k apply -f exam.yaml
```
