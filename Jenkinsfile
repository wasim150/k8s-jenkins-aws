node {

    stage("Git Clone"){

        git credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/wasim150/k8s-jenkins-aws.git'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }
   
       
    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t jhooq-docker-demo .'
        sh 'docker image list'
        sh 'docker tag jhooq-docker-demo 007786/jhooq-docker-demo:${BUILD_NUMBER}   
    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u wasim150 -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  wasim150/jhooq-docker-demo:${BUILD_NUMBER}'
    }

    publishers {
       mailer ('nadeembhandale@gmail.com',true,true)

}
       
   
       }
