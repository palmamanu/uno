pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            echo 'Building...'
            sh 'npm install'
            task 'tarea1'
            pwd(tmp: true)
          }
        }
        stage('prueba2') {
          steps {
            echo 'hola'
            sh '/usr/bin/ansible-playbook /tmp/apache.yml'
          }
        }
        stage('tomcat') {
          steps {
            sh '/usr/bin/ansible-playbook /tmp/tomcat.yml'
          }
        }
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            echo 'Testing...'
          }
        }
        stage('copia estaticos') {
          steps {
            pwd(tmp: true)
            sh 'scp /tmp/lala* root@10.28.107.98:/var/www'
          }
        }
        stage('error') {
          environment {
            prod = 'prod'
          }
          steps {
            sleep 12
            sh '/usr/bin/ansible-playbook /tmp/tomcat.yml'
          }
        }
      }
    }
    stage('Testeadoya') {
      steps {
        echo 'Testing...'
      }
    }
  }
}