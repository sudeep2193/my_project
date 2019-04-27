pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build'
                archiveArtifacts artifacts: 'src/index.html'
            }
        }
        stage('DeployToStage') {
            when {
                branch 'master'
            }
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '<CREDENTIAL_ID>',
                    usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                                  println(env.USERNAME)
            }
        }
        stage('DeployToProd') {
            when {
                branch 'master'
            }
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '<sudeep>',
                    usernameVariable: 'sudeep2193', passwordVariable: 'minni123']]) {
                                  println(env.USERNAME)
            }
    }
    
    
    
