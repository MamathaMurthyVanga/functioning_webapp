Problem Set I - Regex

Write a regex to extract all the numbers with orange color background from the below text in italics (Output should be a list).


{"orders":[{"id":1},{"id":2},{"id":3},{"id":4},{"id":5},{"id":6},{"id":7},{"id":8},{"id":9},{"id":10},{"id":11},{"id":648},{"id":649},{"id":650},{"id":651},{"id":652},{"id":653}],"errors":[{"code":3,"message":"[PHP Warning #2] count(): Parameter must be an array or an object that implements Countable (153)"}]}


# to complete the problem 1 i have used python

import re

text = '''{"orders":[{"id":1},{"id":2},{"id":3},{"id":4},{"id":5},{"id":6},{"id":7},{"id":8},{"id":9},
{"id":10},{"id":648},{"id":649},{"id":650},{"id":651},{"id":652},{"id":653}], "errors":[{"code":3,
"message":"[PHP Warning #2] count(): Parameter must be an array or an object that implements Countable [153]"}]}
'''


matches = re.findall(r'(?<="id":)(\d+)', text)

numbers = list(map(int, matches))
print(numbers)

output = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 648, 649, 650, 651, 652, 653]
# regex(regular expression) is pattern matchinh tool used to search, validate, extract and manipulate data efficiently
# regex is used for 
# data validation, search and validation, web scraping, file manupulation


Problem Set 2 - A functioning web app with API

# functioning_webapp 
created virtual environment using python -m venv env
activate the env from env/scripts/activate
pip install django
create project  using django-admin startproject web_app or python -m django startproject web_app
cd web_app
python manage.py startapp admin(only admin has the access to post the apps)
python manage.py startapp user
include the apps in settings.py(INSTALLED APPS) in project, apps url in project urls
database models are written in models.py for admin and user in their repective apps
logic in the views.py for the purpose of register, login, to add apps for admin
logic in the views.py for the purpose of register, login, profile, points, task, for user
created templates for the purpose of admin, app, home, index, login, points, profile, register and task code it written in each .html file according to requirement
to check the data while developing i used get, delete functiionality for that purpose i used serializers from rest framework (pip install djangorestframework) included it INSTALLED APPS in settings.py

freezed the requirements.txt(pip freeze > requirements.txt)


Problem Set 3
Please answer the below questions:

A. Write and share a small note about your choice of system to schedule periodic tasks (such as downloading a list of ISINs every 24 hours). Why did you choose it? Is it reliable enough; Or will it scale? If not, what are the problems with it? And, what else would you recommend to fix this problem at scale in production?

ANSWER
Choice of System for Scheduling Periodic Tasks
System Chosen: Celery with a Message Broker (e.g., RabbitMQ/Redis) and a Scheduler like Celery Beat
Why Did I Choose It?
1.Ease of Use: Celery is a proper task queue system for python, making it straightforward to schedule and excute periodic tasks.
2.Flexibility: with celery beat, you can schedule tasks dynamically without restarting the service and use Cron-like scheduling.
3.Reliabilty:Celery ensures task execution with retries in case of failure, using message brokers like redis or RabbitMQ  to queue the tasks.
4.Scalability: Celery supports distributed task execution, making it suitable for systems with growing workloads.

Is It Reliable Enough?
Yes, it is reliable for small to medium-scale systems due to its mature ecosystem, active community, and robust error handling. However, its reliability depends on:

The configuration of the message broker (e.g., Redis/RabbitMQ).
The system's ability to handle message persistence and retries during downtime.

Will It Scale?
Celery scales well for moderate workloads by adding workers and supporting distributed task execution. However, at large scales, it may face bottlenecks in message broker capacity, task coordination, and monitoring, making it less ideal for high-throughput systems.

Problems with Celery at Scale
Celery may face bottlenecks in message brokers (Redis/RabbitMQ), limited monitoring (e.g., Flower), increased task latency for high-throughput systems, and challenges in recovering from broker or worker failures.    

Recommendations for Scaling in Production
Airflow: For complex workflows with dependencies.
Kubernetes CronJobs: For simple, periodic tasks that need scalability.
Kafka: For large-scale, event-driven systems.
Monitoring & Optimization: Track performance and fine-tune task settings for efficiency.