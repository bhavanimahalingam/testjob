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
      sshagent(['jenkins_cat']) {
      sh 'scp -o StrictHostKeyChecking=no target/*.war  ec2-user@3.95.10.198:/home/ec2-user/apache-tomcat-9.0.36/webapps/'
      }
  }
   node {
    stage('test advance script') {
            echo "current build number: ${currentBuild.number}"
            echo "previous build number: ${currentBuild.previousBuild.getNumber()}"
            def causes = currentBuild.rawBuild.getCauses()
            echo "causes: ${causes}"
            def rebuildCause0 = currentBuild.rawBuild.getCause(com.sonyericsson.rebuild.RebuildCause)
            echo "rebuildCause0: ${rebuildCause0}"
            echo "rebuild up number: ${rebuildCause0.getUpstreamBuild()}"
        }
}
    stage('Deploy to airflow'){
     sshagent(['jenkins_cat']) {
      sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/bavani_pipeline/*.py  ec2-user@3.95.10.198:/home/ec2-user/airflow/dags/'
      sh "pwd"
      sh "whoami"
     dir('/home/ec2-user/airflow/'){
      sh 'airflow scheduler & airflow webserver -p 8080 '
      sh 'pwd'
    }
    }
   
    }
    stage('Email Notification'){
      mail bcc: '', body: '''Hi Welcome to jenkins email alerts
      Thanks
      bhavani''', cc: '', from: '', replyTo: '', subject: 'Jenkins Job', to: 'bavani15799@gmail.com'
   }
}
   
 
