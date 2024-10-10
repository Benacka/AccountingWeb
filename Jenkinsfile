node('ubuntu-Appserver-2')
{

def app
stage('Cloning Git')
{
    checkout scm
}

stage('Build-and-Tag')
{
    /* This builds the actual image;
        *synonymous to docker build on the command line*/
    app = docker.build('Benacka/AccountingWeb')
}

stage('Post-to-dockerhub')
{
    /* Pushes to Docker Hub*/
    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
    {
        app.push('latest')
    }
}

stage('Deploy')
{
    sh "docker-compose down"
    sh "docker-compose up -d"
}

}