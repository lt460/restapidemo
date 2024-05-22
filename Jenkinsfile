node {
  def dockerHubRepo = 'azizbek_kadyrov@mail.ru/lt460'
  def dockerHubCredentialsId = 'DockerHub_ID'

  stage("Clone the project") {
    git branch: 'main', url: 'https://github.com/daumsimac/restapidemo.git'
  }

  stage("Compilation") {
    sh "chmod +x ./gradlew"
    sh "./gradlew clean build -x test"
  }

  stage("Tests and Deployment") {
    stage("Running unit tests") {
      sh "chmod +x ./gradlew"
      sh "./gradlew test"
    }
    stage("Deployment") {
      sh "chmod +x ./gradlew"
      sh 'nohup ./gradlew bootRun -Dserver.port=8080 &'
      sh 'echo Lslc102130 | sudo docker login -u azizbek_kadyrov@mail.ru --password-stdin'
      sh 'sudo docker build -t lt460/restapidemo:1.0 .'
    }
    stage('Push Docker Image') {
        script {
            docker.withRegistry('https://index.docker.io/v1/', dockerHubCredentialsId) {
                def image = docker.image("lt460/restapidemo:1.0")
                image.push()
                image.push('1.0')
            }
        }
    }
  }
}