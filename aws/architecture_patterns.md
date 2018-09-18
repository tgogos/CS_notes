
# Public Service, Public Network

![](public-subnet-public-lb.png)

A public facing service is one of the most common architecture patterns for deploying containers on AWS. It is well suited for:

-   A static HTML website, perhaps hosted by NGINX or Apache
-   A dynamically generated web app, perhaps served by a Node.js process
-   An API service intended for the public to access
-   A public facing endpoint designed to receive push notifications, perhaps from Amazon SNS (Simple Notification Service)
-   An edge service which needs to make outbound connections to other services on the internet

Everything is deployed in an Amazon Virtual Private Cloud (VPC) which has a subnet exposed to the internet. An internet gateway is attached to allow resources launched in the VPC to accept connections from the internet, and initiate connections to the internet. Inside the VPC each resource has its own public IP address. A few resources are included:

-   A public facing load balancer which accepts inbound connections on specific ports
-   One or more EC2 instances hosting the application container, configured to accept inbound connections from the load balancer on specific ports (optionally from any source).





# Public Service, Private Network

![](private-subnet-public-lb.png)



# Private Service, Private Network

![](private-subnet-private-lb.png)



# Private Service, Service Discovery

![](private-subnet-private-service-discovery.png)
