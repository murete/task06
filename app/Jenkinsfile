pipeline {
    agent any

    environment {
        APACHE_ROOT = "${WORKSPACE}/public"
        DOCS_DIR = "${WORKSPACE}/docs"
    }

    stages {
        stage('Prepare Directories') {
            steps {
                script {
                    // Crear directorios necesarios
                    sh "mkdir -p ${APACHE_ROOT}"
                    sh "mkdir -p ${DOCS_DIR}"
                }
            }
        }

        stage('Deploy (Local Copy)') {
            steps {
                script {
                    // Copiar archivos del repositorio al directorio "public"
                    sh "cp -R * ${APACHE_ROOT}"
                }
            }
        }

        stage('Generate Documentation') {
            steps {
                script {
                    // Generar documentación con phpDocumentor
                    sh "phpdoc -d ${APACHE_ROOT} -t ${DOCS_DIR}"
                }
            }
        }
    }

    post {
        success {
            echo "Deployment and documentation generation successful."
        }
        failure {
            echo "Deployment or documentation generation failed."
        }
        always {
            // Mostrar contenido generado (opcional para debug)
            sh "ls -la ${APACHE_ROOT}"
            sh "ls -la ${DOCS_DIR}"
        }
    }
}
