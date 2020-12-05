pipeline {
    agent any

    stages {
        stage('Compilar Codigo') {
            steps {
                        sh 'mvn clean compile -e'  
            }
        }
        stage('Test Code') {
            steps {
                        sh 'mvn clean test -e'
            }
        }
        stage('Jar Code') {
            steps {
                        sh 'mvn clean package -e'
            }
        }
        stage('Sonar') {
            steps {
			withSonarQubeEnv(installationName: 'SonarLocal_kls') {
				sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
			}      
            }
        }		
        stage('Run Jar') {
            steps {
                        sh 'nohup bash mvn spring-boot:run &'
            }
        }
        stage('Testing Application') {
            steps {
                        sh "curl -X GET 'http://localhost:9090/rest/mscovid/test?msg=testing'"
            }
        }
    }
}
