node
       {
	     def mavenHome = tool name: "maven3.8.6"
		 stage('checkOutCode')
		 {
		  git branch: 'development', credentialsId: '209eec3b-1934-445a-8fff-1b3e73bee51d', url: 'https://github.com/new-fork-organization/maven-web-application.git'
		  }
		  stage('Build')
		  {
		   sh "${mavenHome}/bin/mvn clean package"
		   }
		   stage('Execute sonar qube repoer')
		  {
		   sh "${mavenHome}/bin/mvn clean sonar:sonar"
		   }
		   stage('upload Artifacts')
		  {
		   sh "${mavenHome}/bin/mvn clean deploy"
		   }
		   stage('Deploy Application')
		  {
		   sshagent(['6e6c086d-a8b4-4752-8226-48cf56741745']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.90.2.92:/opt/apache-tomcat-9.0.64/webapps/"
}
       }
       stage( "Send Notification"){
emailext body: '''Bulid Over

Regards,
Sreenivasulu N''', subject: 'Build Over', to: 'sreenu114.tmk@gmail.com'
}
       }
