node {
  stage("Clone the project") {
    git branch: 'main', url: 'https://github.com/daumsimac/restapidemo.git'
  }

  stage("Compilation") {
    sh "./gradlew clean build -x test"
  }

  stage("Tests and Deployment") {
    stage("Running unit tests") {
      sh "./gradlew test"
    }
    stage("Deployment") {
      sh 'nohup ./gradlew bootRun -Dserver.port=8001 &'
    }
  }
}
