pipeline{
    agent any

   stages{
            stage('Veified Branch'){
                steps{
                echo "$GIT_BRANCH"                    
                }
            }
       stage('build'){
            steps{
               sh 'mvn package'
            }
        }
       stage('Junit'){
           steps {([$class: 'JUnitResultArchiver', 
          testResults: 'test-results/**/test-results.xml'])
                 }                  
       }
    }
    post { 
        always { 
            echo 'I will always say Hello!'
              mail to: 'pl.shivashankar@gmail.com',
            subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
            body: "Something is wrong with ${env.BUILD_URL}"
        }
        aborted {
            echo 'I was aborted'
              mail to: 'pl.shivashankar@gmail.com',
            subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
            body: "Something is wrong with ${env.BUILD_URL}"
        }
        failure {
            mail to: 'pl.shivashankar@gmail.com',
            subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
            body: "Something is wrong with ${env.BUILD_URL}"
        }
    }
}    
