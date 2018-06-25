pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
		sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
		sh 'cd /var/lib/jenkins/workspace/assignment/'
		sh 'mvn surefire-report:report -DouputFile=junitreport.html'
            }
        }
	stage('JUnit Test') {
	    steps {
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site/', reportFiles: 'surefire-report.html', reportName: 'HTML Report', reportTitles: ''])
            }
	}
	try {
		stage("Building SONAR ...") {
			sh './gradlew clean sonarqube'
			}
		} catch (e) {emailext attachLog: true, body: 'See attached log', subject: 'BUSINESS Build Failure', to: 'abc@gmail.com'
		step([$class: 'WsCleanup'])
		return
	}	
        
	 stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
