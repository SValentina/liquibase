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
        sh 'liquibase status --url="jdbc:mysql://20.123.136.162:3306/mydb" --changeLogFile=my_app-wrapper.xml --username=$MYSQL_CRED_USR --password=$MYSQL_CRED_PSW'
      }
    }
    stage('Update') {
      steps {
        sh 'liquibase update --url="jdbc:mysql://20.123.136.162:3306/mydb" --changeLogFile=my_app-wrapper.xml --username=$MYSQL_CRED_USR --password=$MYSQL_CRED_PSW'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}