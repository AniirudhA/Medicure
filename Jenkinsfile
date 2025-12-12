pipeline 
{
   agent any
   
   stages 
  {
    stage('Git checkout') 
    {
      steps  
        {
          echo 'This for only clonning the git repository'
          git 'https://github.com/AniirudhA/Medicure-Project.git'
        }
    }
    stage('Maven Package') 
    {
      steps 
        {
          echo 'This for Packaging the application'
          sh 'mvn package'
        }
    }
    stage('Generating Docker Image') 
    {
      steps 
        {
          echo 'This is to build Docker Image'
          sh 'docker build -t aniirudh/medicure .'
        }
      }
      stage('Logging to DOCKER HUB') 
    {
      steps 
        {
          echo 'This is to push Docker Image'
          withCredentials([usernamePassword(credentialsId: 'dockerhub-cre', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
          sh "echo $PASS | docker login -u $USER --password-stdin"
          sh 'docker push aniirudh/medicure'  
          }
        }
	}
  }
}