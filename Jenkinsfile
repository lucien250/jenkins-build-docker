node{
  def app
    stage('Clone') {
        checkout scm
    }
    stage('Build image') {
        app = docker.build("lucien/nginx")
    }
     stage('RUN') {
        sh "docker run --name run-${env.BUILD_ID} -p 80:80 -d $IMAGE"
        sh 'curl localhost'
        sh "docker stop run-${env.BUILD_ID} && docker rm run-${env.BUILD_ID}"
    }

    stage('Push') {
        docker.withRegistry('https://registry.gitlab.com', 'reg1') {
            img.push('latest')
            img.push("version-${env.BUILD_ID}")
       }
     }
  }
