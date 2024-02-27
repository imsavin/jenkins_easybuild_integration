pipeline {
    agent any
    parameters {
        string(name: "easyconfig", defaultValue: "", trim: true, description: "введите наименование изиконфига")
    }
    
    environment {
        LMOD_PATH = "/opt/lmod/lmod/init/bash"
        LOCAL_PREFIX = "/home/jenkins"
        EASYBUILD_PREFIX = "${LOCAL_PREFIX}/easybuild"
        SINGULARITY_CONTAINER = "${LOCAL_PREFIX}/containers/easybuild_container.sif"
        SINGULARITY_BIND = "${EASYBUILD_PREFIX}"
    }
    
    stages {
        stage('Build') {
            steps {
                sh"""
                    source ${LMOD_PATH}
                    module use ${EASYBUILD_PREFIX}/modules/all
                    module load Apptainer
                    singularity run ${SINGULARITY_CONTAINER} $params.easyconfig --job --job-cores=16 --job-backend-config ./gc3pie.conf -r -l
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
