node {
    def mvnHome = tool 'M3'

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        bat "${mvnHome}/bin/mvn -B package"
    }
}
