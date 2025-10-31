pipeline {
    agent any

    stages {
        
        stage('Checkout') {
            steps {
                git 'https://github.com/CesarEduardoCeronM/express-pokemonsApiJenkins.git'
            }
        }

        stage('Build') {
            steps {
                echo "Construyendo la imagen Docker..."
                sh 'docker build -t pokemon-api:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo "Desplegando la aplicación..."
                sh  '''                 
                    docker stop pokemon-app-container || true
                    
                    docker rm pokemon-app-container || true
                
                    docker run -d --name pokemon-app-container -p 8080:3000 pokemon-api:latest
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline terminado."
            sh 'docker stop pokemon-app-container || true'
            sh 'docker rm pokemon-app-container || true'
        }
    }
}
