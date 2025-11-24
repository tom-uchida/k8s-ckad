# 7-CronJob

## Question

Create a cronjob called dice that runs every one minute.
Use the Pod template located at /root/throw-a-dice.
The image throw-dice randomly returns a value between 1 and 6.
The result of 6 is considered success and all others are failure.

The job should be non-parallel and complete the task once. Use a backoffLimit of 25.

If the task is not completed within 20 seconds the job should fail and pods should be terminated.

You don't have to wait for the job completion.
As long as the cronjob has been created as per the requirements.

## Answer

```bash
cat throw-a-dice/throw-a-dice.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: throw-dice-pod
spec:
  containers:
  -  image: kodekloud/throw-dice
     name: throw-dice
  restartPolicy: Never

k create cj dice --image=kodekloud/throw-dice --schedule="*/1 * * * *" --dry-run=client -o yaml > dice.yaml

vi dice.yaml 

k apply -f dice.yaml 
cronjob.batch/dice created

k get cj
NAME   SCHEDULE      TIMEZONE   SUSPEND   ACTIVE   LAST SCHEDULE   AGE
dice   */1 * * * *   <none>     False     0        14s             4m54s
```
