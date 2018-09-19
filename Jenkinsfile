pipeline {
    agent any

    stages {
        stage('Build....') {
            steps {
                echo 'Building...'
		sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Testing') {
            steps {
                echo 'Test..'
		sh 'cd /var/lib/jenkins/workspace/assignment/'
		sh 'mvn surefire-report:report -DouputFile=junitreport.html'
            }
        }
	stage('JUnit Test') {
	    steps {
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site/', reportFiles: 'surefire-report.html', reportName: 'HTML Report', reportTitles: ''])
            }
	}
     
	 stage('Deploy') {
            steps {
                echo 'Deploying..'
            }
        }
    }
}
