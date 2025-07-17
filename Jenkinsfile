pipeline {
    agent any
    environment {
        NOM = 'datascientest'
    }
    stages {
        stage('debug') {
            steps{
                echo "ça plane pour moi a a a a a a !"
            }
        }
        stage('Example') {
            steps {
                echo "NOM = ${env.NOM}"
                sh 'echo $NOM'
            }
        }
        stage("Datascientest Variables") {
            steps {
                sh "printenv"
            }
        }
        stage("Datascientest Env Variables") {
            steps {
                echo "The build id is ${env.BUILD_ID}"
            }
        }
        stage("Env Variables") {
            environment {
                NAME = "Datascientest"
            }
            steps {
                echo "NAME = ${env.NAME}"

                script {
                    env.TEST_VARIABLE = "some test value"
                }
                echo "TEST_VARIABLE = ${env.TEST_VARIABLE}"

                withEnv(["ANOTHER_ENV_VAR=here is some value"]) {
                    echo "ANOTHER_ENV_VAR = ${env.ANOTHER_ENV_VAR}"
                }
            }
        }
    }
}
