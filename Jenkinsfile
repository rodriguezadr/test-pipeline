pipeline {
    agent any
    
    environment{
        BASE_URL = 'https://172.25.10.57:8443'
        TEST_COLLECTION_PATH = '/home/adrian/Desktop/Test_Instapay_P2B_RFI.postman_collection'
        SKIP_VAR = "${env.SKIP_VAR}"
        NODEJS_HOME = '/var/lib/jenkins/tools/jenkins.plugins.nodejs.tools.NodeJSInstallation/Newman/bin/node'
    }

    stages {
        
        stage('Checkout Source Code') {
            steps {
                //Define which branch to checkout
               git branch: 'integration',
               //Replace with your credentials as found in Jenkins credential manager
               //Change to sabilaed-github
                credentialsId: 'b59f4f33-99f8-49fd-8eaf-e7c45bfd1bf0',
                url: 'https://github.com/pnbph-asid/pnb-biller-service.git'
                script {
                    env.PATH = "${NODEJS_HOME}"
                }
            }
        }
            
        stage('Execute Test Collection') {
            steps {
                //Define path of test collection to be executed
                //To specify folder, use arugment --folder "Folder Name"
                //To provide environment variables, use --env-var "key=value"
                    //Example in P2B RFI, --env-var "baseUrl=https://baseUrl=https://172.25.10.57:8443" for SIT Server
        sh "newman run ${TEST_COLLECTION_PATH} ${SKIP_VAR} --env-var 'baseUrl=${BASE_URL}' -r htmlextra --insecure"
            }
        }
    }
} 
