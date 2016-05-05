* APP: Create a bean stalk (rails) application and deploy it
* LOAD: Create a load generator bean stalk application: https://github.com/awslabs/eb-locustio-sample
* Create a cloud watch alarm to autoscale if the APP's EnvironmentHealth >= 5 for 5 minutes
* Create also some dashboards

ElastiCache
* Create elasticCache cluster (m3.medium was least available) with 'default' security group
  - Choose REDIS for simplicity with default port
  - Note down the endpoint
* Create a fresh EC2 instance
  - Select default security group and add SSH and TCP (6379) in InBound connections
* SSH to EC2 and try to telnet to redis endpoint from above in 6379 port 

Elastic Load Balancer
* Create a fresh/use an existing EC2
  - Install httpd and start the service
  - Check with WGET if the localhost and Public IP/DNS works
* Create an LB for it
  - From the Ec2's dashboard create an LB
  - Ensure the selected security group has port 80 opened for inbound connections
  - Ensure that "Status" is showing atleast 1 in the loadbalancer's selection in EC2.
    Otherwise, try to tune the Health check based on the need (e.g. change /index.html to /)
  - Check with browser the Public DNS if it works  
* (optional) Try to test this ElasticLB with eb-locustio

Cloud watch metrics
* Create custom metrics
  - Put custom metrics with 'put-metric-data' and 'get-metric-statistics'
  
Elasticache
* Memcached
 - Launch an t2.micro and get memcahced running (`sudo apt-get install mysql-server php5-mysql php5 php5-memcached memcached`)
 - Try to connect with a client (e.g. ruby: https://github.com/petergoldstein/dalli)
* Redis
