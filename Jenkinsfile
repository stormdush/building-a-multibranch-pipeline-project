node{
    properties([disableConcurrentBuilds()])
    echo "$branch_name"

    stage('checkout code') {
        echo "start checkout code and build image"
        // withCredentials([file(credentialsId: CONFIG_FILE[branch_name], variable: 'CONFIG_JSON'), file(credentialsId: CONFIG_FILE['prod'], variable: 'CONFIG_PROD')]) {
            dir('test') {
                git branch: branch_name,
                    url: 'https://github.com/stormdush/building-a-multibranch-pipeline-project.git';
                
            }
        // }
        echo "checkout code and build image finished"
    }
    stage('test') {
        echo "test finished"
    }
    stage('Deploy') {
        echo "Deploy finished"
    }
}