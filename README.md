# Flowise Deployment Project

This project contains configurations for deploying Flowise using both Docker and Kubernetes. Flowise is an open-source UI visual tool for building LLM apps.

## Project Structure

The project is organized into two main deployment methods:

1. Docker Deployment (`flowise-docker/`)
2. Kubernetes Deployment (`flowise-k8s/`)

### Docker Deployment

The Docker deployment uses Docker Compose to set up Flowise and its dependencies. Key files include:

- `docker-compose.yml`: Defines the Flowise and PostgreSQL services.
- `proxy/`: Contains configurations for an Nginx reverse proxy.

### Kubernetes Deployment

The Kubernetes deployment is organized into several subdirectories:

- `deployments/`: Contains Kubernetes Deployment manifests for Flowise and PostgreSQL.
- `services/`: Defines ClusterIP services for Flowise and PostgreSQL.
- `ingress/`: Includes an Ingress resource for external access to Flowise.
- `secrets/`: Contains Kubernetes Secrets for sensitive information.
- `storage/`: Defines PersistentVolumes and PersistentVolumeClaims for data persistence.
- `autoscaling/`: Includes a HorizontalPodAutoscaler for Flowise.

## Technical Details

### Docker Deployment

- Uses the official Flowise Docker image: `flowiseai/flowise:latest`
- PostgreSQL 13 is used as the database
- Environment variables are used for configuration
- Data persistence is achieved through Docker volumes
- Nginx reverse proxy is set up for SSL termination and routing

### Kubernetes Deployment

- Flowise is deployed with 3 replicas for high availability
- PostgreSQL is deployed as a single instance (consider using a managed database service for production)
- Ingress is configured with Nginx Ingress Controller
- TLS is enabled for secure communication
- Horizontal Pod Autoscaler is set up to scale Flowise based on CPU utilization
- PersistentVolumes and PersistentVolumeClaims are used for data persistence
- Kubernetes Secrets are used to manage sensitive information

## Getting Started

### Docker Deployment

1. Navigate to the `flowise-docker/` directory
2. Copy the `.env.example` file to `.env` and fill in the required variables
3. Run `docker-compose up -d` to start the services

### Kubernetes Deployment

1. Navigate to the `flowise-k8s/` directory
2. Apply the Kubernetes manifests in the following order:
   ```
   kubectl apply -f secrets/
   kubectl apply -f storage/
   kubectl apply -f deployments/
   kubectl apply -f services/
   kubectl apply -f ingress/
   kubectl apply -f autoscaling/
   ```

## Security Considerations

- Always use strong, unique passwords for database and API access
- Keep your Kubernetes Secrets and environment variables secure
- Regularly update the Flowise image and all dependencies
- Use network policies to restrict communication between pods
- Implement proper access controls and authentication mechanisms

## Monitoring and Logging

- Consider setting up Prometheus and Grafana for monitoring
- Use Kubernetes' built-in logging capabilities or implement a centralized logging solution

## Backup and Disaster Recovery

- Regularly backup the PostgreSQL database
- Implement a disaster recovery plan for both Docker and Kubernetes deployments

## Contributing

Contributions to improve the deployment configurations or documentation are welcome. Please submit a pull request or open an issue for any enhancements.

## License

This project is open-source and available under the [MIT License](LICENSE).
