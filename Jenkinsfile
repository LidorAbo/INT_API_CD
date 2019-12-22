//@Library('Utilities') _
import groovy.json.JsonSlurper
import hudson.model.*
def Current_version
def NextVersion
def dev_rep_docker = 'lidorabo/docker_repo'
def colons = ':'
def module = 'intapi'
def underscore = '_'
def path_json_file
pipeline {

    options {
        timeout(time: 30, unit: 'MINUTES')
    }
    agent { label 'master' }
    stages {
        stage('Checkout') {
            steps {
                script {
                        dir('Release') {
                            deleteDir()
                            checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-cred', url: "https://github.com/lidorabo/Release.git"]]])
                            path_json_file = sh(script: "pwd", returnStdout: true).trim() + '/' + 'dev' + '.json'
                            Current_version = Return_Json_From_File("$path_json_file").Services.INT_API

                        }
                    dir('Deployment') {
                        deleteDir()
                        checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-cred', url: "https://github.com/lidorabo/INT_API_CD.git"]]])
                        echo Current_version
                    }


                }
            }
        }
    }

}
def Return_Json_From_File(file_name){
    return new JsonSlurper().parse(new File(file_name))
}