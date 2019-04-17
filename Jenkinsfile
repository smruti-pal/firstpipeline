node {
    stage ('SCM checkout')
    checkout([$class: 'GitSCM',
              branches: [[name: '*/master']], 
              doGenerateSubmoduleConfigurations: false, 
              extensions: [], submoduleCfg: [], 
              userRemoteConfigs: [[credentialsId: 'Github_id', url: 'https://github.com/smruti-pal/firstpipeline.git']]])
}
