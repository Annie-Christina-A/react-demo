pipeline {
    agent any
    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
        REPO_URL = 'https://github.com/Annie-Christina-A/react-demo.git'
        REACT_APP_DIR = 'react-hello-world-master'
        NODE_OPTIONS = "--openssl-legacy-provider"
    }
    stages {
        stage('Checkout & Build React App') {
            // agent { label 'windows' } // Build on any one node (change label if needed)
            steps {
                git branch: 'main', credentialsId: 'github-id', url: 'https://github.com/Annie-Christina-A/react-demo.git'
                dir("${REACT_APP_DIR}") {
                    sh 'npm install'
                    sh 'npm run build'
                    stash name: 'react-build', includes: 'build/**'
                }
                // Archive the build artifacts
                // archiveArtifacts artifacts: "${REACT_APP_DIR}/build/**", fingerprint: true
            }
        }
        stage('Deploy to All Agents') {
            parallel {
                stage('Deploy to Agent 1') {
                    agent { label 'windows' }
                    environment {
                        // Windows-specific PATH
                        PATH = "C:\\Windows\\System32;${NODEJS_HOME}\\bin;${env.PATH}"
                    }
                    steps {
                        dir("${REACT_APP_DIR}") {
                            unstash 'react-build'
                        }
                        // copyArtifacts(projectName: env.JOB_NAME, selector: lastSuccessful())
                        bat 'if exist C:\\inetpub\\wwwroot\\my-react-app rd /s /q C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'mkdir C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'xcopy react-hello-world-master\\build\\* C:\\inetpub\\wwwroot\\my-react-app /E /I /Y'
                    }
                }
                stage('Deploy to Agent 2') {
                    agent { label 'Shahana-Agent' }
                    environment {
                        // Windows-specific PATH
                        PATH = "C:\\Windows\\System32;${NODEJS_HOME}\\bin;${env.PATH}"
                    }
                    steps {
                        dir("${REACT_APP_DIR}") {
                            unstash 'react-build'
                        }
                        // copyArtifacts(projectName: env.JOB_NAME, selector: lastSuccessful())
                        bat 'if exist C:\\inetpub\\wwwroot\\my-react-app rd /s /q C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'mkdir C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'xcopy react-hello-world-master\\build\\* C:\\inetpub\\wwwroot\\my-react-app /E /I /Y'
                    }
                }
                stage('Deploy to Agent 3') {
                    agent { label 'Archana-agent' }
                    environment {
                        // Windows-specific PATH
                        PATH = "C:\\Windows\\System32;${NODEJS_HOME}\\bin;${env.PATH}"
                    }
                    steps {
                        dir("${REACT_APP_DIR}") {
                            unstash 'react-build'
                        }
                        // copyArtifacts(projectName: env.JOB_NAME, selector: lastSuccessful())
                        bat 'if exist C:\\inetpub\\wwwroot\\my-react-app rd /s /q C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'mkdir C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'xcopy react-hello-world-master\\build\\* C:\\inetpub\\wwwroot\\my-react-app /E /I /Y'
                        // bat 'iisreset'
                    }
                }
                stage('Deploy to Agent 4') {
                    agent { label 'Dharshanads-agent' }
                    environment {
                        // Windows-specific PATH
                        PATH = "C:\\Windows\\System32;${NODEJS_HOME}\\bin;${env.PATH}"
                    }
                    steps {
                        dir("${REACT_APP_DIR}") {
                            unstash 'react-build'
                        }
                        // copyArtifacts(projectName: env.JOB_NAME, selector: lastSuccessful())
                        bat 'if exist C:\\inetpub\\wwwroot\\my-react-app rd /s /q C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'mkdir C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'xcopy react-hello-world-master\\build\\* C:\\inetpub\\wwwroot\\my-react-app /E /I /Y'
                        // bat 'iisreset'
                    }
                }
                stage('Deploy to Agent 5') {
                    agent { label 'Annie-Agent' }
                    environment {
                        // Windows-specific PATH
                        PATH = "C:\\Windows\\System32;${NODEJS_HOME}\\bin;${env.PATH}"
                    }
                    steps {
                        dir("${REACT_APP_DIR}") {
                            unstash 'react-build'
                        }
                        // copyArtifacts(projectName: env.JOB_NAME, selector: lastSuccessful())
                        bat 'if exist C:\\inetpub\\wwwroot\\my-react-app rd /s /q C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'mkdir C:\\inetpub\\wwwroot\\my-react-app'
                        bat 'xcopy react-hello-world-master\\build\\* C:\\inetpub\\wwwroot\\my-react-app /E /I /Y'
                        // bat 'iisreset'
                    }
                }
            }
        }
    }
    post {
        success {
            echo ':white_check_mark: React app successfully deployed to all 5 agents!'
        }
        failure {
            echo ':x: Deployment failed. Please check logs on respective agents.'
        }
    }
}
