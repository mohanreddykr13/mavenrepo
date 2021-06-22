pipeline{
agent {label 'jkslavemachine1'}
triggers { pollSCM('* * * * *') }
stages{

stage('scm'){
steps{checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'cd28416a-10eb-4dfc-a220-3e49a2e528df', url: 'https://github.com/Devopssampleproject/mavenrepo.git']]])
} // steps close
}  //stage1 close

stage('build'){
steps{
    sh 'mvn package'
}    
}

stage('sonar'){
steps{withSonarQubeEnv('sonarqube') {
     sh 'mvn sonar:sonar'
}
}   //steps close
}   //stage2 close

stage('nexus'){
steps{
    sh 'mvn deploy'
}    
}

stage('deploy'){
steps{
    sh 'scp /root/workspace/jobmaven/target/studentapp-2.1.1-FEAT01-SNAPSHOT.war 172.31.4.37:/var/lib/tomcat/webapps'
}    
}

}   //stages close
}   //pipeline close
