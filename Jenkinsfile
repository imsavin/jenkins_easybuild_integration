pipeline {
    agent any
    environment {
    TEST_EASYBUILD_PREFIX = "/opt/EasyBuild"
    TEST_EASYBUILD_ROBOT_PATHS = "${WORKSPACE}/easyconfig"
    MODULEPATH = "${TEST_EASYBUILD_PREFIX}/modules/all"
    LMOD_PATH = "/opt/lmod/lmod/init/bash"
    }
    
    stages {
        stage('Run EasyBuild Tests') {
    

            steps {
                sh"""
                source ${LMOD_PATH}
                python3 -m venv eb_check
                source eb_check/bin/activate
                pip3 install pycodestyle python-graph-core python-graph-dot
                export PYTHONPATH=${WORKSPACE}
                module load EasyBuild
                python3 -m test.easyconfigs.suite
                """
            }
        }
        stage('Run Style Tests') {
            steps {
                sh"""
                source ${LMOD_PATH}
                source eb_check/bin/activate
                module load EasyBuild
                eb --check-style easybuild/
                """
                }
        
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
     post {
          Clean after build
        always {
            cleanWs()
        }
    }
 }
