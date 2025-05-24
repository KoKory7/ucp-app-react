pipeline {
    agent any
    tools {
        nodejs 'Node_24'  // Nombre definido en Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/KoKory7/ucp-app-react.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build' // Ejecuta el build de React
            }
        }

        // Etapa 2: Instalar dependencias y build del proyecto
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build' // Ejecuta el build de React
            }
        }

        // Etapa 3: Ejecutar pruebas unitarias
        stage('Pruebas Unitarias') {
            steps {
                sh 'npm test -- --watchAll=false --ci --reporters=default --reporters=jest-junit' // Genera reporte JUnit
            }
        }
    }

    post {
        always {
            junit 'junit.xml' // Publica reporte en Jenkins
            archiveArtifacts artifacts: 'junit.xml', allowEmptyArchive: true
        }

        // Post-actions (opcional)
        always {
            emailext(
                subject: "Pipeline ${currentBuild.result}: ucp-app-react #${env.BUILD_NUMBER}",
                body: """Estado: ${currentBuild.result}
URL Build: ${env.BUILD_URL}
Detalles de Pruebas: ${env.BUILD_URL}testReport/""",
                to: 'kcifuentesmonsalve@gmail.com' // Reemplaza con tu email
            )
        }
    }
}
