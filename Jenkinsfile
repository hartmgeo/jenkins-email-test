pipeline {
	options {
		disableConcurrentBuilds()
	}
	agent any
	stages {
		stage('build') {
			steps {
				echo "foo bar"
			}
        
        }
    }
	post {
		unstable {
			emailext body: '${SCRIPT,template="email.template"}', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', recipientProviders: [culprits()]
		}
		failure {
			emailext body: '${SCRIPT,template="email.template"}', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', recipientProviders: [culprits()]
		}
        always {
			emailext body: '${SCRIPT,template="email.template"}', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', recipientProviders: [culprits()]
		}
	}
}