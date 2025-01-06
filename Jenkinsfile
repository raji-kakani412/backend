pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time:30, unit:'MINUTES')
        disableConcurrentBuilds()
        //retry(1)
    }
    environment {
        DEBUG = 'true'
        appVersion= ''
    }

    stages {
        stage('Read Version') {
            steps {
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "App Version is ${appVersion}"
                }

            }
        }
        stage('Install dependencies'){
            steps {
               sh  'npm install'
            }
        }
        stage('Docker Build') {
            steps {
                sh """
                    docker build -t rajikakani412/backend:${appVersion} .
                    docker images
                """
            }
        }
        // stage('PrintParams') {
        //     steps{
        //         echo "Hello ${params.PERSON}"
        //         echo "Biography: ${params.BIOGRAPHY}"
        //         echo "Toggle: ${params.TOGGLE}"
        //         echo "Choice: ${params.CHOICE}"
        //         echo "Password: ${params.PASSWORD}"
        //     }
        // }
        // stage('approval'){
        //     input {
        //         message "Should we continue?"
        //         ok "Yes, we should."
        //         submitter "alice,bob"
        //         parameters {
        //             string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                
        //         }
        //     }    
        //     steps {
        //         echo "Hello, ${PERSON}, nice to meet you."
        //     }
        // }  
    }
    post{
        always{
            sh 'echo This runs always'
            deleteDir()
        }
        success{
            sh 'echo This runs when pipeline is success'
        }
        failure{
            sh 'echo This runs when pipeline fails'
        }
    }
}