pipeline {
    agent any
    tools {
        jdk 'JDK21'         // Asegúrate que esta es la configuración de JDK en Jenkins Tools
        maven 'Maven-3.9'   // Asegúrate que esta es la configuración de Maven en Jenkins Tools
    }
    stages {
        stage('Verificar Maven y Java') {
            steps {
                bat '''
                echo ===== Verificación del entorno =====
                echo JAVA_HOME=%JAVA_HOME%
                java -version
                echo -------------------------------
                echo MAVEN_HOME=%MAVEN_HOME%
                mvn -v
                echo =====================================
                '''
            }
        }

        stage('Checkout código') {
            steps {
                // Reemplaza con tu URL de repositorio en GitHub
                git 'https://github.com/NatalyAvila20/test-app.git'
            }
        }

        stage('Compilar y Testear') {
            steps {
                bat 'mvn clean test'
            }
        }

        stage('Empaquetar') {
            steps {
                bat 'mvn package'
                // Archiva el archivo JAR generado en la carpeta target
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Despliegue simulado') {
            steps {
                bat 'if not exist C:\\deploy mkdir C:\\deploy'
                bat 'copy target\\*.jar C:\\deploy'
            }
        }
    }
    post {
        success {
            echo '✅ Pipeline ejecutado correctamente'
        }
        failure {
            echo '❌ Fallo en alguna etapa del pipeline'
        }
    }
}
