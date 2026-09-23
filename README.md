# Cloud-Native-E-Commerce-Platform
A secure, cloud-native microservice for a E commerce platform developed for SE4010 (Current Trends in Software Engineering). Implements Docker containerization, CI/CD pipelines, DevSecOps practices, and cloud deployment using managed container services.

## 🚀 CI/CD Pipeline

### DeliveryManagementService Deployment

The DeliveryManagementService has an automated CI/CD pipeline that deploys to AWS ECS Fargate.

#### Setup GitHub Secrets

Before using the pipeline, you need to configure these secrets in your GitHub repository:

1. Go to your repository → Settings → Secrets and variables → Actions
2. Add the following secrets:
   - `AWS_ACCESS_KEY_ID`: Your AWS access key ID
   - `AWS_SECRET_ACCESS_KEY`: Your AWS secret access key

#### How it works

The pipeline (`.github/workflows/deploy-delivery-service.yml`) automatically:
- Triggers on pushes to `main` or `DeliveryManagementService` branches
- Only runs when files in `DeliveryManagementService/` directory change
- Builds Docker image and pushes to Amazon ECR
- Updates ECS service with new image
- Waits for service stability

#### Manual Deployment

You can also trigger the pipeline manually:
1. Go to Actions tab in GitHub
2. Select "Deploy DeliveryManagementService to AWS ECS"
3. Click "Run workflow"

#### Current AWS Resources

- **Region**: eu-north-1 (Stockholm)
- **ECS Cluster**: chaveenn
- **ECS Service**: delivery-service
- **ECR Repository**: delivery-service
- **Task Definition**: delivery-service-task

## Local Development

Install dependencies in each service once, then run the services in separate terminals:

```bash
cd UserAuthenticationService && npm run dev
cd ShopManagementService && npm run dev
cd OrderManagementService && npm run dev
cd DeliveryManagementService && npm run dev
cd NotificationService && npm run dev
cd Frontend && npm run dev
```

The Vite frontend runs at `http://localhost:5173`. The local backend ports are user/auth `5002`, shop `4040`, order `4000`, delivery `5003`, and notification `5000`.

The backend `.env` files contain the local MongoDB and RabbitMQ settings. Start RabbitMQ locally when using order events, or run the `rabbitmq` service with `docker compose up rabbitmq`.
