pipeline {
    agent any

    environment {
        DOCKER_HOME = tool 'docker'
    }

    stages {
        stage('Preparation') {
            steps {
                script {
                    // Verificar si Docker está instalado
                    if (DOCKER_HOME == null) {
                        echo 'Docker no está instalado. Instalando...'
                        def installer = new DockerInstaller('20.10.9')
                        installer.install()
                        echo 'Docker instalado exitosamente.'
                        
                        // Configurar la variable de entorno DOCKER_HOME
                        DOCKER_HOME = tool 'docker'
                    } else {
                        echo 'Docker ya está instalado.'
                    }
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    // Asegurarse de que DOCKER_HOME esté configurado
                    if (DOCKER_HOME == null) {
                        error 'Docker no está instalado. Deteniendo el pipeline.'
                    }

                    // Resto de las acciones para construir la imagen Docker...
                    echo 'Construyendo la imagen Docker...'
                    sh "${DOCKER_HOME}/bin/docker build -t testingovalada/realtime_ping:latest ."
                }
            }
        }

        // Agregar más etapas según sea necesario...

        stage('Cleanup') {
            steps {
                script {
                    // Limpiar después de completar el pipeline...
                    echo 'Limpiando...'
                    sh "${DOCKER_HOME}/bin/docker rmi testingovalada/realtime_ping:latest"
                }
            }
        }
    }

    // Post-actions...
}

class DockerInstaller {
    def version

    DockerInstaller(version) {
        this.version = version
    }

    def install() {
        script {
            if (isUnix()) {
                sh "curl -fsSL https://get.docker.com -o get-docker.sh"
                sh "sh get-docker.sh"
            } else {
                bat "curl -fsSL https://get.docker.com -o get-docker.cmd"
                bat "call get-docker.cmd"
            }
        }
    }
}

def isUnix() {
    return !isWindows()
}

def isWindows() {
    return (isAnyOf('windows', 'win32', 'win64', 'cygwin'))
}

def isAnyOf(...candidates) {
    def current = System.properties['os.name'].toLowerCase()
    return candidates.any { candidate -> current.contains(candidate) }
}
