pipeline {
	options {
		disableConcurrentBuilds()
		timestamps()
	}
	stages {
		stage('build') {
        
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

		}
		cleanup {
			deleteDir()
		}
	}
}