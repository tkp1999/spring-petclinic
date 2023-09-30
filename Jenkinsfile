pipeline{
    agent { label 'openkdk17' }
    options{
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers{
        pollSCM('* * * * *')
    }
    tools{
        maven 'maven3.9'
        jdk 'JAVA_17'
    }
    stages{
        stage('code get from VCS'){
            steps{
                git branch: 'main',
                    url: 'https://github.com/tkp1999/spring-petclinic.git'

            }
        }
        stage('build and package'){
            steps{
                sh script: 'mvn package'

            }
        }
        stage('reporting'){
            steps{
                archiveArtifacts artifacts: '**/target/springpetclinic-*.jar'
                junit testResults: 'target/surefire-reports/TEST-*.xml'

            }
        }
    }
}