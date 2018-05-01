# OnTheCloud
Cloud Storage web app

To run locally, do the following:

1. Clone this 'https://github.com/cmpe172-sp18/OnTheCloud'
2. Open terminal and go to '~/OnTheCloud/' directory
3. Type pip install -r requirements.txt on terminal
4. Type "python manage.py migrate" and press enter
5. Type "python manage.py createsuperuser" and press enter
6. Type "python manage.py collectstatic" and press enter
7. Type "python manage.py runserver" and press enter
8. Go to a web browser and navigate to 'localhost:8000'

To run using Jenkins:

1.Create jenkins pipeline.
2.Connect pipeline to github repository
3.Change build configuration to "by jenkinsfile" and directory to correct file location
4.Go to a web browser and navigate to 'localhost:8000'

You should now have a working jenkins build server that automatically builds upon commit and stops any previous build in the process. This allows for automated continuos deployment of you web app with out the need to manual rebooting.
