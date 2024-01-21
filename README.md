## This is demonstration how to set up a CI/CD pipeline for a simple Python application using Jenkins and Docker and Django

### How to Run
* Clone this repository
* Install Jenkins
* Install Docker and Docker Compose that is out of the box with Docker Desktop
* python -m venv venv
* source venv/bin/activate
* pip install -r requirements.txt
* python manage.py makemigrations
* python manage.py migrate
* python manage.py createsuperuser
* python manage.py runserver