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

        stage('Build') {
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
                echo "building states"
                sh 'ls -a'
                sh 'sudo chown -R $USER:$(id -gn $USER) /home/ubuntu/.nvm/versions/node/v18.17.0'
                sh "npm install -g yarn"
                sh 'cd /home/ubuntu/project/elochka/frontend'
                sh 'pwd'
                sh 'ls -a'
                sh "yarn install"
                sh "yarn build"
                // Далее можете продолжить со сборкой в Build стадии
            }
        }
    }
}
