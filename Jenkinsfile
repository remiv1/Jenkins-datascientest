// at the pipeline and stage level
pipeline {
    agent any
    environment {
         nom = 'datascientest'
    }
    stages {
        stage('Example') {
            environment {
                AN_ACCESS_KEY = credentials('datascientest-secret')  // variable secret
            }
            steps {
                sh 'print $nom' // variable call
            }
        }
        stage("Datascientest Variables") {
            steps {
                sh "printenv"
            }
        }
        stage("Datascientest Env Variables") {
            steps {
                echo "The build id is ${env.BUILD_ID} or $BUILD_ID or ${BUILD_ID} "
            }
        }
        stage("Env Variables") {
            environment {
                NAME = "Datascientest"
            }

            steps {
                echo "SHOOL = ${env.SHOOL}"
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
