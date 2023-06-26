pipeline{
    agent any

    stages{

        stage("aprobar despliegue"){
            input{
                message "¿Desea comenzar el despliegue?"
                ok "Si"
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
                sh "npm run test"
            }
        }
        stage ("Compilacion de la aplicacion"){
            steps{
                sh "npm run build"
            }
        }
    }

    
}
