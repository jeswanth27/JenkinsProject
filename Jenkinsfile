pipeline{
	agent any 		   
	environment{
		LABS=credentials('labcreds')
	}
	stages{
		stage('Build'){
			steps{
				sh 'pip3 install--user pipenv'
				sh '/bitnami/jenkins/home/.local/bin/pipenv--rm||exit0'
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
				sh 'zip-rretailproject.zip.'
				}
			}
		stage('Deploy'){
			steps{
				sh 'sshpass-p$LABS_PSWscp-oStrictHostKeyChecking=no-r.$LABS_USR@g02.itversity.com:/home/itv009820/retailproject'
				}
			}
		}
	}