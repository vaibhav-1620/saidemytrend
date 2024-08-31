pipeline {
    // Specify the agent to run the pipeline
    agent any
    // Set environment variables for the pipeline
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    // Define the stages of the pipeline
    stages {
        // Stage for checking out the repository
        stage("github clone") {
            steps {
                //clone the github repo
		git url: 'https://github.com/vaibhav-1620/saidemytrend.git', branch: 'main'
            }
        }

        // Stage for building the project
        stage("build") {
            steps {
                // Run Maven
                sh 'mvn clean deploy'
          }
        }

        // Stage for SonarQube analysis
        stage('SonarQube analysis') {
            environment {
                // Set the SonarQube scanner tool
                scannerHome = tool 'vaibhav-sonar-scanner'
            }
            steps {
                // Execute SonarQube analysis within the SonarQube environment
                withSonarQubeEnv('vaibhav-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
       
    }
}

