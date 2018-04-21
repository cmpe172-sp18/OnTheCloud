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
            

        stage 'Deploy'
            python OnTheCloud/manage.py migrate
            python OnTheCloud/manage.py createsuperuser
            python OnTheCloud/manage.py collectstatic
            python OnTheCloud/manage.py runserver

    }

    catch (err) {
        
        throw err
    }

}
