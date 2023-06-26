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
        /*
        stage ("Prueba unitaria"){
            steps{
                sh "npm run test"
            }
        }*/
        stage ("Compilacion de la aplicacion"){
            steps{
                sh "npm run build"
            }
        }
        stage ("Despliegue en dev"){
            steps{
                sh "scp dist/AngularApp/* root@206.189.254.187:/usr/ucreativa/sebas-dev/"
            }
        }
        stage ("Despliegue en staging"){
            steps{
                sh "scp dist/AngularApp/* root@206.189.254.187:/usr/ucreativa/sebas-staging/"
            }
        }
        stage ("Despliegue en prod"){
            steps{
                sh "scp dist/AngularApp/* root@206.189.254.187:/usr/ucreativa/sebas-prod/"
            }
        }
    }

    
}
