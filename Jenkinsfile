pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out GitHub repository'
            }
        }

        stage('Execute Script') {
            steps {
                sh '''
                    chmod +x build.sh
                    ./build.sh
                '''
            }
        }
    }

    post {
        always {
            emailext(
                to: 'dhanyasathasivam@gmail.com',
                subject: "Jenkins Build ${currentBuild.currentResult}: ${env.JOB_NAME}",
                body: """
Hello,

Your Jenkins build has completed.

Project: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build Status: ${currentBuild.currentResult}
Build URL: ${env.BUILD_URL}

Please find the console output attached.

Regards,
Jenkins
                """,
                attachLog: true
            )
        }
    }
}
