pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    parameters{
        string(name: 'version', defaultvalue: '', description: 'version to deploy')
        choice(name: 'version', choices: ['1.1','1.2','1.3'])
        booleanParam(name: 'executetests', defaultValue: true, description: '')
    }
    environment {
        new_version = '1.1.3'
        myserver_credentials = credentials('server-credentials') //for this install 'credentials binding' plugin.
        //server_credentials is a variable, server-credentials is ID
    }

    stages {
        stage('test') {
            when {
                expression {
                    BRANCH_NAME = 'dev' && CODE_CHANGE = True
                }
            }
            steps {
                echo 'testing application'
                echo "version is ${new_version}"
            }
        }
        stage('build') {
            when {
                expression {
                    params.executetests
                }
            }
            steps {
                echo 'building application'
            }
        }
        stage('deploy') {
            steps {
                echo "deploying application version ${version}"
                echo "deploying with ${myserver_credential}"
                sh"${myserver_credential}"
                

            }
        }
    }

}
