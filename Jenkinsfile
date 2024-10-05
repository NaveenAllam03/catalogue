

pipeline {
    agent { //adding agent , can add multiple agents
        node {
            label 'node1-nodejs'
        }
    } 
    // parameters {}
        //write parameters and pass arguments in stages

    environment {
        packageVersion = ''
        nexusURL = '172.31.36.195'
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
                zip -r -q catalogue.zip ./* -x ".git" -x "*.zip"
                ls -ltr
                """
            }
        }
         stage('publish Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${nexusURL}",
                    groupId: 'com.roboshop',
                    version: "${packageVersion}",
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
            }
        }
    }
    // Post build section, write what you want to do after build is sucessful
    post {
        always { //multiple options avaliable instead of always, it will run irrespective of results
            echo 'I will always say hello again'
            deleteDir()
        }
        failure {
            echo 'this runs when pipeline is failes' // generally used when pipiline fails for failure
        }
        success {
            echo 'executes when pipeline is sucessful' // runs only when pipeline is sucessful
        }
    }
}
