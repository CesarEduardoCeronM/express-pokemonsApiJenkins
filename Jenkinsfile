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
                bat 'docker build -t pokemon-api:latest .'
            }
        }

        stage('Deploy') {
            steps {
                echo "Desplegando la aplicación..."
                bat  '''                 
                    docker stop pokemon-app-container
                    
                    docker rm pokemon-app-container
                
                    docker run -d --name pokemon-app-container -p 8081:8081 pokemon-api:latest
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline terminado."
        }
    }
}
