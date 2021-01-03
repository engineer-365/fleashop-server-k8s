```shell

DOCKER_PASSWORD=xxxx

kubectl create secret docker-registry engineer365-deployer --docker-username=engineer365-deployer --docker-password=$DOCKER_PASSWORD  --docker-server=docker.engineer365.org:40444 --docker-email=engineer365-builder@mail.engineer365.org

kubectl get secret engineer365-deployer --output="jsonpath={.data.\.dockerconfigjson}" | base64 -d
kubectl get secrets engineer365-deployer
```
