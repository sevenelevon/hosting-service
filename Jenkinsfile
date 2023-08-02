pipeline {
    agent any
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
                sh "chmod -R 777 ${env.WORKSPACE}"
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
                sh 'sudo chown -R $USER:$(id -gn $USER) /home/ubuntu/.nvm/versions/node/v18.17.0'
                // sh "npm install -g yarn"
                dir('/home/ubuntu/project/build_project/hosting_service') {
                    echo "Working dir /home/ubuntu/project/build_project/hosting_service"
                    sh 'sudo chown -R $USER:$(id -gn $USER) /home/ubuntu/project/build_project'
                    sh 'sudo chmod  -R 777 /home/ubuntu/project/build_project'
                    sh 'pwd'
                    sh 'ls -a'
                    sh 'yarn install'
                    sh 'yarn build'
                }
            }
        }

        stage('Serve') {
            steps {
                echo "Install and run serve"
                sh "yarn global add serve"
                dir('/home/ubuntu/project/build_project/hosting_service/build') {
                    sh 'sudo chown -R $USER:$(id -gn $USER) /home/ubuntu/project/build_project/'
                    sh 'sudo chmod  -R 777 /home/ubuntu/project/build_project/'
                    sh 'serve -s .'
                }
            }
        }
    }
}
