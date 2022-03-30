pipeline{
	agent any 
	tools	{
		maven 'maven'
		dockerTool 'docker'
		}	
		stages{
			stage('git-clone') {
				steps{
				checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_credentials', url: 'https://github.com/ETECH-Co/etech_nodejsApp/']]])
				}
			}
			stage('code validation'){
				steps{
				sh 'mvn validate'
				}
			}
			stage('code compile'){
				steps{
				sh 'mvn compile'
				}
			}
			stage('code test'){
				steps{
				sh 'mvn test'
				}
			}
			stage('code package'){
				steps{
				sh 'mvn clean package' // -DskipTests=true'
				}
			}
			stage('Unit Tests - JUnit and JaCoCo'){
				steps{
					sh 'mvn test'
					sh 'mvn -v'
				}
//				post{
//					always{
//						junit'target/surefire-reports/*.xml'
//						jacoco execPattern: 'target/jacoco.exec'
//					}
//				}
			}
//			stage('Build Docker Image'){
//				steps{
//				withDockerRegistry(credentialsId: 'dockerHubcredentials2', url: 'https://hub.docker.com/repository/docker/jamaweh/springboot-mongo') {
//				sh 'docker build -t jamaweh/springboot-mongo:""$GIT_COMMIT"" .'
//				sh 'docker push jamaweh/springboot-mongo:""$GIT_COMMIT"" .'
//				}
//			}
  		}
	}
