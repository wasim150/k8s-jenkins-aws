node {

    stage("Git Clone"){

        git credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/Nadeem-13/k8s-jenkins-aws.git'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }
   
       
    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t jhooq-docker-demo .'
        sh 'docker image list'
        sh 'docker tag jhooq-docker-demo 007786/jhooq-docker-demo:jhooq-docker-demo'
    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u 007786 -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  007786/jhooq-docker-demo:jhooq-docker-demo'
    }

    publishers {
       mailer ('nadeembhandale@gmail.com',true,true)

}
       
   
       }
