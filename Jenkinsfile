pipeline {
   agent any

   stages {
   
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git 'https://github.com/bdaquasec-scc/updated-bank.git'
        
    }
    stage('Aqua scanner') {
        withCredentials([
          string(credentialsId: 'AQUA_KEY', variable: 'AQUA_KEY'),
          string(credentialsId: 'AQUA_SECRET', variable: 'AQUA_SECRET'),
          string(credentialsId: 'GITHUB_TOKEN', variable: 'GITHUB_TOKEN')
        ]){
          sh '''
            curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin v0.37.1
            export TRIVY_RUN_AS_PLUGIN=aqua
            trivy fs --security-checks config,vuln,secret .
            # Customizing which severities are scanned for is done by adding the following flag: --severity UNKNOWN,LOW,MEDIUM,HIGH,CRITICAL
          '''
        }
      }
    }
