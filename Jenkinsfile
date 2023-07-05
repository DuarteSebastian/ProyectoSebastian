pipeline{
    agent {
        label "linux-agent"
    }

    stages{

        stage("aprobar despliegue"){
            input{
                message "¿Desea comenzar el despliegue?"
                ok "Correcto"
            }
            steps{
              echo "comenzando deploy"
            }
        }

        stage("Intalacion de dependencias"){
            steps{
                sh "npm install"
            }
        }
        
        stage ("Prueba unitaria"){
            steps{
                echo "comando de las pruebas unitarias npm run test"
            }
        }

        stage('Pruebas de seguridad-sonarqube'){
            steps{
                withSonarQubeEnv('SonarQubeCursoCI'){
                    sh "/opt/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=AngularApp"
                }
            }
        }

        stage ("Compilacion de la aplicacion"){
            steps{
                sh "npm run build"
            }
        }

        stage ("Carpetas"){
            steps{
                sh 'ls -la dist/'
            }
        }

        stage ("Deploy al servidor"){
            steps{
                sh 'scp dist/angular-app/* root@206.189.254.187:/usr/ucreativa/sebas-prod/'
            }
        }
        
    }

    post{
        success {
            emailext body: "La prueba ha finalizado con exito", subject: "Aviso", to: "sebasucreativa123@gmail.com"
        }
        failure {
            emailext body: "La prueba no finalizo con exito", subject: "Aviso", to: "sebasucreativa123@gmail.com"
        }
     }

    
}
