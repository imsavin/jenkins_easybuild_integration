pipeline {
    agent local
    parameters {
        string(name: "easyconfig", defaultValue: "", trim: true, description: "введите наименование изиконфига")
    }
    
    environment {
        LMOD_PATH = "/opt/lmod/lmod/init/bash"
        LOCAL_PREFIX = "/home/jenkins"
        EASYBUILD_PREFIX = "${LOCAL_PREFIX}/easybuild"
        SINGULARITY_CONTAINER = "${LOCAL_PREFIX}/containers/easybuild_container.sif"
        SINGULARITY_BIND = "${EASYBUILD_PREFIX},${EASYBUILD_PREFIX}/CUDA/logs:/var/log,${EASYBUILD_PREFIX}/CUDA/desktopfiles:/usr/share/applications,${EASYBUILD_PREFIX}/CUDA/bin:/usr/local/"
    }
    
    stages {
        stage('Prepare') {
            steps {
                sh"""
                    mkdir -p  ${EASYBUILD_PREFIX}/CUDA/logs ${EASYBUILD_PREFIX}/CUDA/bin ${EASYBUILD_PREFIX}/CUDA/desktopfiles
  		"""
            }
    	}
        stage('Build') {
            steps {
                sh"""
                    source ${LMOD_PATH}
                    module use ${EASYBUILD_PREFIX}/modules/all
                    module load EasyBuild
                    # singularity run ${SINGULARITY_CONTAINER} $params.easyconfig --job --job-output-dir ${EASYBUILD_PREFIX}/job_output  --job-backend-config ./gc3pie.conf -r -l --accept-eula-for=CUDA
                    eb -r -f -l --accept-eula-for='CUDA,Intel-oneAPI,NVHPC'  $params.easyconfig 
                    """
            }
        }
     } 
     post {
          always {
             sh"""
                    rm -rf ${EASYBUILD_PREFIX}/CUDA/*
  	     """
            cleanWs()
        }
    }
 }
