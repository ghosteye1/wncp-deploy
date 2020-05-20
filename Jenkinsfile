cplxStrng = "";

pipeline {
    //agent any //Use this for default
    agent{
	    node{
	    	label 'cd-jenkins'
	    }
    }
    environment {
        PROJECT_ID = 'wn-cloud-275704'
		CLUSTER_NAME = 'wn-cloud-portal-test'
		LOCATION = 'us-central1-c'
		CREDENTIALS_ID = 'wncp-k8s-service-accnt'
    }
    stages {
        stage("Checkout code") {
            steps {
                echo "Start checkout"
                checkout scm
            }
        }
        stage('Applying all yaml to GKE') {
            steps{
                echo "${projectfolder}"
                sh "ls wncp/"
                
                //step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'k8s/', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
            }
        }

    }    
}