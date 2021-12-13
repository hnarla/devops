pipeline { 
    agent any  
    tools { 
        maven 'mvn_3.6.0' 
        jdk 'jdk11' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                   '''
            }
        }
        stage ('Build') {
            steps {
			    echo "Running Maven build"
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
            post {
                success {
                    echo "Testing cases"
                }
            }
        }
        stage ('Scan') {
            steps {
			    echo "sonar scan"
                sh 'mvn -Dmaven.test.failure.ignore=true sonar:sonar -Dsonar.login=sonar-token' 
            }
            post {
                success {
                    echo "sonar completed"
                }
            }
        }
    }
}