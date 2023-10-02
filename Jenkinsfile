pipeline{
    agent { label 'openkdk17' }
    options{
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers{
        pollSCM('H/5 * * * *')
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
                rtMavenDeployer (
                    id: "SPC_DEPLOYER",
                    serverId: "MY_FREE_JFROG",
                    releaseRepo: 'qt-app-libs-release',
                    snapshotRepo: 'qt-app-libs-release'
                )
                 rtMavenRun (
                    tool: 'maven3.9', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "SPC_DEPLOYER",
                   // buildName: "${JOB_NAME}"
                  //  buildNumber: "${BUILD_ID}"
                    
                )
                 rtPublishBuildInfo (
                    serverId: "MY_FREE_JFROG"
                )
                sh script: 'mvn package'

            }
        }
        stage('reporting'){
            steps{
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar'
                junit testResults: 'target/surefire-reports/TEST-*.xml'

            }
        }
    }
}