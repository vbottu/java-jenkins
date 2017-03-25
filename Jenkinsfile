pipeline {
  agent none
  
  stages {
    stage('Unit Tests'){
      steps{
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
      }
    }
    
    stage('build') {
      steps {
        sh 'ant -f build.xml -v'
      }
      post{
    success{
      archiveArtifacts artifacts: 'dist/*.jar',fingerprint : true
    }
    
  }
      
    }
    stage('deploy'){
      steps{
        sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all"
      }
    }
    stage('Running on CentOS'){
      agent{
      label 'CentOS'
      }
      steps{
        sh "wget http://vv25591.mylabserver.com/var/www/html/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
      
      }
    }
  }
  
  
}
