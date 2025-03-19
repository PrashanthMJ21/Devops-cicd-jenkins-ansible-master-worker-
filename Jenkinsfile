pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("Pull SCM") {
            steps {
                git branch:"master",url:"https://github.com/rjn991/Devops-projects.git"
            }
        }
        stage("Prepare build") {
            steps {
                sh "mvn clean package"
            }
        }
        stage("Build image and push to dockerhub") {
            steps {
                script {
                    try {
                        sh "docker rmi rjn991/warimage"
                    }
                    catch(err) {
                        echo err.getMessage()
                    }
                }
                sh '''  mv target/marcos.war .
                        docker build -t rjn991/warimage .
                        docker login -u rjn991 -p $DOCKERHUB_TOKEN
                        docker push rjn991/warimage
                    '''
            }
        }
        stage("Run ansible Playbook") {
            steps {
                sh "ansible-playbook containerize.yml"
            }
        }
        
    }
}
