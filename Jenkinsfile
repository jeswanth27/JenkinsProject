pipeline{
	agent any 		   
	environment{
		LABS=credentials('labcreds')
	}
	stages{
		stage('Build'){
			steps{
				def python37 = tool 'Python 3.7'
				env.PATH = "${python37}/bin:${env.PATH}"

            // Install pipenv
				sh 'pip3 install --user pipenv'

            // Clean up existing virtual environment if exists
				sh '/bitnami/jenkins/home/.local/bin/pipenv --rm || exit 0'

            // Install dependencies using pipenv
				sh '/bitnami/jenkins/home/.local/bin/pipenv install'
			}
		}
		stage('Test'){
			steps{
				sh '/bitnami/jenkins/home/.local/bin/pipenv run pytest'
				}
			}
		stage('Package'){
			steps{
				sh 'zip -r retailproject.zip.'
				}
			}
		stage('Deploy'){
			steps{
				sh 'sshpass -p $LABS_PSW scp -o StrictHostKeyChecking=no -r . $LABS_USR@g02.itversity.com:/home/itv009820/retailproject'
				}
			}
		}
	}