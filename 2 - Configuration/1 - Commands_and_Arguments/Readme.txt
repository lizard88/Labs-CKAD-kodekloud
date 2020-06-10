apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper-3
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command:
      - sleep
      - "1200"

FROM python:3.6-alpine
RUN pip install flask
COPY . /opt/
EXPOSE 8080
WORKDIR /opt
ENTRYPOINT ["python", "app.py"]
CMD ["--color", "red"]

apiVersion: v1
kind: Pod
metadata:
  name: webapp-green
  labels:
      name: webapp-green
spec:
  containers:
  - name: simple-webapp
    image: kodekloud/webapp-color
    command: ["python", "app.py"]
    args: ["--color", "pink"]



Create a pod with the given specifications. By default it displays a 'blue' background. Set the given command line arguments to change it to 'green'

Pod Name: webapp-green
Image: kodekloud/webapp-color
Command line arguments: --color=green

$ kubectl run webapp-green --image kodekloud/webapp-color --generator=run-pod/v1 --dry-run -o yaml > pod.yaml