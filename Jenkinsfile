pipeline {
    environment {
        registry = 'ducluanxutrieu/petclinic-spinnaker-jenkins'
        registryCredential = 'dockerHubCredentials'
        dockerImage = ''
    }
    agent any
    triggers {
        pollSCM '* * * * *'
    }

    tools {
        maven 'M3'
    }
    stages {
        // stage('Build Application') {
        //     steps {
        //         echo '=== Building Petclinic Application ==='
        //         sh 'mvn -B -DskipTests clean package'
        //     }
        // }
        // stage('Test Application') {
        //     steps {
        //         echo '=== Testing Petclinic Application ==='
        //         sh 'mvn test'
        //     }
        // //       post {
        // //        always {
        // //        junit 'target/surefire-reports/*.xml'
        // //    }
        // //           }
        // }
        // stage('Build Docker Image') {
        //     steps {
        //         echo '=== Building Petclinic Docker Image ==='
        //         script {
        //             dockerImage = docker.build registry + ":$BUILD_NUMBER"
        //         }
        //     }
        // }
        // env.BUILD_NUMBER
        stage('Push Docker Image') {
            //        when {
            //            branch 'master'
            //            }
            steps {
                echo '=== Pushing Petclinic Docker Image ==='
                script {
                    // docker.withRegistry('', registryCredential ) {
                    //     dockerImage.push()
                    // }
                    docker.withRegistry("https://966163032495.dkr.ecr.ap-southeast-1.amazonaws.com/spinnaker", "ecr:ap-southeast-1:aws_credential") {
                        docker.image("ducluanxutrieu/petclinic-spinnaker-jenkins").push()
                    }
                }
            }
        }
        stage('Remove local images') {
            steps {
                echo '=== Delete the local docker images ==='
                sh("docker rmi -f $registry:$BUILD_NUMBER || :")
            }
        }
    }
}
