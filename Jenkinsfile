

pipeline {
    agent { //adding agent , can add multiple agents
        node {
            label 'agent-1'
        }
    } 
    // parameters {}
        //write parameters and pass arguments in stages

    environment {
        packageVersion = ''
    }
    //options{}
        // to write timeout, exits when time limit exceeds
        //disableconcurentbuilds()

    // build section, Write alll the build steps here 
    stages {
        stage('Get the version') {
            steps {
                script { // writing ruby scripts
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version 
                    echo "appliaction version is $packageVersion"
                }
            }
        }
         stage('install depencencies') {
            steps {
                sh """
                    npm install
                """
            }
        }
         stage('build job') {
            steps {
                sh """
                ls -la  
                """
            }
        }
    }
    // Post build section, write what you want to do after build is sucessful
    post {
        always { //multiple options avaliable instead of always, it will run irrespective of results
            echo 'I will always say hello again'
        }
        failure {
            echo 'this runs when pipeline is failes' // generally used when pipiline fails for failure
        }
        success {
            echo 'executes when pipeline is sucessful' // runs only when pipeline is sucessful
        }
    }
}
