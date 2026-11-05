pipeline {
    agent any

    environment {
        DEPLOY_DIR = "${WORKSPACE}/../java-sum-deployment"
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                    mkdir -p build
                    javac -d build src/SumArray.java
                    jar cfe build/SumArray.jar SumArray -C build .
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    mkdir -p "$DEPLOY_DIR"
                    cp build/SumArray.jar "$DEPLOY_DIR/"
                '''
            }
        }

        stage('Execute') {
            steps {
                sh '''
                    cd "$DEPLOY_DIR"
                    printf "10\\n20\\n30\\n40\\n50\\n" | java -jar SumArray.jar
                '''
            }
        }
    }

    post {
        success {
            echo 'Build, deployment and execution completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
