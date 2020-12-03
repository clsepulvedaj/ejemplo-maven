pipeline {
    agent any

    stages {
        stage('Compilar Codigo') {
            steps {
			dir("/home/csepu/ejemplo-maven") {
				sh 'mvn clean compile -e'
			}
            }
        }
        stage('Test Code') {
            steps {
			dir("/home/csepu/ejemplo-maven") {
				sh 'mvn clean test -e'
			}                
            }
        }
        stage('Jar Code') {
            steps {
			dir("/home/csepu/ejemplo-maven") {
				sh 'mvn clean package -e'
			}
            }
        }
        stage('Run Jar') {
            steps {
			dir("/home/csepu/ejemplo-maven") {
				sh 'nohup bash mvn spring-boot:run &'
			}
            }
        }
        stage('Testing Application') {
            steps {
			dir("/home/csepu/ejemplo-maven") {
				sh "curl -X GET 'http://localhost:9090/rest/mscovid/test?msg=testing'"
			}
            }
        }
    }
}
