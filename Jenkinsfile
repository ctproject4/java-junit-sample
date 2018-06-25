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
		sh 'mvn surefire-report:report -DouputFile=YourFileName.html'
            }
        }
	stage('JUnit Test') {
	    steps {
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/site/', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
            }
	}
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
