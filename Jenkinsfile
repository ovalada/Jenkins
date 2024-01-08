pipeline {
    agent any

    stages {
        stage('Check Docker') {
            steps {
                script {
                    // Verificar si Docker está instalado
                    def dockerVersion = sh(script: "docker --version", returnStdout: true).trim()
                    echo "Versión de Docker: ${dockerVersion}"
                }
            }
        }

        // Resto del pipeline...
    }
    
    // Post-actions...
}
