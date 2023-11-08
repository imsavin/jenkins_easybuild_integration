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
                . ${LMOD_PATH}
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
