
# Public Service, Public Network

A public facing service is one of the most common architecture patterns for deploying containers on AWS. It is well suited for:

-   A static HTML website, perhaps hosted by NGINX or Apache
-   A dynamically generated web app, perhaps served by a Node.js process
-   An API service intended for the public to access
-   A public facing endpoint designed to receive push notifications, perhaps from Amazon SNS (Simple Notification Service)
-   An edge service which needs to make outbound connections to other services on the internet

![](public-subnet-public-lb.png)



# Public Service, Private Network

![](private-subnet-public-lb.png)



# Private Service, Private Network

![](private-subnet-private-lb.png)



# Private Service, Service Discovery

![](private-subnet-private-service-discovery.png)
