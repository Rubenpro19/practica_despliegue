pipeline {
    agent any

    stages {
        stage('Verificar Docker') {
            steps {
                sh '''
                    echo "Verificando instalación de Docker..."
                    which docker || echo "Docker no encontrado"
                    docker --version || echo "Docker no está disponible"
                '''
            }
        }
        
        stage('Construir Imagen Docker') {
            steps {
                script {
                    sh 'docker build -t hola-mundo-node:latest .'
                }
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                script {
                    sh '''
                        # Detener y eliminar cualquier contenedor previo
                        docker stop hola-mundo-node || true
                        docker rm hola-mundo-node || true

                        # Ejecutar el contenedor de la aplicación
                        docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                    '''
                }
            }
        }
    }
}