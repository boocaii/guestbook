# Example: Guestbook application on Kubernetes with Jenkins and Helm

This directory contains the source code and Kubernetes/Helm manifests for PHP Guestbook application.

The `build`, `push`, `deploy` phases are listed in `Jenkinsfile`.

To publish and deploy a new version, 

1. modify the source code or Helm manifests 
2. change the `version` field in `guestbook/Chart.yaml` to a new one, like 0.3.1 to 0.3.2
3. then commit and push this commit to the upstream

The Jenkins server will be triggered periodically (or by hooks), to execute the `Jenkinsfile`.