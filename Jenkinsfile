node{
    
    //properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), 
    
    //pipelineTriggers([pollSCM('* * * * *')])])
    
    def mavenHome=tool name: "maven3.8.4"

stage('CheckoutCode'){
git branch: 'development', credentialsId: 'c3fa4962-5861-4b6c-bf09-611675677e60', url: 'https://github.com/Devops-subba90/maven-web-application.git'

}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"

}

stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"

}

stage('UploadArtifactIntoNexusRepo'){
sh "${mavenHome}/bin/mvn deploy"

}

stage('DeployAppintoTomcatServer')
{sshagent(['81f4f259-3c19-491b-8f88-ad6233159d61']) {
   sh "scp -o Stricthostkeychecking=no target/maven-web-application.war ec2-user@13.126.145.157:/opt/apache-tomcat-9.0.56/webapps/"
}

}




}//closing node
