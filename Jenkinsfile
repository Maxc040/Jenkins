pipeline {
    agent any

    stages {
        stage('Checkout from GitHub (Test)') {
            steps {
                // Check out your code from the "main" branch on GitHub.
                script {
                    def scmVars = checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'main']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [
                            [$class: 'CloneOption', noTags: false, reference: '', shallow: false],
                            [$class: 'CleanBeforeCheckout'],
                        ],
                        userRemoteConfigs: [[url: 'https://github.com/Maxc040/Jenkins.git']]
                    ])
                }
            }
        }

        stage('Deploy to Dev Server') {
            steps {
                // Deze stap is uitgeschakeld voor nu.
            }
        }

        stage('Confirmation Dev') {
            steps {
                // Deze stap is uitgeschakeld voor nu.
            }
        }

        stage('Deploy to test') {
            steps {
                // Deze stap is uitgeschakeld voor nu.
            }
        }

        stage('Confirmation test server') {
            steps {
                // Deze stap is uitgeschakeld voor nu.
            }
        }

        stage('Deploy to main Server') {
            steps {
                sh "sshpass -p student scp -o StrictHostKeyChecking=no ${currentBuild.workspace}/index.html student@192.168.1.22:/var/www/html/"
            }
        }
    }
}
