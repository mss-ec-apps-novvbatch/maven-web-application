
   node 
   {
   def mavenHome = tool name: "maven3.8.4"
   stage('chechkoutcode')
   {
   git branch: 'development', credentialsId: '1a75dcca-80db-4226-b3cc-28ab48cc4a5e', url: 'https://github.com/mss-ec-apps-novvbatch/maven-web-application.git'
   }
   
   stage ('build') {
   sh "${mavenHome}/bin/mvn clean package"
   }
   stage ('execution') {
   sh "${mavenHome}/bin/mvn clean sonar:sonar"
   }
   stage ('uploadartifactintonexus') {
   sh "${mavenHome}/bin/mvn clean deploy"
   }
   stage ('deployappintoTomcat') {
   sshagent(['2b1fc561-1658-4c8e-a069-31eb09c7f97c']) {
    sh "scp -o  StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.108.193.26:/opt/apache-tomcat-9.0.58/webapps/"}
   }
   
   stage('sendnotifications'){
   emailext body: '''Buildover

       Regards,

        Sudhakar reddy sura''', subject: 'buildover', to: 'sudhakarreddy7300@gmail.com'
   }
 }  
