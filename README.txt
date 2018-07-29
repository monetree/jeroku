
    python 3.5.2
    virualenv -p python3 .
    source bin/activate
    pip install -r requirements-dev.txt


    deployment steps:
      step1:  --install all pip packages --
                dj-database-url==0.5.0
                dj-static==0.0.6
                python-decouple==3.1

      step2: --create a Procfile and add the line below--
                web: gunicorn jiroku.wsgi --log-file -

      step3: create runtime.txt
                mention python version(python-3.5.2)

      step4: pip freeze > requirements-dev.txt

      step5: --create requirements.txt file and add below lines--
              -r requirements-dev.txt
              gunicorn
              psycopg2
      ***warning: these apps are not mandate. requires as per requirements***

      step6: add this in settings.py
              from decouple import config
              SECRET_KEY = config('SECRET_KEY')
              DEBUG = config('DEBUG',default=False, cast=bool)
              ALLOWED_HOSTS = ['*']

    step7: add these in wsgi.py
              import os
              from dj_static import Cling
              from django.core.wsgi import get_wsgi_application
              os.environ.setdefault("DJANGO_SETTINGS_MODULE", "yourprojectname.settings")
              application = Cling(get_wsgi_application())


    steps to deploy on heroku:
      step1: git init
      step2: heroku login
      step3: heroku create appname
      step4: heroku config:set DEBUG:True
      step5: heroku config:set SECRET_KEY='SECRET KEY'
      step6: heroku config
      step7: git add .
      step8: git commit -m "commit message"
      step9: git remote -v
      step10: git push heroku master --force
