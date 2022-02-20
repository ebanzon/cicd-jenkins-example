pipeline {

    agent any

    stages {

        stage ('Build') {
            steps {
                withMaven() {
                    sh 'mvn clean package'
                }
            }
        }

        stage ('Deploy') {
            steps {

                withCredentials([[$class          : 'UsernamePasswordMultiBinding',
                                  credentialsId   : 'PCF_LOGIN',
                                  usernameVariable: 'USERNAME',
                                  passwordVariable: 'PASSWORD']]) {

                    sh 'cf login -a https://api.us-south.cf.cloud.ibm.com -u $USERNAME -p $PASSWORD'
					sh 'cf target -o ernie@emansoft.com -s release'
                    sh 'cf push'
                }
            }

        }

    }

}