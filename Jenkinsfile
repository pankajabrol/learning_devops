pipeline {
    agent any
    
    environment {
        OPENSHIFT_SERVER = 'https://api.crc.testing:6443'
        OPENSHIFT_TOKEN = credentials('jenkins-openshift-token')
        OPENSHIFT_NAMESPACE = 'devops'
        GIT_REPO_URL = 'https://github.com/pankajabrol/learning_devops/'
        DEPLOYMENT_YAML_PATH = 'deployment.yml'
        OC_CMD = "/tmp/oc"
    }
    
    stages {
        stage('Login to OpenShift') {
            steps {
                script {
                    // Log in to OpenShift cluster
                    sh "oc login --token=${OPENSHIFT_TOKEN} --server=${OPENSHIFT_SERVER} --insecure-skip-tls-verify=true"
                }
            }
        }
        
        stage('Clone Git Repository') {
            steps {
                script {
                    // Clone Git repository
                    git branch: 'main', url: GIT_REPO_URL
                }
            }
        }
        
        stage('Deploy to OpenShift') {
            steps {
                script {
                    // Apply deployment YAML
                    sh "oc apply -f ${DEPLOYMENT_YAML_PATH} -n ${OPENSHIFT_NAMESPACE}"
                }
            }
        }
    }
}
