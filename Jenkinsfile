pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage ("validate") {
            steps{
                sh 'mvn clean validate'
            }
        }
        stage ("Build") {
            steps{
                sh 'mvn clean package'
            }
        }
        stage ("Deploy") {
            steps {
                sh 'mvn -s settings.xml clean deploy'
            }
        }
    }
}
