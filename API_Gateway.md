*************  API Gateway **************

For a sr. DevOps engineer, the most important API Gateway topics are:

API Gateway + Lambda integration
API Gateway + EKS/ECS via VPC Link
Authentication (JWT, Cognito, Lambda Authorizers)
Throttling and rate limiting
CloudWatch troubleshooting
Private APIs
Infrastructure as Code (Terraform/CloudFormation)
High-availability and secure API architectures
429, 502, and 504 troubleshooting
CI/CD deployment strategies for APIs.

##

# Scenario-Based Questions

**Scenario 1**: Users complain API latency increased from 50ms to 2s. What will you check?

Answer: 
CloudWatch metrics
Lambda duration
Cold starts
Backend DB latency
Network latency
API cache status

**Scenario 2**: API Gateway works in Dev but fails in Prod.

Checks:
Stage variables
IAM permissions
Resource policy
VPC connectivity
Lambda permissions


**Scenario 3**: You need to expose a private EKS service to external clients securely.

Typical answer: Client -> API Gateway -> VPC Link -> NLB -> EKS Service  


**Scenario 4**: How would you protect an API from DDoS attacks?

Answer:
API Gateway throttling
AWS WAF rules
AWS Shield
Rate limiting
Caching

##

AWS API Gateway Interview Questions
Basic Questions
1. What is AWS API Gateway?  
A: A fully managed service that allows you to create, publish, secure, monitor, and manage APIs. It acts as an entry point between clients and backend services such as Lambda, EC2, containers, or HTTP endpoints.

2. What API types does API Gateway support?  
A: HTTP APIs, REST APIs, WebSocket APIs.

Follow-up: Which one is cheaper?  
A: HTTP APIs are generally lower cost and lower latency than REST APIs.  

3. Difference between HTTP API and REST API?  
Feature	    HTTP API	    REST API
Cost	      Lower	        Higher
Latency	    Lower	        Higher
Features	  Basic	        Advanced
API Keys	  Limited	      Full support
Request Validation:	Limited	  Full support
Usage Plans	  No	        Yes


5. What backends can API Gateway integrate with?
AWS Lambda
HTTP endpoints
Application Load Balancers
EC2 applications
Containers running on Amazon ECS or Amazon EKS
Other AWS services
Architecture Questions


7. Explain the request flow.
Client --> API Gateway --> Lambda / ECS / EKS / EC2 --> Database


9. Why use API Gateway instead of exposing an ALB directly?

Advantages:
Authentication
Authorization
Rate limiting
Request validation
API versioning
Usage plans
Monitoring
API keys

7. How does API Gateway work with Lambda?

Flow:

Request
  |
API Gateway
  |
Lambda Function
  |
Response
  |
Client

API Gateway converts HTTP requests into Lambda events.

Security Questions
8. How can you secure an API Gateway?

Methods:

IAM Authentication
JWT Authentication
Lambda Authorizer
Cognito
API Keys
WAF
Resource Policies
9. What is a Lambda Authorizer?

A Lambda function that validates:

JWT tokens
OAuth tokens
Custom authentication logic

before allowing access.

10. Difference between Authentication and Authorization?

Authentication:
"Who are you?"

Authorization:
"What are you allowed to do?"

11. How do API Keys work?
Identify consumers
Track usage
Apply throttling

Important:
API Keys are not security controls by themselves.

Networking Questions
12. Can API Gateway access private resources?

Yes.

Options:

VPC Link
Private API
Private ALB
13. What is VPC Link?

Secure connection between API Gateway and resources inside a VPC.

Example:

API Gateway --> VPC Link --> Internal NLB --> Private ECS Service  

14. What is a Private API?

API accessible only from within a VPC using a VPC endpoint.

Not accessible from the internet.

15. Difference between Edge-Optimized and Regional API?

Edge Optimized

Uses CloudFront
Better for global users

Regional

Stays within region
Better when users are local
Performance Questions
16. What is API throttling?

Limits request rates to protect backend services.

Example:

1000 requests/sec
2000 burst
17. Difference between Rate Limit and Burst Limit?

Rate:
Sustained requests per second.

Burst:
Temporary spikes allowed above the rate.

18. How does caching work?

API Gateway can cache responses.

Benefits:

Lower latency
Reduced backend load
Reduced Lambda invocations
Monitoring & Troubleshooting
19. How do you monitor API Gateway?

Using:

Amazon CloudWatch metrics
Access logs
Execution logs
X-Ray tracing

Metrics:

Count
Latency
4XX errors
5XX errors
20. API returns 502 Bad Gateway. What would you check?

Common causes:

Lambda timeout
Invalid Lambda response format
Backend unavailable
Permission issues
Mapping template issues
21. API suddenly shows 429 errors. Why?

429 = Too Many Requests.

Possible reasons:

Throttling limit reached
Usage plan exceeded
Backend overloaded
22. Difference between 4XX and 5XX?

4XX:
Client-side errors.

Examples:

400
401
403
404

5XX:
Server-side errors.

Examples:

500
502
503
DevOps / CI-CD Questions
23. How would you deploy API Gateway using Infrastructure as Code?

Tools:

AWS CloudFormation
AWS SAM
Terraform
24. How do you version APIs?

Examples:

/api/v1/users
/api/v2/users

or

Stages:

dev
test
prod
25. How do you implement Blue-Green deployment?

Example:

v1 Lambda
v2 Lambda

API Gateway
    |
 Route traffic

Switch traffic gradually or instantly.
