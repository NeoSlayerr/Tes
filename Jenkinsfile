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
   
    stage('Detect build type') {
      steps {
        script {
          if (env.BRANCH_NAME == 'develop' || env.CHANGE_TARGET == 'develop') {
            env.BUILD_TYPE = 'debug'
          } else if (env.BRANCH_NAME == 'master' || env.CHANGE_TARGET == 'master') {
            env.BUILD_TYPE = 'release'
          }
        }
        
      }
    }
    
    stage('Compile') {
      steps {
        // Compile the app and its dependencies
        bat './gradlew wrapper --gradle-version=7.3.3'
      }
    }

    stage('Build') {
      steps {
        // Compile the app and its dependencies
        bat './gradlew clean assemble${choice}'
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
