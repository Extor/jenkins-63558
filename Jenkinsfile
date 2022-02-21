pipeline {
     agent none

     parameters {
        string(
            name: 'BRANCH',
            defaultValue: 'master',
            description: 'Please specify commit, branch, tag'
        )
        // gitParameter defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
    }

    stages {

        stage('Check Jenkinsfile branch') {
            steps {
                echo 'Jenkinsfile read from master branch...'
                echo "${params.BRANCH}"
            }
        }

        stage ('Get code from SCM') {
            agent {
                kubernetes {
                    yamlFile 'WorkerPod.yml'
                }
            }
            options {
                skipDefaultCheckout(true)
            }
            steps {
                container('jenkins-63558') {
                    checkout scm: [
                        $class: 'GitSCM',
                        branches: [[name: "${params.BRANCH}" ]],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [[
                        ]],
                        submoduleCfg: [],
                        userRemoteConfigs:
                        [[
                            url: 'git@github.com:Extor/jenkins-63558.git'
                        ]]
                    ]
                }
            }
        }
    }
}
