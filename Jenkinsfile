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
        stage('collect') {
            steps {
                recordIssues tools: [spotBugs(pattern: 'spotbugs_*.xml', useRankAsPriority: true)], qualityGates: [[threshold: 1, type: 'NEW', unstable: true]], blameDisabled: true
                recordIssues tools: [pmdParser(pattern: 'report_*.xml')], qualityGates: [[threshold: 1, type: 'NEW', unstable: true]], blameDisabled: true
                recordIssues tools: [java()], filters: [includePackage('com\\.wago\\..*'), excludePackage('.*\\.(constants|jalo).*')], qualityGates: [[threshold: 10, type: 'NEW', unstable: true]], blameDisabled: true
                recordIssues tools: [cpd(pattern: 'cpd_*.xml')], blameDisabled: true
                recordIssues tools: [checkStyle(pattern: 'report_*.xml')], blameDisabled: true         
            }
        }
    }
	post {
		unstable {
			emailext body: '${SCRIPT,template="email.template"}', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'foo@bar.de'
		}
		failure {
			emailext body: '${SCRIPT,template="email.template"}', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'foo@bar.de'
		}
        always {
			emailext body: '${SCRIPT,template="email.template"}', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'foo@bar.de'
		}
	}
}