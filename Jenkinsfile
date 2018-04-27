node{
    def classroomapp
    def build_arg = ""
    def prefix = "warriortrading"
    def classroomname = "hermes.service.classroom"
    def docker_image_classroom = "${prefix}/${classroomname}:DEV-${env.BUILD_ID}"
    def registry_address = "https://registry.hub.docker.com"
    def maillist = "barry@warriortrading.com;chaofan.jiang@nirvana-info.com;avalon.han@nirvana-info.com"
    def test_db_ip
    def TEST_POSTGRES_ENTRY
    boolean pushImageSuccess = false
    echo env.BRANCH_NAME
    stage('checkout code and build image') {
        echo "start checkout code and build image"
        withCredentials([
            // DEV
            // common 
            string(credentialsId: 'dev-crm-jwt-secret', variable: 'DEV_CRM_JWT_SECRET'),
            string(credentialsId: 'dev-key-hex', variable: 'DEV_KEY_HEX'),
            string(credentialsId: 'dev-iv-hex', variable: 'DEV_IV_HEX'),
            string(credentialsId: 'dev-jwt-secret', variable: 'DEV_JWT_SECRET'),
            string(credentialsId: 'dev-enhance-key-hex', variable: 'DEV_ENHANCE_KEY_HEX'),
            string(credentialsId: 'dev-enhance-iv-hex', variable: 'DEV_ENHANCE_IV_HEX'),
            string(credentialsId: 'dev-postgres-entry', variable: 'DEV_POSTGRES_ENTRY'),
            // for classroom and file
            string(credentialsId: 'dev-hermes-api-secret', variable: 'DEV_HERMES_API_SECRET'),
            // for classroom
            string(credentialsId: 'dev-auth-secret', variable: 'DEV_AUTH_SECRET'),
            string(credentialsId: 'dev-test-secret', variable: 'DEV_TEST_SECRET'),
            string(credentialsId: 'dev-liveswitch-appid', variable: 'DEV_LIVESWITCH_APPID'),
            string(credentialsId: 'dev-liveswitch-secret', variable: 'DEV_LIVESWITCH_SECRET'),
            // QA
            string(credentialsId: 'qa-crm-jwt-secret', variable: 'QA_CRM_JWT_SECRET'),
            string(credentialsId: 'qa-key-hex', variable: 'QA_KEY_HEX'),
            string(credentialsId: 'qa-iv-hex', variable: 'QA_IV_HEX'),
            string(credentialsId: 'qa-jwt-secret', variable: 'QA_JWT_SECRET'),
            string(credentialsId: 'qa-enhance-key-hex', variable: 'QA_ENHANCE_KEY_HEX'),
            string(credentialsId: 'qa-enhance-iv-hex', variable: 'QA_ENHANCE_IV_HEX'),
            string(credentialsId: 'qa-postgres-entry', variable: 'QA_POSTGRES_ENTRY'),
            // for classroom and file
            string(credentialsId: 'qa-hermes-api-secret', variable: 'QA_HERMES_API_SECRET'),
            // for classroom
            string(credentialsId: 'qa-auth-secret', variable: 'QA_AUTH_SECRET'),
            string(credentialsId: 'qa-test-secret', variable: 'QA_TEST_SECRET'),
            string(credentialsId: 'qa-liveswitch-appid', variable: 'QA_LIVESWITCH_APPID'),
            string(credentialsId: 'qa-liveswitch-secret', variable: 'QA_LIVESWITCH_SECRET'),
            // PROD
            string(credentialsId: 'prod-crm-jwt-secret', variable: 'PROD_CRM_JWT_SECRET'),
            string(credentialsId: 'prod-key-hex', variable: 'PROD_KEY_HEX'),
            string(credentialsId: 'prod-iv-hex', variable: 'PROD_IV_HEX'),
            string(credentialsId: 'prod-jwt-secret', variable: 'PROD_JWT_SECRET'),
            string(credentialsId: 'prod-enhance-key-hex', variable: 'PROD_ENHANCE_KEY_HEX'),
            string(credentialsId: 'prod-enhance-iv-hex', variable: 'PROD_ENHANCE_IV_HEX'),
            string(credentialsId: 'prod-postgres-entry', variable: 'PROD_POSTGRES_ENTRY'),
            // for classroom and file
            string(credentialsId: 'prod-hermes-api-secret', variable: 'PROD_HERMES_API_SECRET'),
            // for classroom
            string(credentialsId: 'prod-auth-secret', variable: 'PROD_AUTH_SECRET'),
            string(credentialsId: 'prod-test-secret', variable: 'PROD_TEST_SECRET'),
            string(credentialsId: 'prod-liveswitch-appid', variable: 'PROD_LIVESWITCH_APPID'),
            string(credentialsId: 'prod-liveswitch-secret', variable: 'PROD_LIVESWITCH_SECRET'),
            // STAGE
            string(credentialsId: 'stage-crm-jwt-secret', variable: 'STAGE_CRM_JWT_SECRET'),
            string(credentialsId: 'stage-key-hex', variable: 'STAGE_KEY_HEX'),
            string(credentialsId: 'stage-iv-hex', variable: 'STAGE_IV_HEX'),
            string(credentialsId: 'stage-jwt-secret', variable: 'STAGE_JWT_SECRET'),
            string(credentialsId: 'stage-enhance-key-hex', variable: 'STAGE_ENHANCE_KEY_HEX'),
            string(credentialsId: 'stage-enhance-iv-hex', variable: 'STAGE_ENHANCE_IV_HEX'),
            string(credentialsId: 'stage-postgres-entry', variable: 'STAGE_POSTGRES_ENTRY'),
            // for classroom and file
            string(credentialsId: 'stage-hermes-api-secret', variable: 'STAGE_HERMES_API_SECRET'),
            // for classroom
            string(credentialsId: 'stage-auth-secret', variable: 'STAGE_AUTH_SECRET'),
            string(credentialsId: 'stage-test-secret', variable: 'STAGE_TEST_SECRET'),
            string(credentialsId: 'stage-liveswitch-appid', variable: 'STAGE_LIVESWITCH_APPID'),
            string(credentialsId: 'stage-liveswitch-secret', variable: 'STAGE_LIVESWITCH_SECRET')
        ]) {
            dir('classroom') {
                // DEV
                build_arg += "--build-arg DEV_CRM_JWT_SECRET"
                build_arg += " --build-arg DEV_KEY_HEX"
                build_arg += " --build-arg DEV_IV_HEX"
                build_arg += " --build-arg DEV_JWT_SECRET"
                build_arg += " --build-arg DEV_ENHANCE_KEY_HEX"
                build_arg += " --build-arg DEV_ENHANCE_IV_HEX"
                build_arg += " --build-arg DEV_HERMES_API_SECRET"
                build_arg += " --build-arg DEV_AUTH_SECRET"
                build_arg += " --build-arg DEV_TEST_SECRET"
                build_arg += " --build-arg DEV_LIVESWITCH_APPID"
                build_arg += " --build-arg DEV_LIVESWITCH_SECRET"
                build_arg += " --build-arg DEV_POSTGRES_ENTRY"
                // QA
                build_arg += " --build-arg QA_CRM_JWT_SECRET"
                build_arg += " --build-arg QA_KEY_HEX"
                build_arg += " --build-arg QA_IV_HEX"
                build_arg += " --build-arg QA_JWT_SECRET"
                build_arg += " --build-arg QA_ENHANCE_KEY_HEX"
                build_arg += " --build-arg QA_ENHANCE_IV_HEX"
                build_arg += " --build-arg QA_HERMES_API_SECRET"
                build_arg += " --build-arg QA_AUTH_SECRET"
                build_arg += " --build-arg QA_TEST_SECRET"
                build_arg += " --build-arg QA_LIVESWITCH_APPID"
                build_arg += " --build-arg QA_LIVESWITCH_SECRET"
                build_arg += " --build-arg QA_POSTGRES_ENTRY"
                // PROD
                build_arg += " --build-arg PROD_CRM_JWT_SECRET"
                build_arg += " --build-arg PROD_KEY_HEX"
                build_arg += " --build-arg PROD_IV_HEX"
                build_arg += " --build-arg PROD_JWT_SECRET"
                build_arg += " --build-arg PROD_ENHANCE_KEY_HEX"
                build_arg += " --build-arg PROD_ENHANCE_IV_HEX"
                build_arg += " --build-arg PROD_HERMES_API_SECRET"
                build_arg += " --build-arg PROD_AUTH_SECRET"
                build_arg += " --build-arg PROD_TEST_SECRET"
                build_arg += " --build-arg PROD_LIVESWITCH_APPID"
                build_arg += " --build-arg PROD_LIVESWITCH_SECRET"
                build_arg += " --build-arg PROD_POSTGRES_ENTRY"
                //STAGE
                build_arg += " --build-arg STAGE_CRM_JWT_SECRET"
                build_arg += " --build-arg STAGE_KEY_HEX"
                build_arg += " --build-arg STAGE_IV_HEX"
                build_arg += " --build-arg STAGE_JWT_SECRET"
                build_arg += " --build-arg STAGE_ENHANCE_KEY_HEX"
                build_arg += " --build-arg STAGE_ENHANCE_IV_HEX"
                build_arg += " --build-arg STAGE_HERMES_API_SECRET"
                build_arg += " --build-arg STAGE_AUTH_SECRET"
                build_arg += " --build-arg STAGE_TEST_SECRET"
                build_arg += " --build-arg STAGE_LIVESWITCH_APPID"
                build_arg += " --build-arg STAGE_LIVESWITCH_SECRET"
                build_arg += " --build-arg STAGE_POSTGRES_ENTRY"
                // test
                build_arg += " --build-arg TEST_POSTGRES_ENTRY=${TEST_POSTGRES_ENTRY}"
                build_arg += " .";
                echo build_arg
            }
        }
        echo "checkout code and build image finished"
    }
    stage('compose and test') {
        echo "test finished"
    }
    stage('mail test result and push image') {
        echo "mail result and push image finished"
    }
    stage('deploy image on aws') {
        
    }
}