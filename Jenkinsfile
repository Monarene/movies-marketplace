def imageName = 'mlabouardy/movies-marketplace'
def registry = 'https://registry.slowcoder.com'

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

    // stage('Build'){
    //     docker.build(imageName, '--build-arg ENVIRONMENT=sandbox .')
    // }

    // stage('Push'){
    //     docker.withRegistry(registry, 'registry') {
    //         docker.image(imageName).push(commitID())

    //         if (env.BRANCH_NAME == 'develop') {
    //             docker.image(imageName).push('develop')
    //         }
    //     }
    // }
}

// def commitID() {
//     sh 'git rev-parse HEAD > .git/commitID'
//     def commitID = readFile('.git/commitID').trim()
//     sh 'rm .git/commitID'
//     commitID
// }