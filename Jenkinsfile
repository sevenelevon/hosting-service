pipeline {
    agent {
        node('мастер') {
            label 'мастер'
            customWorkspace '/home/jenkins/workspace/hosting-service'
        }
    }
    environment {
        // Указываем путь к NVM_DIR для Jenkins
        NVM_DIR = '/home/ubuntu/.nvm'
        // Активируем нужную версию Node.js
        PATH = "$NVM_DIR/versions/node/v18.17.0/bin:$PATH"
        WORKSAPCE = "/home/ubuntu/project/elochka/frontend"
    }
    stages {
        stage('install node js') {
            steps {
                echo "install nvm and use node js"
                sh 'cd /home/ubuntu/project/elochka/frontend'
                sh 'ls -a'
                sh 'hostname'
            }
        }

        stage('Path to nvm') {
            steps {
                script {
                    //Активируем нужную версию node.js
                    def nodeBinPath = sh(
                        returnStdout: true,
                        script: ". $NVM_DIR/nvm.sh && nvm use 18.17.0 && echo \$NVM_BIN"
                    ).trim()
                        withEnv(["PATH+NODE=${nodeBinPath}:$PATH"]) {
                            sh 'npm --version'
                    }
                }
                // Далее можете продолжить со сборкой в Build стадии
            }
        }

        stage('Install and Build') {
            steps {
                echo "Install nvm and use Node.js"
                sh "npm install -g yarn"
                sh 'yarn install'
                sh 'yarn build'
                sh 'ls -l'
                sh 'pwd'
                // mv folder in service
                sh 'mkdir -p home/ubuntu/project/build_project/hosting-service/'
                sh 'sudo cp -r /home/ubuntu/jenkins/workspace/hosting-service/build/* /home/ubuntu/project/build_project/hosting-service/build/'
                dir('/home/ubuntu/project/build_project/hosting_service') {
                    echo "Working dir /home/ubuntu/project/build_project/hosting_service"
                    sh 'pwd'
                    sh 'ls -a'

                }
            }
        }

        stage('Serve') {
            steps {
                echo "Install and run serve"
                sh 'whoami'
                // dir('/home/ubuntu/project/build_project/hosting-service/build/') {
                //     sh 'serve -s .'
                // }
                dir('/home/ubuntu/jenkins/workspace/hosting-service/build') {
                    sh 'pwd'
                    sh 'yarn build'
                    sh 'serve -s .'
                }
            }
        }
    }
}
