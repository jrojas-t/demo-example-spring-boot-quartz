# Spring Boot Quartz Scheduler : Building an Email Scheduling

## Requirements

1. Java - 8
2. Maven - 3.x.x > 
3. MySQL - 5.x.x >

## Steps to Setup

**1. Clone the application**

```bash
git clone https://github.com/jrojas-t/demo-example-spring-boot-quartz.git
```

**2. Create MySQL database**

```bash
create database quartz_demo
```

**3. Change MySQL username and password as per your MySQL installation**

open `src/main/resources/application.properties`, and change `spring.datasource.username` and `spring.datasource.password` properties as per your mysql installation


**4. Setup Spring Mail**

The project is using Gmail's SMTP server for sending emails. Whether you use Gmail or any other SMTP server, you'll need to configure the following mail properties accordingly -

```properties
spring.mail.host = smtp.gmail.com
spring.mail.port = 587
spring.mail.username = YOUR_EMAIL@gmail.com
spring.mail.password = YOUR_PASSWORD
```

If you're using Gmail, you need to allow the third party apps to send emails by following the instructions below -

+ Go to https://myaccount.google.com/security?pli=1#connectedapps
+ Set ‘Allow less secure apps’ to YES

**5. Create Quartz Tables**

The project stores all the scheduled Jobs in MySQL database. You'll need to create the tables that Quartz uses to store Jobs and other job-related data. Please create Quartz specific tables by executing the `quartz_tables.sql` script located inside `src/main/resources` directory.

```bash
mysql> source <PATH_TO_QUARTZ_TABLES.sql>
```

**6. Build and run the app using maven**

Finally, You can run the app by typing the following command from the root directory of the project -

```bash
mvn spring-boot:run
```

## Scheduling an Email using the /scheduleEmail API

```bash
curl --location --request POST 'http://localhost:8080/scheduleEmail' \
--header 'Content-Type: application/json' \
--data-raw '{
 "email":"jkrojas@atsistemas.com",
 "subject":"Demo Example",
 "body":"<b> Hello Quartz!!! </b>",
 "dateTime":"2022-01-25T17:59:00",
 "timeZone":"Europe/Madrid"
}'

# Output
{"success":true,"jobId":"0741eafc-0627-446f-9eaf-26f5d6b29ec2","jobGroup":"email-jobs","message":"Email Scheduled Successfully!"}
```
