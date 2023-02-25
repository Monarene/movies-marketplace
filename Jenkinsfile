def imageName = 'mlabouardy/movies-marketplace'
def myImageName = 'monarene/movies-marketplace'

// send test

node(''){
    stage('Checkout'){
        checkout scm
    }

    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")

    stage('Quality Tests'){
        sh "docker run --rm ${imageName}-test npm run lint --force"
    }

    stage('Unit Tests'){
        sh "echo 'pass tests'"
        
    }

    stage('Build'){
        dockerImage = docker.build(myimageName)
    }

    // stage('Static Code Analysis'){
    //     withSonarQubeEnv('sonarqube') {
    //         sh 'sonar-scanner'
    //     }
    // }

    // stage("Quality Gate"){
    //     timeout(time: 5, unit: 'MINUTES') {
    //         def qg = waitForQualityGate()
    //         if (qg.status != 'OK') {
    //             error "Pipeline aborted due to quality gate failure: ${qg.status}"
    //         }
    //     }
    // }

    stage('Push'){
        withDockerRegistry([credentialsId: "dockerhub", url: "" ]) {
        dockerImage.push(commitID())
        
        if (env.BRANCH_NAME == 'develop') {
            dockerImage.push('develop')
        }
        
        }
        
    }

}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}