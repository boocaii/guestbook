node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"
    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    values = readYaml('./guestbook/values.yaml')

    echo values
    
    version = tag

    registryHost = "hub.yuansuan.cn/xx"

    stage "Build"

        sh "docker build -t ${registryHost}/gb-frontend:${version} -f php-redis/Dockerfile php-redis"
        sh "docker build -t ${registryHost}/gb-redisslave:${version} -f redis-slave/Dockerfile redis-slave"

    stage "Push"

        sh "docker push ${registryHost}/gb-frontend:${version}"
        sh "docker push ${registryHost}/gb-redisslave:${version}"

    stage "Deploy"

        // kubernetesDeploy configs: "applications/${appName}/k8s/*.yaml", kubeconfigId: 'kenzan_kubeconfig'
        sh "kubectl apply -f guestbook-all-in-one.yaml"

}

