apiVersion: v1
kind: Pod
metadata:
  labels:
    name: webapp-color
  name: webapp-color
  namespace: default
spec:
  containers:
  - env:
    - name: APP_COLOR
      value: pink
    image: kodekloud/webapp-color
    imagePullPolicy: Always
    name: webapp-color



Update pod to use configmap

apiVersion: v1
kind: Pod
metadata:
  name: dapi-test-pod
spec:
  containers:
    - name: test-container
      image: k8s.gcr.io/busybox
      command: [ "/bin/sh", "-c", "env" ]
      envFrom:
      - configMapRef:
          name: special-config
  restartPolicy: Never

con envFrom si puo puntare ad una configmap

envFrom:
      - configMapRef:
          name: special-config