# Steps to complete Lab6-Microservices

To run the services as indicated in the Wiki, we first must launch the registration services:

```bash
./gradlew :registration:bootRun
```

Then, the remaining services can be launched:

```bash
./gradlew :accounts:bootRun

./gradlew :web:bootRun
```

The services' logs can be seen in the following screencaptures:

* Accounts ->

![accounts-logs](screenshots/accounts-logs.png)

* Web ->

![web-logs](screenshots/web-logs.png)

We can check they are up and registered in the Eureka dashboard:

![eureka-initial](screenshots/eureka-initial.png)

With these steps we have succesfully launched the microservices demo.

Next, we'll initiate and register another accounts service, this time under the port number 4444.
To achieve that, we must modify the application.yml file for the accounts service, indicating the new port, and then launch another terminal with the same command as before:

![accounts-4444-logs](screenshots/accounts-4444-logs.png)

Once we have the two accounts services and the web service up, we can kill the accounts service running in port 2222 to check if the service running in the port 4444 takes its place.
To achieve this, we close the terminal on which the service was running, and then try to access `localhost:2222`, to which we get an error.

After accessing the web service, we can see the accounts service is still working via the one on the port 4444:

![accounts-up-1](screenshots/accounts-up-1.png) ![accounts-up-2](screenshots/accounts-up-2.png)

This is achieved thanks to Eureka, the registration service. When it detects that the accounts service first instantiation has failed, it automatically switches the accounts service that the web service is using, making it available through the one that is up and running.
