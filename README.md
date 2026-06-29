# Frontend - Tienda de Perritos

## Arquitectura y Tecnologías
* **Orquestador:** AWS EKS (Elastic Kubernetes Service).
* **Contenedores:** Imagen Docker almacenada en Amazon ECR (`tienda-frontend`).
* **Redes:** Expuesto a internet mediante un AWS Application Load Balancer (ALB).
* **Autoscaling:** Configurado con Horizontal Pod Autoscaler (HPA).

## Estructura del Repositorio
* `/frontend`: Código fuente y Dockerfile de la interfaz web.
* `/k8s`: Archivos de manifiesto YAML para el despliegue en Kubernetes (Deployment, Service, HPA).
* `.github/workflows/deploy-frontend.yml`: Pipeline de CI/CD.

## Pipeline CI/CD (GitHub Actions)
El despliegue está 100% automatizado mediante GitHub Actions. Cada vez que se realiza un `push` a la rama `main`, el pipeline ejecuta los siguientes pasos:
1. Autenticación segura con AWS mediante IAM y Secrets de GitHub.
2. Construcción (`build`) de la imagen Docker del Frontend.
3. Subida (`push`) de la imagen al repositorio de Amazon ECR.
4. Actualización del Kubeconfig y despliegue automático en el clúster EKS (`devopseks`) en el namespace `tienda`.

## Comandos para interactuar con el cluster
Para obtener la URL pública de la tienda y verificar el frontend manualmente a través de CloudShell:

**Obtener la URL de acceso (ALB):**
`kubectl get svc tienda-frontend -n tienda`

**Ver los pods activos:**
`kubectl get pods -n tienda`

**Ver el Autoscaling (HPA):**
`kubectl get hpa -n tienda`
