# jenkinsk8s

1. Clone the lab repository in your cloud shell, then `cd` into that dir:

  ```shell
  $ git clone https://github.com/juliole/jenkinsk8s.git
  ...

  $ cd jenkinsk8s
  ```


## Create namespace and quota for Jenkins

Create the `jenkins` namespace:
```shell
$ kubectl create ns jenkins
```

Jenkins POD is set to use hostPath /var/jenkins. The folder need to be created as 777 or volume changed on k8s/jenkins.yaml

### Create a Jenkins Deployment and Service
Here you'll create a Deployment running a Jenkins container

First, set the password for the default Jenkins user. Edit the password in `k8s/options` with the password of your choice b


Now create the secret using `kubectl`:
```shell
$ kubectl create secret generic jenkins --from-file=k8s/options --namespace=jenkins
secret "jenkins" created
```

Additionally you will have a service that will route requests to the controller.

The Jenkins Deployment is defined in `jenkins.yaml`. Create the Deployment and confirm the pod was scheduled:

```shell
$ kubectl apply -f k8s
deployment "jenkins" created
service "jenkins-ui" created
service "jenkins-discovery" created
```
