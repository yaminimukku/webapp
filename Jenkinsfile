pipeline {
    agent any

    parameters {
        booleanParam(name: 'sonarScan', defaultValue: true, description: 'To run scan in pipeline')
    }

    environment {
        JAVA_HOME = "/usr/lib/jvm/java-11-openjdk-amd64"
        PATH = "$PATH:$JAVA_HOME/bin"
        MVN_SETTINGS = "pipeline/settings.xml"
        SONAR_TOKEN = credentials('sonar-cred')
        GIT_CREDS = credentials('git-cred')
        VERSION = ""
    }

    stages {
        stage("code") {
            steps {
                script {
                    deleteDir()
                    checkout scm
                    echo "success"
                }
            }
        }

        stage("build") {
            steps {
                sh "mvn -s ${MVN_SETTINGS} clean compile"
                echo "build success"
            }
        }

        // Commented-out stage must include closing braces
        // stage("test") {
        //     steps {
        //         sh "mvn -s ${MVN_SETTINGS} test"
        //         echo "test completed"
        //     }
        // }

        stage("scan") {
            when {
                expression {
                    params.sonarScan == true
                }
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh """mvn -s ${MVN_SETTINGS} sonar:sonar \
                        -Dsonar.projectKey=webapp-demo \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=${SONAR_TOKEN}"""
                }
            }
        }
    }
}
