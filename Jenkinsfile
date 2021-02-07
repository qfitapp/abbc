node('maven-label'){
   
    def mvnHome
    stage('Preparation') { // for display purposes
      
        git 'https://github.com/qfitapp/abbc.git'
        
        mvnHome = tool 'maven-3.6.3'
    }
    stage('Build') {
       
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package sonar:sonar -Dsonar.host.url=http://ec2-13-127-157-193.ap-south-1.compute.amazonaws.com:9000/'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
    }
}
