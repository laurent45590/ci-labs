de votre espace de stockage. Il vous sera bientôt impossible d'envoyer et de recevoir des e-mails, sauf si vous libérez de l'espace ou si vous achetez de l'espace supplémentaire. Un délai maximal de 24 heures peut être nécessaire pour que ces modifications soient appliquées à votre espace de stockage.
Meet
Nouvelle réunion
Rejoindre une réunion
Hangouts
1 sur 24 237
Re: Support de cours
Boîte de réception
soufiene BEN JAMAA
	
	Pièces jointes10:10 (il y a 4 heures)
Le lun. 14 févr. 2022 à 17:16, soufiene BEN JAMAA <benjamaasoufiene@gmail.com> a écrit : https://form.dragnsurvey.com/survey/r/3903f60a Le lun. 14 févr. 2022 à
2
soufiene BEN JAMAA
	
	Pièces jointes14:10 (il y a 33 minutes)
Le mar. 15 févr. 2022 à 12:17, soufiene BEN JAMAA <benjamaasoufiene@gmail.com> a écrit : Le mar. 15 févr. 2022 à 11:54, soufiene BEN JAMAA <benjamaasoufiene@gma
soufiene BEN JAMAA <benjamaasoufiene@gmail.com>
	
Pièces jointes14:41 (il y a 1 minute)
	
À pauline.malosse, laurent.david, moi
   
Traduire le message
Désactiver pour : anglais
Zone contenant les pièces jointes
	
	
	

pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            parallel {
                stage('Compile') {
                    agent {
                        docker {
                            image 'maven:3.6.0-jdk-8-alpine'
                            reuseNode true
                        }
                    }
                    steps {
                        sh ' mvn clean compile'
                    }
                }
                stage('CheckStyle') {
                    agent {
                        docker {
                            image 'maven:3.6.0-jdk-8-alpine'
                            args '-v /root/.m2/repository:/root/.m2/repository'
                            reuseNode true
                        }
                    }
                    steps {
                        sh ' mvn checkstyle:checkstyle'
                    }
                    post {
                        always {
                            recordIssues enabledForFailure: true, tool: checkStyle()
                        }
                    }
                }
            }
        }
        stage('Unit Tests') {
            when {
                anyOf { branch 'master'; branch 'develop' }
            }
            agent {
                docker {
                    image 'maven:3.6.0-jdk-8-alpine'
                    args '-v /root/.m2/repository:/root/.m2/repository'
                    reuseNode true
                }
            }
            steps {
                sh ' mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
        }
    }
}
