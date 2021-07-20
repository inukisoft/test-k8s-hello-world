def MVN_PROFILE="integracion"; // Por default, por el momento sin uso especifico.
def PROPERTIES_PATH=''; // Ruta de las properties descargadas desde Estabilizacion Negocios
def FAIL_BUILD_ON_CVSS = 9; // Nota de seguridad para que el Test Owasp sea fallido. // TODO: Esto debe ir dentro de Jenkins (no modiificable)
def ACCESS_TOKEN_GIT='Sc9zTEQ5KBCcFicezKyt' // change it! Cada proyecto pone su access token (asociado a un usuario)

// Definiendo los proyectos MS (backend) y Front UI
def ms = ['arsii-ms']; // proyectos backend (nombres de directorios)
def ui = ['arsii-ui']; // proyectos front end

@NonCPS
def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}

pipeline {
 
  environment { 
    HTTP_PROXY = 'http://laurel.sii.cl:3128'
    HTTPS_PROXY = 'http://laurel.sii.cl:3128'
    NO_PROXY = 'localhost,127.0.0.1,172.17.0.1,*.sii.cl'

    NEXUS_VERSION = "nexus3"
    NEXUS_PROTOCOL = "http"
    NEXUS_URL = "apus.sii.cl:8081"
    NEXUS_REPOSITORY = "sii-repo-releases"
    NEXUS_CREDENTIAL_ID = "nexus-user-deploy"    
  }

  agent any
  
  stages {
    
    stage('Test Jira') {
      steps {
        script {
            echo "hola mundo !" 
            jiraSendBuildInfo site: 'inukisoft.atlassian.net'
        }
      }
    }
  }


post {
    always {
        jiraSendDeploymentInfo site: 'inukisoft.atlassian.net', environmentId: 'us-prod-1', environmentName: 'us-prod-1', environmentType: 'production'
        jiraSendBuildInfo site: 'inukisoft.atlassian.net'
    }
}


}
