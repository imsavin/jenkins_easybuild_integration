pipeline {
    agent any
    environment {
    EASYBUILD_PREFIX = "/opt/EasyBuild"
    EASYBUILD_ROBOT_PATHS = "${WORKSPACE}"
    MODULEPATH = "${EASYBUILD_PREFIX}/modules/all"
    LMOD_PATH = "/opt/lmod/lmod/init/bash"
    }

    stages {
        stage('EasyBuild Tests') {
            steps {
                sh"""
                source ${LMOD_PATH}
                export PYTHONPATH=${WORKSPACE}
                python3 -m venv eb_check
                source eb_check/bin/activate
                pip3 install easybuild-framework easybuild-easyblocks pycodestyle python-graph-core python-graph-dot
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
