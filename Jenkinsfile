pipeline {
    agent any

    environment {
        dockerRepoId = "springshop/discovery"
        dockerRepoUser = credentials("docker-hub-username")
        dockerRepoPass = credentials("docker-hub-password")
    }

    // tools {
    //     // Install the Maven version configured as "M3" and add it to the path.
    //     maven "jenkins-maven"
    // }

    stages {
        stage('Build') {
            steps {
                cleanWs()
                git url: 'https://github.com/SpringShop/discovery.git', branch: 'dev'
                sh "./mvnw -DskipTests clean package"
                sh "./mvnw docker:build"
            }

            post {
                success {
                    sh 'echo "Building docker image is successful." '
                    //junit '**/target/surefire-reports/TEST-*.xml'
                    //archiveArtifacts 'target/*.jar'
                }
            }
        }

        stage('Docker Push') {
            steps {
                sh "echo 'will push image'"
                sh 'docker login -u $dockerRepoUser -p $dockerRepoPass'
                sh 'docker tag springshop/discovery:latest springshop/discovery:latest'
                sh 'docker push springshop/discovery:latest'
                sh 'docker images'
            }

            post {
                success {
                    sh 'echo "Pushing docker image is successful." '
                }
                // always {

                // }
            }
        }

        stage('Kubernetes') {
            steps {
                sh "echo 'Going to deploy in kubernetes'"
                sh '/usr/local/bin/kubectl apply -f k8s.yml'
                sh '/usr/local/bin/kubectl get service discovery'
                sh '/usr/local/bin/kubectl describe service discovery'
            }

            post {
                success {
                    sh 'echo "Kubernetes deployment is successful." '
                }
            }
        }
    }
}
