#!groovy

node {

    try {
        stage 'Checkout'
            checkout scm

            sh 'git log HEAD^..HEAD --pretty="%h %an - %s" > GIT_CHANGES'
            def lastChanges = readFile('GIT_CHANGES')
        stage 'Test'
            sh 'virtualenv env -p python2.7'
            sh '. env/bin/activate'
            sh 'env/bin/pip install -r OnTheCloud/requirements.txt'
            sh 'python OnTheCloud/manage.py migrate'
            sh 'python OnTheCloud/manage.py createsuperuser'
            sh 'python OnTheCloud/manage.py collectstatic -y'
            sh 'python OnTheCloud/manage.py runserver'


        stage 'Deploy'
            
    }

    catch (err) {
        
        throw err
    }

}
