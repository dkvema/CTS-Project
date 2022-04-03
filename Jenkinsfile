def appName='nodejs-docker'
def app
def versiontag
def dockerImageName
def MAJOR_VERSION="1"
def ARTIFACT_VERSION="${MAJOR_VERSION}.${BUILD_NUMBER}"

def getGitCommitHash(){
    def result =sh(returnStdout:true,script:'git rev-parse--short HEAD'.trim())
    return result
}
def generateVersionTag(){
    def gitCommitHash=getGitCommitHash()
    versionTag= ${env.BRANCH_NAME} + ${env.BUILD_NUMBER} + "-"+gitCommitHash
    return versionTag


}
pipeline {

  /* environment {
     registry = "devendravemadevops/nodejs-docker"
     registryCredential = 'dockerhubrepository'
     dockerImage = ''
    }
    */

    agent any

     options {

        // This is required if you want to clean before build
        skipDefaultCheckout(true)
      }
     // tools {nodejs "NodeJS"}

    stages{
        stage('Clone the repository') {
            steps{
                echo sh(script: 'env|sort', returnStdout: true)
                echo 'cloning the respository..'
                echo " build version: ${MAJOR_VERSION}.${env.BUILD_ID}"
                  echo "code commited from repository APPName:${appName}"
              checkout scm
              }
           }
      stage('NPM install') {
            steps{
                sh 'NPM install'
                sh 'NPM install dotenv'
            }
        }
       stage('test') {
            steps{
               echo 'Testing..'
              sh 'NPM test'
            }
        }

    }  
  }
