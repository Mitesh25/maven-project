pipeline {
	agent any
		stages {
			stage ('SCM Checkout') {
				steps {
					git 'https://github.com/Mitesh25/jenkins_pipeline_hello.git'
				}
			}
			stage ('Validate Source Code') {
				steps {
					withMaven (maven: 'My_Maven') {
						sh 'mvn validate'
					}
				}
			}
			stage ('Compile Source Code') {
				steps {
					withMaven (maven: 'My_Maven'){
						sh 'mvn compile'
					}
				}
			}
			stage ('Test Source Code') {
				steps {
					withMaven (maven: 'My_Maven'){
						sh 'mvn test'
					}
				}
			}
			stage ('Package Source Code') {
				steps {
					withMaven (maven: 'My_Maven') {
						sh 'mvn package'
					}
				}
			}
			stage ('Verify Source Code') {
				steps {
					withMaven (maven: 'My_Maven') {
						sh 'mvn verify'
					}
				}
			}
			stage ('Install Source Code') {
				steps {
					withMaven (maven: 'My_Maven') {
						sh 'mvn install'
					}
				}
			}
	}}
