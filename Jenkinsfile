cplxStrng = "";

pipeline {
    //agent any //Use this for default
    agent{
	    node{
	    	label 'cd-jenkins'
	    }
    }
    environment {
		CREDENTIALS_ID = 'wncp-k8s-service-accnt'
    }
    stages {
        stage("Checkout code") {
            steps {
                echo "Start checkout"
                checkout scm
            }
        }
        stage('Creating name space') {
            steps{
                script {
                    projectfolder = projectfolder + '/' + projectfolder+ '-namespace.json'
                }

                echo "${projectfolder} ${projectid} ${clusterid} ${location}"
                sh "ls wncp/"
                //step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: projectfolder, credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
                step([$class: 'KubernetesEngineBuilder', projectId: projectid, clusterName: clusterid, location: location, manifestPattern: projectfolder, credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])

            }
        }
        stage('Applying all yaml to GKE') {
            steps{
                script {
                    projectfolder = projectfolder + '/'
                }

                echo "${projectfolder} ${projectid} ${clusterid} ${location}"
                sh "ls wncp/"
                //step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: projectfolder, credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
                step([$class: 'KubernetesEngineBuilder', projectId: projectid, clusterName: clusterid, location: location, manifestPattern: projectfolder, credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])

            }
        }

    }    
}