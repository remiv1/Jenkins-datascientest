pipeline {
    agent any
    environment {
        DOCKER_ID = "dstdockerhub"
        DOCKER_IMAGE = "datascientestapi"
        DOCKER_TAG = "v.${BUILD_ID}.0" 
    }
    stages {
        stage ('Building') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage ('Testing') {
            steps {
                sh 'python -m unittest'
            }
        }
        stage ('Deploying') {
            steps {
                script {
                    sh'''
                    docker rm -f jenkins
                    docker build -t $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG .
                    docker run -d -p 8000:8000 --name jenkins $DOCKER_ID/$DOCKER_IMAGE:$DOCKER_TAG
                    '''
                }
            }
        }
        stage ('Confirmation') {
            steps {
                input message: "Confirm Deployment", ok: "Deploy"
            }
        }
        stage ('pushing and merging') {
            parallel {
                stage ('Pushing Image') {
                    steps {
                        echo 'Pushing Docker image to Docker Hub...'
                    }
                }
                stage('Merging') {
                    steps {
                        echo 'Merging done'
                    }
                    post {
                        always {
                            echo 'Cleaning up...'
                        }
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed'
            sh 'docker logout'
        }
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Deployment failed'
        }
    }
}
