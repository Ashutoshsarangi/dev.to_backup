This article details the journey of developing and deploying an AI agent proof-of-concept (POC), highlighting the challenges encountered and the solutions implemented. My goal in sharing this experience is to assist others who may face similar hurdles when moving from local development to a containerized and orchestrated environment.

-----

### The AI Agent POC: Summarization and Error Detection

My use case involved processing logs to summarize them and identify potential errors in parallel, leveraging an AI agent. To achieve this, I utilized **LangGraph** for building the agent's workflow, incorporating **parallelization** and **subgraph concepts** with **Large Language Models (LLMs)**.

Once the core AI agent functionality was established, the next step was to expose it for external consumption. I developed a **Python server** to serve as the interface, allowing a UI to send logs and receive summarized and error-checked outputs. This Python server internally orchestrates the LangGraph-powered AI agent.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tpqa3zz6igmldsebfape.png)


-----

### Containerization with Docker

To ensure portability, scalability, and consistent environments, containerizing the Python server was essential. I decided to create a **Docker image** for the application. The ultimate goal was to deploy this image on an orchestration platform like **Kubernetes** to manage scaling and provide high availability.

While developing the LangGraph and running the local Python server was relatively straightforward, the complexity significantly increased once Docker and Kubernetes were introduced.

**Note:** For this POC, I used **Docker Desktop** and enabled its built-in Kubernetes feature, which sets up a single-node Kubernetes architecture.

#### Docker Challenges and Solutions

My initial step was to create a **Dockerfile** and build the Docker image. The first challenge arose when attempting to run the containerized application:

**1. Exposing Ports and Uvicorn Binding:**

When I initially ran the Docker container, I used the command:

```bash
docker run -d -p 8080:9000 --name my-genai-app-ashu genai-server-poc-ashu:1.8.0
```

I expected to access the application via `http://localhost:8080`. However, I observed the following log from the Docker container:

```
INFO: Uvicorn running on http://127.0.0.1:9000 (Press CTRL+C to quit)
```

This indicated that **Uvicorn**, my Python web server, was binding to `127.0.0.1` (localhost) *inside* the container. While the `docker run -p 8080:9000` command correctly mapped host port 8080 to container port 9000, Uvicorn wasn't listening for external connections on that port because it was specifically bound to localhost within the container's isolated network.

**The Solution:**

To make Uvicorn accessible from outside the container, I needed to instruct it to listen on `0.0.0.0` (all available network interfaces) inside the container. This change ensures Uvicorn accepts connections from external sources, allowing the Docker port mapping to work effectively.

The fix involved modifying the `CMD` instruction in my Dockerfile:

```dockerfile
CMD ["uvicorn", "server:app", "--host", "0.0.0.0", "--port", "9000"]
```

After this adjustment, I was successfully able to access my Dockerized application from my local machine.

`http://localhost:8080` Worked

-----

### Kubernetes Deployment and Access

With the Docker image successfully running, the next phase was to deploy it to Kubernetes. I created a **Kubernetes Deployment** and a **Service** with a single pod, which ran without issues.

The primary challenge then shifted to accessing the application running within Kubernetes from my local machine.

**Understanding Kubernetes Services:**

A **Kubernetes Service** provides a stable network endpoint for your Pods. Pods are ephemeral and their IP addresses can change frequently. A Service ensures a consistent IP and DNS name for your application within the cluster.

  * **`type: ClusterIP`**: This is the default service type, providing a stable internal IP address. Services of this type are only reachable from within the Kubernetes cluster and are typically used for inter-pod communication.
  * **Accessing from Outside the Cluster**: To access your application from your local machine or the internet, you need to change your Service type.
      * **`NodePort` (for testing/development)**: This type exposes the Service on a static port on each Node's IP address. You can then access it at `http://<NodeIP>:<NodePort>`.
      * **`LoadBalancer` (for cloud production)**: If you're on a cloud provider (e.g., GKE, EKS, AKS), changing the type to `LoadBalancer` automatically provisions an external load balancer and assigns a public IP address.

For my scenario, during development and testing, I chose to use a **`NodePort` Service**. To find the Node IP and Node Port, I used `kubectl get -o wide` and `kubectl describe services`.

#### Kubernetes Access Challenges with Docker Desktop

I encountered difficulties directly accessing `http://<NodeIP>:<NodePort>` with Docker Desktop for the following reasons:

1.  **Isolation (WSL2/Hyper-V):** Docker Desktop (on Windows and macOS) runs Kubernetes inside a lightweight virtual machine (WSL2 on Windows). The `NodeIP` obtained from `kubectl get nodes -o wide` is the IP of this virtual machine, not your host machine's IP. Direct access from your host machine to this internal VM IP often doesn't work without specific routes or port forwards configured by Docker Desktop.
2.  **NodePort Behavior in Docker Desktop:** While NodePort technically exposes the service on a port across all nodes (in this case, the single "docker-desktop" node), directly accessing `NodeIP:NodePort` from your host machine isn't as straightforward as with a cloud-based Kubernetes cluster. Docker Desktop attempts to make NodePort accessible, but it requires additional steps for reliable external access.

**The Solution: `kubectl port-forward`**

The most reliable and convenient method for temporary access and debugging within this setup is `kubectl port-forward`. This command creates a secure tunnel from your local machine to a specific Service or Pod within your Kubernetes cluster.

My previous Service definition (assuming `NodePort`):

```yaml
spec:
  ports:
    - protocol: TCP
      port: 80 # This is the service's internal cluster IP port
      targetPort: 9000 # This is the port on the pod where your app is listening
      nodePort: 30080 # Example NodePort
  type: NodePort
```

My Dockerfile clearly stated that my Uvicorn application was listening on port `9000` inside the container. The Service was configured to expose port `80` internally and map it to the Pod's `targetPort: 9000`.

The key insight for `kubectl port-forward` is that the second port number in the command must be the **Service's port**, not the Pod's `targetPort` or the `nodePort`. Kubernetes handles the routing from the Service's port to the Pod's `targetPort`.

Therefore, the correct `kubectl port-forward` command was:

```bash
kubectl port-forward service/python-app-service 7000:80
```

  * **`service/python-app-service`**: Specifies the name of the Kubernetes Service.
  * **`7000`**: This is the port on my local machine (host) that I wanted to use to access the application (e.g., `http://localhost:7000`).
  * **`80`**: This is the port on the Kubernetes Service (`python-app-service`) that the command connects to.

By using this command, I successfully established a connection to my AI agent application running within Kubernetes from my local browser.

-----

### Conclusion

This POC demonstrates the end-to-end process of building an AI agent for log summarization and error detection, deploying it as a Python server, containerizing it with Docker, and orchestrating its deployment on Kubernetes. The journey highlighted critical learning points regarding Docker port binding and effective access strategies for Kubernetes services within a Docker Desktop environment. Overcoming these challenges provided invaluable experience in building robust and scalable AI-powered applications.
