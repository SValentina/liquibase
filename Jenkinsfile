pipeline {
  agent {
    docker { image 'liquibase/liquibase:4.4.2' }
  }
  environment {
    MYSQL_CRED=credentials('db_mysql')
  }
  stages {
    stage('Status') {
      steps {
        sh 'liquibase status --url="jdbc:mysql://127.0.0.1:3306/mydb" --changeLogFile=my_app-wrapper.xml --username=$MYSQL_CRED_USR --password=$MYSQL_CRED_PSW'
      }
    }
    /*stage('Update') {
      steps {
        sh 'liquibase update --url="jdbc:mysql://127.0.0.1:3306/mydb" --changeLogFile=my_app-wrapper.xml --username=$MYSQL_CRED_USR --password=$MYSQL_CRED_PSW'
      }
    }*/
    stage('Update sql') {
      steps {
        sh 'liquibase update --url="jdbc:mysql://127.0.0.1:3306/mydb" --username=$MYSQL_CRED_USR --password=$MYSQL_CRED_PSW --changeLogFile=changelog.sql generateChangeLog'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}