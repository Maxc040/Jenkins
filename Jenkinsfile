pipeline {
    agent any

    stages {
        stage('Checkout from GitHub') {
            steps {
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
                sh "sshpass -p student scp -o StrictHostKeyChecking=no ${currentBuild.workspace}/index.html student@192.168.1.24:/var/www/html/"
            }
        }

        stage('Confirmation Dev') {
            steps {
                input(id: 'confirmDeployment', message: 'Review the test environment. If everything looks good, approve for Development.', ok: 'Deploy')
            }
        }

        stage('Deploy to Test Server') {
            steps {
                sh "sshpass -p student scp -o StrictHostKeyChecking=no ${currentBuild.workspace}/index.html student@192.168.1.23:/var/www/html/"
            }
        }

        stage('Confirmation Test Server') {
            steps {
                input(id: 'confirmDeployment', message: 'Review the test environment. If everything looks good, approve for Development.', ok: 'Deploy')
            }
        }

        stage('Deploy to Main Server') {
            steps {
                sh "sshpass -p student scp -o StrictHostKeyChecking=no ${currentBuild.workspace}/index.html student@192.168.1.22:/var/www/html/"
            }
        }
    }
}
