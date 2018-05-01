#!groovy
def abortPreviousRunningBuilds() {
            def hi = Hudson.instance
            def pname = env.JOB_NAME.split('/')[0]

            hi.getItem(pname).getItem(env.JOB_BASE_NAME).getBuilds().each{ build ->
            def exec = build.getExecutor()

            if (build.number != currentBuild.number && exec != null) {
            exec.interrupt(
            Result.ABORTED,
            new CauseOfInterruption.UserInterruption(
            "Aborted by #${currentBuild.number}"
            )
            )
            println("Aborted previous running build #${build.number}")
            } else {
            println("Build is not running or is current build, not aborting - #${build.number}")
            }
        }
       }
node {

    try {
        stage 'Checkout'
            checkout scm

            sh 'git log HEAD^..HEAD --pretty="%h %an - %s" > GIT_CHANGES'
            def lastChanges = readFile('GIT_CHANGES')
        stage 'Build'
            sh 'virtualenv env -p python2.7'
            sh '. env/bin/activate'
            sh 'env/bin/pip install -r OnTheCloud/requirements.txt'
            sh 'python OnTheCloud/manage.py migrate'
            sh 'python OnTheCloud/manage.py createsuperuser'
            sh 'python OnTheCloud/manage.py collectstatic --noinput'
        
        stage 'Deploying'
            abortPreviousRunningBuilds()
            sh 'BUILD_ID=dontKillMe nohup python OnTheCloud/manage.py runserver'
            
    }
    catch (err) {
        
        throw err
    }

}
