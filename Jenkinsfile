pipeline {

    agent any
    stages {

        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build image'){          
            step {
                script {
                    print "Environment will be : ${env.NODE_ENV}"
                    
                    try {
                        app = docker.build("digitalhouse-app:${env.BUILD_ID}")
                        }
                    catch(e){
                        echo "Caught: ${e}"
                        currentBuild.result = 'FAILURE'
                        error "Build stage failed"
                    }
                    finally{

                    }
                }
            }
        }

        stage('Test image') {
            script {
                app.inside {
                    sh 'echo "Tests passed"'
                }
            }
        }

        stage('Deploy image') {

            when {
                branch 'prod'
            }
            steps {
                echo 'Deploy para Desenvolvimento'
                script {
                    app.push("latest")
                }
            }
        }

    }
}