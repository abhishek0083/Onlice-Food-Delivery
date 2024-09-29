pipeline {
    agent any

    tools {
        maven 'MVN'  // Ensure this matches your Maven installation name in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git url: 'https://github.com/abhishek0083/Onlice-Food-Delivery.git', branch: 'main'
            }
        }

        stage('Generate Maven Project') {
            steps {
                // Generate a basic Maven project with a `pom.xml` file
                bat 'mvn archetype:generate -DgroupId=com.example -DartifactId=online-food-delivery -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false'
            }
        }

        stage('Move POM') {
            steps {
                // Move the generated `pom.xml` to the root directory
                bat 'move online-food-delivery\\pom.xml .'
                // Optionally, delete the generated project folder
                bat 'rmdir /S /Q online-food-delivery'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add your deployment steps here
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            cleanWs()
        }
    }
}
