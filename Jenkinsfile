pipeline {
  agent {
  node { label 'nodejs-apic' } 
  } 
  environment {
    APIC_DEV_CREDS = credentials('jenkins-apic-dev-creds')
  }
  stages {
   stage('Login to APIC') {
      steps {
        // login

        echo '############################################################################################################################'
        echo '########################################ß      Login to APIC Connect         ################################################'
        echo '############################################################################################################################'

        sh "apic-slim login --username ${env.APIC_DEV_CREDS_USR} --password ${env.APIC_DEV_CREDS_PSW} --server https://mgmt.icp-proxy.project-fidelity-uk-3cd0ec11030dfa215f262137faf739f1-0000.eu-gb.containers.appdomain.cloud --realm provider/default-idp-2"
        
      }
    }
       

     stage('clone') {
         when {
          expression {
            env.BRANCH_NAME =~ /^.*(clone).*$/
        }
       }
      steps {
        //deploy to environment
        echo '############################################################################################################################'
        echo '########################################      Clone from Dev environment         ############################################ß'
        echo '############################################################################################################################'
        sh "apic-slim products clone hello-world-product.yaml --server https://mgmt.icp-proxy.project-fidelity-uk-3cd0ec11030dfa215f262137faf739f1-0000.eu-gb.containers.appdomain.cloud --org fidelity-integration --catalog fidelity-dev"
      }
    }
  }
  }
