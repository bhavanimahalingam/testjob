node{
   
   stage('SCM Checkout'){
     git 'https://github.com/bhavanimahalingam/testjob'
   }
   stage('Compile-Package'){
      // Get maven home path
    def mvn_home = 'maven'
    withEnv( ["PATH+MAVEN=${tool mvn_home}/bin"] ) {
     sh "mvn clean install"
    }
   }
   stage('Deploy to Tomcat'){
      sshagent(['jenkins_cat']){
      sh 'scp -o StrictHostKeyChecking=no target/*.war  ec2-user@35.174.208.62:/home/ec2-user/apache-tomcat-7.0.104/webapps/'
      }
  }
    stage('Email Notification'){
      mail bcc: '', body: '''Hi Welcome to jenkins email alerts
      Thanks
      bhavani''', cc: '', from: '', replyTo: '', subject: 'Jenkins Job', to: 'bavani15799@gmail.com'
   }
}
   
 
