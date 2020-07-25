
See: https://stackoverflow.com/questions/63083403/how-to-deploy-visual-studio-flask-app-to-elastic-beanstalk/63084914#63084914

This project started with the Visual Studio Template:  **Flask Web Project**

*AWS Toolkit for Visual Studio will not support deployment or environment creation. It only applies to .Net environments.*

 1. Create AWS Elastic Beanstalk Environment. Use the portal or CLI. 
*Environments > Create environment (Web server environment) > Select* 

Settings: 

 - Platform: Python 
 - Platform Branch: Python 3.7 
 - Platform Version: 3.0.3

2. Add **application.py** with content (the port 8080 seems to be a key ingredient):

<br>

    """
    This script runs the FlaskWebProject1 application using a development server.
    """
    
    from os import environ
    from FlaskWebProject1 import app as application
    
    if __name__ == '__main__':
        HOST = environ.get('SERVER_HOST', 'localhost')
        try:
            PORT = int(environ.get('SERVER_PORT', '8000'))
        except ValueError:
            PORT = 8000
        application.run(HOST, PORT)

3. Create a zip with the following root directory. Zip file name does not matter:

<br>

    application.py
    FlaskWebProject1
    requirements.txt

4. Deploy zip using the portal (or cli)
- Elastic Beanstalk > Environments > Flaskwebproject1-env
- click: *Upload and deploy*