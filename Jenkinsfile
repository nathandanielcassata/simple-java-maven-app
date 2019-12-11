node {
 
   stage('Preparation') {  
 
      sh 'mvn archetype:generate -B ' +
      '-DarchetypeGroupId=org.apache.maven.archetypes ' +
      '-DarchetypeArtifactId=maven-archetype-quickstart ' +
      '-DgroupId=com.company -DartifactId=myproject'
      
 
   }
   stage('Build') {
        
      dir ('myproject') {
            sh 'mvn clean install test'
      } 
       
   }
   stage('Archive') {
           dir ('myproject/target') {
           archive '*.jar'
      } 
      
   }  
   stage('Test') { 
            steps {
                sh 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        } 
   stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
            }
        }

}
