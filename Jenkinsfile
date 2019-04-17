properties([parameters([choice(choices: 'master\ntest', description: 'Select branch to build', name: 'choice')])])
node {
    stage ('SCM checkout'){
        echo "Pulling changes from the branch ${params.choice}"
    checkout([$class: 'GitSCM', branches: [[name: '*/master'], [name: '*/test']], 
              doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [],
              userRemoteConfigs: [[credentialsId: 'Github_id', url: 'https://github.com/smruti-pal/firstpipeline.git']]])
    }
    stage ('build'){ 
      bat "mvn clean install"
    }
    stage('SonarQube Analysis') {
        
        withSonarQubeEnv('SonarQube_Server') { 
          bat "mvn sonar:sonar"
        }
    }
        stage('email'){
        emailext body: 'sfsfs', recipientProviders: [developers()], subject: 'dghsfs', to: 'palsmrutiranjan001@gmail.com'
        }
    stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
              echo "Quality gate is successful."
          }
      }        
    
}
