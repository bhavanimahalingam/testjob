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
   stage('Test'){
      def mvn_home = 'maven'
    withEnv( ["PATH+MAVEN=${tool mvn_home}/bin"] ) {
      sh "mvn test"
    }
   }
   stage('Deploy to Tomcat'){
      sshagent(['jenkinstom']){
      sh 'scp -o StrictHostKeyChecking=no target/*.war  ec2-user@174.129.108.233:/home/ec2-user/apache-tomcat-9.0.36/webapps/'
      }
  }
    stage('Email Notification'){
      mail bcc: '', body: '''Hi Welcome to jenkins email alerts
      Thanks
      bhavani''', cc: '', from: '', replyTo: '', subject: 'Jenkins Job', to: 'bavani15799@gmail.com'
   }
}
   
 
