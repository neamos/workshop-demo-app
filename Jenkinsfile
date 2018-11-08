pipeline {
  agent any
  stages {
    stage('test') {
      steps {
        sh '''# Create python virtual Environment
pip3 install virtualenv --user
python3 -m venv repo

. repo/bin/activate

# Install python requirements
pip install -r requirements.txt '''
      }
    }
    stage('error') {
      steps {
        sh '''# Activate python virtual environment
. repo/bin/activate
#Run pytest and export coverage report
pytest --cov-report xml --cov-report term --cov ./lib/'''
      }
    }
    stage('provision') {
      steps {
        sh '''cd deployment
sh provision.sh'''
      }
    }
  }
}