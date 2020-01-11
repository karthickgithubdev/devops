node {
	def app

	stage('clone repository') {

		/* Clone the repository */

		checkout scm
	}
	
	stage('Build image') {
		/* Build the image based on the source */

		app = docker.build('uploadtodocker/experimenthub')

	}

	stage('Test image') {

		/* Test the image */
		app.inside{
		
			sh 'echo "Test passed"'
		}

	}

	stage('Deploy') {

		/* Push the image to repository*/

		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {

		app.push("${env.BUILD_NUMBER}")
		app.push('latest')
		}
	}
}
