pipeline{
    agent {
        label "linux-agent"
    }
    /*
    environment {
        AWS_ACCESS_KEY_ID = credentials {'AWS_ACCESS_KEY_ID'}
        AWS_SECRET_ACCESS_KEY_ID = credentials {'AWS_SECRET_ACCESS_KEY_ID'}
        AWS_DEFAULT_REGION = 'us-east-1'
    }*/

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
        stage ("Deploy al servidor"){
            steps{
                sh 'sh "scp dist/AngularApp/* root@206.189.254.187:/usr/ucreativa/sebas-prod/"'
            }
        }

        /*
        when (branch 'dev'){
            steps{
                sh "cp dist/AngularApp/* root@206.189.254.187:/usr/ucreativa/sebas-dev/""
            }
        }
        /*when (branch 'staging'){
            steps{
                sh "cp dist/AngularApp/* root@206.189.254.187:/usr/ucreativa/sebas-staging/"
            }
        }
        when (branch "main"){
            steps{
                sh "cp dist/AngularApp/* root@206.189.254.187:/usr/ucreativa/sebas-prod/"
            }
        }*/
        
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
