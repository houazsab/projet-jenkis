pipeline {
agent any
stages{
stage('parallel') {
    parallel{
    stage('Unit Testing') {
    steps {
    bat './mvnw test'
    junit 'target/surefire-reports/*.xml'
    }
    stage('Code Analysis') {
    steps {
    bat './mvnw javadoc:javadoc'
    publishHTML ([
         allowMissing: false,
         alwaysLinkToLastBuild: true,
         keepAll: true,
         reportDir: 'target/site/apidocs',
         reportFiles: 'index.html',
         reportName: 'Documentation'
        ])
    }
    }
}
}
/*stage('init'){
steps{
bat './mvnw clean'
}
}
stage('test'){
steps{
bat './mvnw test'
junit 'target/surefire-reports/*.xml'
}
}*/

/*stage('Documentation') {
    steps {
    bat './mvnw javadoc:javadoc'*/
       /* script {
            bat './mvnw javadoc:javadoc'

            bat 'if exist doc rmdir /S /Q doc'
            bat 'mkdir doc'

            bat 'xcopy /E /I /Y target\\site doc'

            bat 'powershell -Command "Compress-Archive -Path doc\\* -DestinationPath doc.zip"'

            archiveArtifacts artifacts: 'doc.zip', fingerprint: true


        }*/
   /* publishHTML ([
     allowMissing: false,
     alwaysLinkToLastBuild: true,
     keepAll: true,
     reportDir: 'target/site/apidocs',
     reportFiles: 'index.html',
     reportName: 'Documentation'
    ])
    }
}*/
stage('build'){
steps{
bat './mvnw package'
archiveArtifacts 'target/*.jar'
/*post {
always{
    emailexct(subject:"build réussi:",
              body:"Le build a réussi.",
              to: "houazenesabrina@gmail.com"
              )
}
}*/
}
/*post {
failure{
    mail(subject:"build échec:",
         body:"Le build a échoué.",
              to: "houazenesabrina@gmail.com"
              )
}
success{
    mail(subject:"build réussi:",
              body:"Le build a réussi.",
              to: "houazenesabrina@gmail.com"
              )
}
}*/
}

stage('deployement'){
steps{
bat ' docker-compose up --build -d'

}
}
}
}