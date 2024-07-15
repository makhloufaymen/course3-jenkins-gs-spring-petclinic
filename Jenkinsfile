
    pipeline {
        agent any
        stages{

            stage("build"){
                  steps {
                    sh "./mvnw package"
                  }
            }
            stage("capture"){
                  steps {
                    archiveArtifacts artifacts: '**/target/*.jar'
                  }
            }
            stage("coverage"){
                  steps {
                    jacoco()
                  }
            }
            stage("junit"){
                  steps {
                    junit stdioRetention: '', testResults: '**/target/surefire-reports/*.xml'
                  }
            }
        }
        
        post{
            always {
                emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}", 
                to: 'always@foo.bar',
                recipientProviders: [previous()],
                subject: "${currentBuild.currentResult} : Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
            }
          
        }

        
    }
