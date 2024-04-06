# Concert-Ticket-System

Concert-Ticket-System is a demo project to illustrate the performance boost by sending concurrent API requests to microservices in HA architecture

## Deployment Flow

1. Use the Minikube [minikube](https://minikube.sigs.k8s.io/docs/start/) to install kubernetes cluster locally.

2. For Docker Desktop user, enable ingress addon.
```bash
minikube addons enable ingress
```

3. Navigate to ticket-process directory (https://github.com/johnnyn2/ticket-process). Build ticket-process image
```bash
docker build -t johnnyhohohohohoho/ticket-process .
```

4. Push to Docker registry
```bash
docker push johnnyhohohohohoho/ticket-process
```

5. Nvigate to ticket-system directory (https://github.com/johnnyn2/ticket-system). Build ticket-system image
```bash
docker build -t johnnyhohohohohoho/ticket-system .
```

6. Push to Docker registry
```bash
docker push johnnyhohohohohoho/ticket-system
```

7. Start K8s cluster
```bash
minikube start
```

8. Navigate to ticket-deployment directory (https://github.com/johnnyn2/ticket-deployment). Deploy to k8s cluster.
```bash
kubectl apply -f k8s.yml
```

9. Check deployment status
```bash
kubectl get all
```

10. For Docker Desktop user to get the ingress to work, run ``` minikube tunnel ```

11. Invoke sample API in Postman
```bash
POST http://localhost/ticket-pc/concurrent/purchase
{
    "accountNo": "abc",
    "seatDTO": [
        {
            "concertCode": "abc",
            "sessionCode": "abc",
            "stage": "A",
            "seatNo": 5
        }
    ],
    "concertCode": "abc",
    "sessionCode": "abc"
}
```

12. Get pod name
```bash
kubectl get pods
```

13. Verify pod log for the sample API traffic
```bash
kubectl logs {POD_NAME}
```
