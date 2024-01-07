pipeline {
    agent any

    stages {
        stage('Preparation') {
            steps {
                script {
                    // Instalar Docker si no está presente
                    def dockerInstallation = tool 'docker'
                    if (dockerInstallation == null) {
                        echo 'Docker no está instalado. Instalando...'
                        def installer = getDockerInstaller()
                        installer.install()
                        echo 'Docker instalado exitosamente.'
                    } else {
                        echo 'Docker ya está instalado.'
                    }
                }
            }
        }

        // Resto del pipeline...
    }
    
    // Post-actions...
}

def getDockerInstaller() {
    // Puedes ajustar la versión según tus necesidades
    def version = '20.10.9'
    def installer = new DockerInstaller(version)
    return installer
}

class DockerInstaller {
    def version

    DockerInstaller(version) {
        this.version = version
    }

    def install() {
        // Instalación de Docker según la plataforma
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
