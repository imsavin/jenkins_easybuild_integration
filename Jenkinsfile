pipeline {
    agent any
    parameters {
        string(name: "easyconfig", defaultValue: "", trim: true, description: "введите наименование изиконфига")
    }
    
    environment {
        LMOD_PATH = "/opt/lmod/lmod/init/bash"
        PREFIX = "/home/jenkins"
        EASYBUILD_PREFIX = "${PREFIX}/easybuild"
        SINGULARITY_CONTAINER = "${PREFIX}/containers/easybuild_container.sif
        SINGULARITY_BIND = "${EASYBUILD_PREFIX}"
    }
    
    stages {
        stage('Build') {
            steps {
                sh"""
                    source ${LMOD_PATH}
                    module use ${EASYBUILD_PREFIX}/modules/all
                    module load Apptainer
                    singularity run ${SINGULARITY_CONTAINER} $params.easyconfig -r
                """
            }
        }
        
    }
     post {
          always {
            cleanWs()
        }
    }
 }
