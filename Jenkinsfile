  pipeline {
    agent any
    tools {
            maven 'maven'
      }
    stages {
        
        stage('Build') {
              steps {
                  sh "mvn -B -DskipTests clean package"
                  archiveArtifacts artifacts: 'target/app.war'
            }
        }        
        
        
        
    
  
    stage('Build Docker image'){
                       
            steps {
                script {
                    app = docker.build("world2enjoy/phoenix2.0")
                    app.inside {
                        sh 'echo $(curl localhost:80)'
                    }
                }
            }
            
        }
        
        stage('Push docker image'){
           
            steps{
                script {
                    docker.withRegistry('https://registry.hub.docker.com','Raghav_hub_login'){
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        
        stage('Run ZAP scan'){  
      steps {
                script {
                    
                  sh('bash ./run-docker.sh http://54.185.178.109:30005/app > scanoutput.txt')
                   sh('cat scanoutput.txt')
                    
                }
            }  
      
        }
        
        stage('Deploy kubernetes'){
          
          steps {
           kubernetesDeploy(
                kubeconfigId: 'kubeconfig',
                configs: 'application.yaml',
                enableConfigSubstitution: true)
                echo 'App url: http://54.185.178.109:30005/app'
          }
                     
        }
        
    }
}
