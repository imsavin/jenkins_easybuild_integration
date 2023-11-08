pipeline {
    agent any
    
    stages {
        stage('EasyBuild Tests') {
        environment {
    TEST_EASYBUILD_PREFIX = "/opt/EasyBuild"
    TEST_EASYBUILD_ROBOT_PATHS = "${WORKSPACE}"
    MODULEPATH = "${TEST_EASYBUILD_PREFIX}/modules/all"
    LMOD_PATH = "/opt/lmod/lmod/init/bash"
    }

            steps {
                sh"""
                source ${LMOD_PATH}
                python3 -m venv eb_check
                source eb_check/bin/activate
                pip3 install easybuild-framework easybuild-easyblocks pycodestyle python-graph-core python-graph-dot
                export PYTHONPATH=${WORKSPACE}
                module load EasyBuild
                python3 -m test.easyconfigs.suite
                """
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
