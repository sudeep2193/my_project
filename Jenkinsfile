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
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '<sudeep>',
                    usernameVariable: 'sudeep2193', passwordVariable: 'minni123']]) {
                    sshPublisher(
                        failOnError: true,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'staging',
                                sshCredentials: [
                                    username: 'sudeep2193',
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'src/**',
                                        removePrefix: 'src/'
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
        stage('DeployToProd') {
            when {
                branch 'master'
            }
            steps {
                input 'Does the staging environment look OK?'
                milestone(1)
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '<sudeep>',
                    usernameVariable: 'sudeep2193', passwordVariable: 'minni123']]) {
                    sshPublisher(
                        failOnError: true,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'production',
                                sshCredentials: [
                                    username: 'cloud_user',
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'src/**',
                                        removePrefix: 'src/'
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
    }
}
