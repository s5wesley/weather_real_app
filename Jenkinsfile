pipeline {
    agent any

    stages {
        // stage('Trivy Scan') {
        //     steps {
        //         script {
        //             sh 'trivy docker-compose.yml'
        //         }
        //     }
        // }
        
        stage('Deploy') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml down --remove-orphans'
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
            }
        }
    }
    
    post {
        always {
            script {
                sh 'docker-compose -f docker-compose.yml ps'
                sleep time: 6*60, unit: 'SECONDS'
                sh 'docker-compose -f docker-compose.yml down'
            }
        }
        
        success {
            script {
                slackSend color: '#2EB67D',
                    channel: 'general',
                    message: "*WEATHER_APP Project Deployment Status*" +
                        "\n Project Name: s5wesley-WESTHER-APP" +
                        "\n Job Name: ${env.JOB_NAME}" +
                        "\n Deployment Status : *SUCCESS*" +
                        "\n Deployment url : ${env.BUILD_URL}"
            }
        }
        
        // failure {
        //     script {
        //         slackSend color: '#E01E5A',
        //             channel: 'general',
        //             message: "*WEATHER_APP Project Deployment Status*" +
        //                 "\n Project Name: s5wesley-WESTHER-APP" +
        //                 "\n Job Name: ${env.JOB_NAME}" +
        //                 "\n Deployment Status : *FAILED*" +
        //                 "\n Deployment url : ${env.BUILD_URL}"
        //     }
        // }
    }
}
