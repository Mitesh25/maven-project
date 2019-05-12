pipeline {
	agent any
		stages {
			stage ('SCM Checkout') {
				steps {
					git 'https://github.com/Mitesh25/mitesh-maven-project.git'
				}
			}
			stage ('Validate Source Code') {
				steps {
					withMaven(maven: 'My_Maven') {
						sh 'mvn validate'
					}
				}
			}
			stage ('Compile Source Code') {
				steps {
					withMaven(maven: 'My_Maven'){
						sh 'mvn clean compile'
					}
				}
			}
			stage ('Test Source Code') {
				steps {
					withMaven(maven: 'My_Maven'){
						sh 'mvn test'
					}
				}
			}
			stage('Sonarqube') {
				environment {
					scannerHome = tool 'SonarQubeScanner'
				}
				steps {
					withSonarQubeEnv('SonarPipeline3') {
					sh 'mvn test sonar:sonar'
					}
					timeout(time: 10, unit: 'MINUTES') {
					waitForQualityGate abortPipeline: true
					}
				}
			}
			stage ('Package Source Code') {
				steps {
					withMaven(maven: 'My_Maven') {
						sh 'mvn package'
					}
				}
			}
			stage ('Verify Source Code') {
				steps {
					withMaven(maven: 'My_Maven') {
						sh 'mvn verify'
					}
				}
			}
			stage ('Install Source Code') {
				steps {
					withMaven(maven: 'My_Maven') {
						sh 'mvn install'
					}
				}
			}
			stage ('Deploy on tomcat') {
				steps {
					sshagent(['12455444-a97a-48e0-abe1-ae4f7da75736']) {
					sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@172.31.32.155:/var/lib/tomcat/webapps'
					}
				}
			}
	}}
