@Library("shared-library") _

node {
    // Define the build number with fallback if not set
    //def buildNumber = "${env.BUILD_NUMBER ?: 'local-build'}"
    //echo "Build Number: ${buildNumber}"
    def buildNumber = env.BUILD_NUMBER ?: 'local-build'
    echo "Build Number: ${buildNumber}"
    
    // Call mavenBuild function with parameters
    //mavenBuild {
    //    branch = 'main'
    //    repoUrl = 'https://github.com/tkp1999/ansible_zone.git'
    //    buildNumber = buildNumber
    //}
    mavenBuild {
        branch = 'main'
        repoUrl = 'https://github.com/tkp1999/spring-petclinic.git'
        //jdkVersion = "JDK17" 
        jdkVersion = "JDK11" 
        //mavenVersion = "Maven3.9"
        mavenVersion = "Maven3.6"
        dockerRegistry = "tkp1999"
        imageName = "spring-app-shared_library"
        dockerCredentialsId = "docker-credentials"
        //buildNumber = buildNumber
    }
}