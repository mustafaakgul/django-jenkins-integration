## This is demonstration how to set up a CI/CD pipeline for a simple Python application using Jenkins and Docker and Django

### How to Run
#### First, we need to set up somethings in local
* Clone this repository
* python -m venv venv
* source venv/bin/activate
* pip install -r requirements.txt
* python manage.py makemigrations
* python manage.py migrate
* python manage.py createsuperuser
* python manage.py runserver

#### Second, we need to set up Jenkins and Docker on AWS EC2 instance
* Create an EC2 Ubuntu instance on AWS and install Jenkins on it
* Connect to this machine via SSH
* Update linux packages with `sudo apt-get update`
* Install python3 and pip3 with `sudo apt-get install python3-pip`
* Install docker with `sudo apt-get install docker.io`
* Install Java with `sudo apt install openjdk-17-jdk`
* Install Jenkins with
  * curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \  
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
  * echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  * sudo apt-get update
  * sudo apt-get install jenkins
* Let's start Jenkins and check status with
  * sudo systemctl start jenkins
  * sudo systemctl status jenkins
* Open Jenkins on your browser with `http://<your-public-ip>:8080`
* Get the initial admin password with `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
* Install suggested plugins
* Create first admin user

#### Third, we need to set up Jenkins pipeline
* Let's set up an agent
  * Go to Dashboard > Nodes > New Node
  * Enter a name for your agent
* Let's create a job
* In configuration page
  * Fill the GitHub repository URL
  * Select Git under Source Code Management
  * Fill the secret key of your GitHub repository that is generated bu webhooks in Github
  * Let's configure build triggers by choosing Branches to build
* Configuring Docker on Jenkins
  * In Build Steps, Enter the commands to build and run
  * sudo docker build . -t <your-repository-name> // This command will build the image
  * sudo docker run -d -p 8005:8005 <your-repository-name> // This command will run the image
* And click the Build Now button to run the job