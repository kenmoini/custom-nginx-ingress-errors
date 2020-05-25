# custom-nginx-ingress-errors
Assets to build a container to provide a custom default backend to the nginx-ingress Kubernetes Ingress controller

![404 Screenshot](https://github.com/kenmoini/simple-static-default-backend/raw/master/404-screenshot.png)

## Editing Error Pages

The container has a set of error HTML and JSON files that are returned based on the error code.  These files are stored in the `www/` directory and are copied to the `/www/` directory in the container.

1. Fork this repo, modify the error pages as you see fit.
2. Connect to Docker Hub/Quay.io to build an image you have access to.
3. Modify the `k8s-deployment.yaml` file to point to your custom built image.

## Deploying a custom default-backend for Nginx Ingress

***Note:*** This is for the Kubernetes Nginx Ingress, not the one made by Nginx.
If you haven't deployed it yet, here ya go: https://kubernetes.github.io/ingress-nginx/deploy/

These instructions assume that you deployed this in the default `ingress-nginx` namespace.

1. Modify the `k8s-deployment.yaml` file to point to your custom built image, or use it as is for some snazzy error pages
2. Deploy to the Kubernetes cluster: `kubectl apply -f k8s-deployment.yaml`
3. Modify the `ingress-nginx/ingress-nginx-controller` Deployment and set the value of the `--default-backend-service` flag to the name of the newly created error backend, which should be `ingress-nginx/nginx-errors` by default.
4. Edit the `ingress-nginx/nginx-configuration` ConfigMap  and add the key:value pair of `"custom-http-errors": "404,500,503"`
5. ??????
6. PROFIT!!!!1
