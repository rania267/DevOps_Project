pipeline {
    agent any

    stages {
         stage('Run All Containers') {
                            steps {
                                sh 'docker start nexus grafana prometheus sonarqube'
                            }
                        }
           stage('Checkout GIT') {
            steps {

            git branch: 'main', url: 'https://github.com/rania267/DevOps_Project'
        }}

    stage('Maven Clean') {
            steps {
                sh 'mvn clean'
            }
        }
        stage('MVN COMPILE') {
            steps{

                sh 'mvn install'

        }}

stage('MVN TEST JUnit/Mockito') {
            steps {
                sh 'mvn test'
            }
        }
      stage('MVN SONARQUBE') {
                            steps{

                                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
                            }
                        }
                stage('Nexus') {
                            steps {
                                sh 'mvn deploy -DskipTests'
                            }
                        }
                         stage('Build Image DockerHub') {
                            steps {
                                 sh 'docker build --no-cache -t raniatouihri/supplierdevops:1.0.0 .'                            }
                        }

                stage('Push to DockerHub') {
                    steps {
                        //Connexion à Docker Hub
                           sh 'docker login -u raniatouihri -p rania98206330'

                        //   Pousse de l'image vers Docker Hub
                               sh 'docker push raniatouihri/supplierdevops:1.0.0'

                  }
                 }

                stage('Docker Compose') {
                            steps {
                                sh 'docker compose up -d'
                            }
                        }
                   stage('Docker start Grafana ') {
                                             steps {
                                                 sh 'docker start grafana'
                                             }
                                         }
                                             stage('Docker start Prometheus ') {
                                                                                      steps {
                                                                                          sh 'docker start prometheus'
                                                                                      }
                                                                                  }

    }
}