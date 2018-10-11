node{
    properties([disableConcurrentBuilds()])
    echo "$branch_name"

    stage('checkout code') {
        echo "start checkout code and build image"
        // withCredentials([file(credentialsId: CONFIG_FILE_[branch_name], variable: 'CONFIG_JSON'), file(credentialsId: CONFIG_FILE['prod'], variable: 'CONFIG_PROD')]) {
            dir('test') {
                git branch: branch_name,
                    credentialsId: '123',
                    url: 'https://github.com/stormdush/building-a-multibranch-pipeline-project.git';
                
            }
        // }
        echo "checkout code and build image finished"
    }
    stage('test') {
        echo "test finished"
    }
    stage('Deploy') {
        // sshagent(['Deploy']) {
        //     test_db_ip = sh (
        //         script: "sshpass ssh -o StrictHostKeyChecking=no -l root host /home/avalon/deploy.sh test",
        //         returnStdout: true
        //     ).replace("\n", "")
        // }
        echo "Deploy finished"
    }
}