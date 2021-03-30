pipeline{
    agent{label 'master'}
    tools{
        maven 'M3'
    }

    stages {
        stage('Checkout'){
            steps{
                 git branch: 'main', url: 'https://github.com/yaminianand/Digital-Bank.git'
            }
        }

        stage('Build'){
            steps{
                 sh 'mvn clean compile'
            }
        }

        stage('Test'){
            steps{
                     sh 'mvn test'
                     junit '**/target/surefire-reports/TEST-*.xml'
            }
        }

        stage('Package'){
            steps{
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
                }
        }

	stage('Deploy'){
            steps{
                input message: 'Do you want to proceed with Deployment? (Click "Proceed" to continue)'   
		sh "sudo docker build . -t yaminianand/digitalbank"
		// sh "sudo docker push yaminianand/digitalbank"
		sh "sudo docker run -d -p 8087:8080 yaminianand/digitalbank"
            }
        } 
   }
}

