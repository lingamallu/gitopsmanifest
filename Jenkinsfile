node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'githubsatya', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email s.lingamallu.gupta@accenture.com"
                        sh "git config user.name satya"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+lsgupta/test.*+lsgupta/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        //sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/GitOpskubernetesmanifestRakhi.git HEAD:main"
                        sh "minikube kubectl -- apply -f deployment.yaml"
      }
    }
  }
}
}
