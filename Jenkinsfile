pipeline {
agent any
environment {
DEPLOY_DIR = '/var/www/html/event-registration'
}stages {
stage('Checkout') {
steps {
echo 'Fetching code from GitHub...'
checkout scm
}
}
stage('Build') {
steps {
echo 'Building the Event Registration Form...'
sh 'ls -l'
}
}
stage('Test') {
steps {
echo 'Running basic tests...'
sh 'test -f index.html && test -f style.css && test -f script.js'
sh 'grep -q "<form" index.html && echo "Form tag present"'
sh 'grep -q "addEventListener" script.js && echo "Validation
script present"'
}
}
stage('Deploy') {
steps {
echo 'Deploying to web server...'
sh 'mkdir -p $DEPLOY_DIR'
sh 'cp index.html style.css script.js $DEPLOY_DIR/'
echo 'Deployed at http://localhost/event-registration/'
}
}
}
post {
success { echo 'Pipeline completed successfully!' }
failure { echo 'Pipeline failed. Check the logs.' }
}
}
