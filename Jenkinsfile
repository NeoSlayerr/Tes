pipeline {
  agent any
  parameters{
    choice(name: 'choice', choices: ['Release', 'Debug'], description: 'Pick something')
  }
  environment {
    APP_NAME = 'test'
  }
  options {
    // Stop the build early in case of compile or test failures
    skipStagesAfterUnstable()
  }
  stages {
   
    // stage('Detect build type') {
    //   steps {
    //     script {
    //       env.APP_NAME = ${params.choice}
    //     }
        
    //   }
    // }
    
    stage('Compile') {
      steps {
        // Compile the app and its dependencies
        bat './gradlew wrapper --gradle-version=7.3.3'
      }
    }

    stage('Build') {
      steps {
        // Compile the app and its dependencies
        bat "./gradlew clean assemble${params.choice}"
      }
    }

    stage('Deploy') {
      steps {
        // Compile the app and its dependencies
        archiveArtifacts artifacts: '**/*.apk', fingerprint: true, onlyIfSuccessful: true
      }
    }
  }   
    
}
