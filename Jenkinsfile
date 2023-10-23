node ('ubuntu-appserver-cweb') 
{
  def app
  stage ('Cloning Git') 
  {
    /* make sure the repository is cloned to workspace */
    checkout scm
  }
    stage ('Build-and-Tag')
  {
    /* this builds the actual image;
    * this is synonymous to docker build on the command line */
      app = docker.build("murnink/real-estateweb")
  }

  stage('Post-to-dockerhub') 
  {
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') 
    {
      app.push("latest")
    }
  }

  stage('Pull-image-server') 
  {
    sh "docker-compose down"
    sh "docker-compose up -d"
  }
}
