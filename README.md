# How to setup rest-apis-queue-email

# setup web services

1. Upload project in Github
2. Open render https://dashboard.render.com/#
3. Signup using Github
4. Click new > web service > Connect a repository > choose rest-apis-queue-email from Github > connect
5. Name: (put any name) > environment : Docker > Branch: main > Region: (Choose nearest region) > Instance Type: (free plan) > create web services
6. waiting until it live
7. Done

# create .env files for own password
1. create .env file at main files
2. paste link of api based on DATABASE_URL, MAILGUN_API_KEY, MAILGUN_DOMAIN, REDIS_URL


# setup databse
1. open elephant.sql ----> https://customer.elephantsql.com/
2. signup with github
3. click button ---> + Create New Instance (create 2db or instances, 1. for local 2. for production)
4. fill Name: > Plan (Tiny Turtle Free) > Tags:
5. select region > review > create instance > Done
6. click instance name that you provide > copy URL 
7. open render.com > click rest-apis-queue-email > click Environment > Add Environment Variable > Key : type DATABASE_URL > Value : paste API that you copy earlier (point 6) > make sure change postgres to postgresql from api > save changes
8. Open file .env from folder rest-apis-queue-email > replace your link from Database : DATABASE_URL=""


# setup email
1. Open mailgun --> https://login.mailgun.com/login/ > signup
2. Dashboard >  click link from Sending Domain > select API > copy API Key & API base URL
3. Open file .env from folder rest-apis-queue-email > replace your link from API Key : MAILGUN_API_KEY=""
4. Open file .env from folder rest-apis-queue-email > replace your link from API base URL : MAILGUN_DOMAIN=""


# setup rest-apis-task-queue
1. Open render https://dashboard.render.com/#
2. Click new > Redis
4. Name (put any name) > Region (choose nearest region) > Maxmemory Policy: choose noeviction (recommended for queues/persistance) > Instance type : choose free plan > Create Redis
5. Go to dashboard > click Name that you given earlier > Access Control > source put : 0.0.0.0/0 > Save > copy Redis URL
6 Open file .env from folder rest-apis-queue-email > replace your link from Redis : REDIS_URL=""


# setting Insomnia
1. install insomnia ----> https://insomnia.rest/
2. see how to setup at folder images
3. open environment and paste ----> {"url": "https://rest-apis-flask-email.onrender.com"} > close
4. you can test in insomnia


# setting environment
1. refer to setting_environment.jpg in folder images>user
2. access_token > click ctrl+space > type: Response- Body Attribute
3. click response body > Request: choose (login-authenticate user)
4. click response body > filter (Jsonpath or Xpath) : type $.access_token
5. click response body > trigger behaviour : choose (when expired - resend when existing response has expired)
6. click response body > max age : 300
7. Done > Close
8. In every endpoint of insomnia for Users, tags, stores, items > click Headers: type Authorization and {{access_token}}
9. except for user > get non fresh token > click Header > type Authorization  and Bearer [paste refresh token from authenticate user]