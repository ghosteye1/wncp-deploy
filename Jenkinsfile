cplxStrng = "";
nameSpaceFolder = "";
deplymentsYamlFolder = ""

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
                    nameSpaceFolder = projectfolder + '/' + projectfolder+ '-namespace.yaml'
                }

                echo "${projectfolder} ${projectid} ${clusterid} ${location}"
                echo "nameSpaceFolder: ${nameSpaceFolder}"
                
                sh "ls ${projectfolder}/"
                //step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: projectfolder, credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
                step([$class: 'KubernetesEngineBuilder', projectId: projectid, clusterName: clusterid, location: location, manifestPattern: nameSpaceFolder, credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])

            }
        }
        stage('Applying all yaml to GKE') {
            steps{
                echo "${projectfolder} ${projectid} ${clusterid} ${location}"

                script {
                    deplymentsYamlFolder = projectfolder + '/'
                }

                echo "deplymentsYamlFolder : ${deplymentsYamlFolder}"

                sh "ls ${deplymentsYamlFolder}/"
                //step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: projectfolder, credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
                step([$class: 'KubernetesEngineBuilder', projectId: projectid, clusterName: clusterid, location: location, manifestPattern: deplymentsYamlFolder, credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])

            }
        }

    }    
}