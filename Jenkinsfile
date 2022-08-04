pipeline {
  agent {
    docker { 
      image 'liquibase/liquibase:4.4.2' 
      args '--network=host'
    }    
  }
  environment {
    MYSQL_CRED=credentials('db_mysql')
  }
  stages {
    stage('Status sql') {
      steps {
        sh 'liquibase status --url="jdbc:mysql://127.0.0.1:3306/mydb" --changeLogFile=changelog.mysql.sql --username=$MYSQL_CRED_USR --password=$MYSQL_CRED_PSW'
      }
    }
    /*stage('Update') {
      steps {
        sh 'liquibase update --url="jdbc:mysql://127.0.0.1:3306/mydb" --changeLogFile=my_app-wrapper.xml --username=$MYSQL_CRED_USR --password=$MYSQL_CRED_PSW'
      }
    }*/
    stage('Update sql') {
      steps {
        sh "liquibase status --url='jdbc:mysql://127.0.0.1:3306/mydb' --username=$MYSQL_CRED_USR --password=$MYSQL_CRED_PSW --changeLogFile=changelog.mysql.sql generateChangeLog"
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}