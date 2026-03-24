ibrary identifier: 'library@master', retriever: modernSCM([
	$class: 'GitSCMSource',
	remote: '/var/share/pipeline-library'
])

node {
	env.PROJECT_NAME = 'v587'
	env.DOCKER_IMAGE = 'rogerdz/shopify:node-22'

	def steps = shopifySteps()
	runPipeline(steps)
}

def shopifySteps() {
	return {
    	stage('Build') {
        	sh "node -v"
        	checkout scm
    	}

    	if (env.BRANCH_NAME.startsWith('PR')) {
        	stage('Validate PR') {
            	prChangedFile()
            	validateNodeCode()
        	}
    	} else {
        	stage('Validate Commit') {
            	commitChangedFile(currentBuild)
            	validateNodeCode()
        	}
    	}
	}
}
