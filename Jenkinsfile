pipeline { 
    agent { label "default" } 
    options {
        ansiColor('xterm')
        timestamps ()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    stages {
                // the code here can access $pass and $user
            stage('Error scan') { 
                steps { 
                    sh '''
                         popeye --force-exit-zero -l error -o html --save --output-file popeye.html
                         trivy k8s -s HIGH,CRITICAL -n app --no-progress --report summary deploy
                    '''
                }
            }
        stage('Warning scan'){
            steps {
                sh 'echo "testing will be here"'
            }
        }
        stage('Publish') {
            steps {
                sh 'echo "deploy with GitOps"'
            }
        }
    }
}