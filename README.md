# AWS-Zero-Trust-Architechture
The Phantom Service Perimeter

In this project I implemented Zero Trust on AWS.

Zero Trust integrates network and identity controls by fortifying the network boundary with identity-aware controls while simultaneously minimizing the network perimeter of individual service components.

In a Zero Trust world, network-centric trust models are extended or replaced by other identity-centric techniques to provide equal or better security than we initially had in place. The following steps were followed in my attempt to implement Zero Trust in the architecture attached below.

1. I updated the API Gateway authorization to leverage AWS IAM short lived credentials and the SigV4 authorization protocol. This gave our application the ability to make authorization decisions for each call request in real time.

2. I implemented AWS IAM authorization on the API Gateway. This created a single mechanism for users (like IAM users or Federated Identities) and other services (like Service A on EC2 instances) to access the data through the API.

3. I leveraged scalable endpoints and network encryption over all communications channels. I also enhanced the VPC endpoint security by adding a security group to only allow communication over ports associated with encryption to enhance protection of our API Gateway.

4. I combined network and identity controls into enforcement points at the API Gateway and VPC endpoint, with each being aware of the other in the authorization process. This protects individual services from being negatively impacted should the other have a security event. Thereby eliminating unnecessary pathways between resources.

5. I was able to gain insight into our user behavior with AWS GuardDuty and enforce the right amount of security at the point of user access.

6. Lastly, I leveraged API Gateway and VPC endpoints to place strict, granular controls on all communication. The API Gateway Resource policy now won't allow unauthorized callers from Service A's VPC, instead only allowing calls when it both traverses the right VPC endpoint (network) and contains the right user credentials (identity). Service A also ensures its service can't be used to send data to anywhere other than the authorized API Gateway by authorizing only access to specific roles and to specific external components.
