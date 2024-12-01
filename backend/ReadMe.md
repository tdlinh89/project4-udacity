# Install dependencies
pipenv install

# Run the tests
pipenv run test

## Expected output
...
collected 3 items

test_app.py::test_movies_endpoint_returns_200 PASSED                                                                                              [ 33%]
test_app.py::test_movies_endpoint_returns_json PASSED                                                                                             [ 66%]
test_app.py::test_movies_endpoint_returns_valid_data PASSED  

# Running linter
pipenv run lint

# Build and run
cd starter/backend

## Install dependencies
pipenv install

## Run application
pipenv run serve

# Build docker
cd starter/backend

## Build the image
docker build --tag mp-backend:latest .

## Run the image
docker run -p 5000:5000 --name mp-backend -d mp-backend

## Check the running application
curl http://localhost:5000/movies

## Review logs
docker logs -f mp-backend

## Expected output
{"movies":[{"id":"123","title":"Top Gun: Maverick"},{"id":"456","title":"Sonic the Hedgehog"},{"id":"789","title":"A Quiet Place"}]}

## Stop the application
docker stop

# Deploy Kubernetes Manifests
cd starter/backend/k8s

/# Make sure you're kubeconfig is configured for the EKS cluster, i.e.
/# aws eks update-kubeconfig`

/# Set the image tag to the newer version
/# ℹ️ Don't commit any changes to the manifests that this command introduces

kustomize edit set image frontend=<ECR_REPO_URL>:<NEW_TAG_HERE>

/# Apply the manifests to the cluster
kustomize build | kubectl apply -f -