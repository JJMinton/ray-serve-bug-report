```bash
export DOCKER_NAME = minimal-example

#build and push the image
docker build -f cluster/Dockerfile -t ${DOCKER_NAME} .
docker push ${DOCKER_NAME}:latest

# TODO: set docker sha that pushed to dockerhub
export DOCKER_SHA = 

# Check ray versions between image and manifest
docker run --rm ${DOCKER_NAME} ray--version
docker run --rm ${DOCKER_NAME} conda run -n minimal-example ray--version
grep rayVersion cluster/manifest.yaml

# Deploy cluster
kubectl apply -f cluster/manifest.yaml
kubectl describe rayservice minimal-ray-example
# TODO set the name of the head pod from the resulting logs
export HEAD_POD = 

# Get logs from the cluster
kubectl exec -it ${HEAD_POD} -n brepdirectgen -- cat /tmp/ray/session_latest/logs/runtime_env_agent.log
```


