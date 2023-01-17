## AWS DYNAMODB 
1. What is the difference between Query and Scan operations in DynamoDB?

A Dynamodb query operation is used to retrieve one or more items from a table or a secondary index in the table. It allows for filtering the results based on the primary key or a secondary index key. It also allows for sorting the results in ascending or descending order WHILE

A Scan operation, on the other hand, scans the entire table or a secondary index and returns all items that match the specified filter. It is slower and not cost effective likeq uery operation because it looks at all items in the table or index, rather than just the items that match the key. However, it is useful when you don't know the exact primary key value of the item you are looking for, or when you want to retrieve all items that match a certain condition.

2.What are projection expressions in DynamoDB?
Projection expressions in DynamoDB are used to specify the attributes that should be returned in the query results. They can be used to return only a subset of the attributes, rather than returning all attributes for each item in the query results

3.How would you make items in a DynamoDB table expire after a period of time?
This can be achieved by setting future timestamp attributes, called Time to Live TTL for each item on the table. Dynamodb then automatically deletes items from table when their TTL values is less than the current time

## DOCKER
4. How would we map ports in docker using cli command?
One can map their local machine port to docker port using the syntax: docker run -p host_port:container_port e.g
docker run -p 80:8080 my_image

5. What is the difference between docker stop and docker kill commands?
The 'docker stop' command stop a running container and also performs cleanup actions before shutting down WHILE the 'docker kill' command abtruptly stops a running container and does not perform any cleanup actions

## AWS BATCH
6.What are the states a job can have when submitted to an AWS Batch job queue?
SUBMITTED: The job has been received by the queue and is waiting to be picked up by a compute environment.
PENDING: The job has been picked up by a compute environment and is waiting for resources to become available.
RUNNABLE: Resources have become available for the job and it is now waiting to be scheduled by the compute environment.
STARTING: The job is being initialized and started by the compute environment.
RUNNING: The job is running on a compute resource.
SUCCEEDED: The job completed successfully.
FAILED: The job failed to complete successfully.

7. What are the main AWS Batch resource types used in a CloudFormation template?
AWS::Batch::JobDefinition
AWS::Batch::JobQueue
AWS::Batch::ComputeEnvironment

8.How would you pass named arguments with parameterized values in a Batch job
definition?
To pass named arguments with parameterized values, you can use the command property of the containerProperties property and include the named arguments and their values in the command string

## AWS LAMBDA
9.How can we tell at runtime whether or not a Batch job failed and has been
attempted again?

We have different ways to tell if a Batch job fails or not and had been attempted again at the runtime. One of them is to check the status by using the commendline. Another way is to implement a logics that send notification or alert when a job fails.

10..How can we schedule execution of a Lambda function in regular time intervals?
This can be achieved by using Amazon CloudWatch Events to schedule regular excution of lambda at some regular interval.

11.How can we execute a Lambda function using Python and, once we do, do we
have to wait for its results?

One can excute a lambda function using the AWS SDK for python (Boto3). Below is syntax of how to invoke a lambda function using boto3
```
import boto3
<!-- Create a client for the Lambda service -->
client = boto3.client('lambda')

<!-- Invoke the Lambda function -->

response = client.invoke(
    FunctionName='my_function',
    InvocationType='Event',
    Payload=b'{ "key1": "value1", "key2": "value2" }'
)
# Print the response
print(response)
```
One can decide to wait for the result or not depending on the InvocationType value. When InvocationType is set to 'Event', the function will excute asynchronously WHILE if it is set 'RequestResponse' the action will be performed synchronously and wait for response before it returns.

## PYTHON
12. Given the following list, how would you produce a list with duplicate entries removed?
`list(set(['a','b','c','d','d','d','e','a','b','f','g','g','h']))`

13. Given the numbers in the following tuple sequence, how would we obtain a list of
their squares?
numbers = (1, 2, 3, 4, 5)
<!-- set into a list -->
```
def convert(set_args):
  num = list(set_args)
  f = lambda x: x*x
  return [f(x) for x in num]

set_args = (1, 2, 3, 4, 5)
print(convert(set_args))
```
14. Define a function is_palindrome that would return True if the input string is
palindrome False

```
def is_palindrome(input_string):  
  new_string = ""
  reverse_string = ""
  <!-- Traverse through each letter of the input string -->
  for string in input_string.lower():
   
    if string.replace(" ",""):
      new_string = string + new_string
      reverse_string = string + reverse_string
  <!-- Compare the strings -->
  if new_string[::-1]==reverse_string:
    return True
  else:
    return False
```

15. Given the following data structure, print a list of pages that have GET as their type
and 403 as their status
```
requestList = [
{
"type": "GET",
"status": 200,
"page": "example.com/one"
},
{
"type": "POST",
"status": 200,
"page": "example.com/two"
},
{
"type": "GET",
"status": 404,
"page": "example.com/three"
},
{
"type": "POST",
"status": 403,
"page": "example.com/four"
},
{
"type": "GET",
"status": 500,
"page": "example.com/five"
},
{
"type": "GET",
"status": 403,
"page": "example.com/six"
},
{
"type": "POST",
"status": 403,
"page": "example.com/seven"
},
{
"type": "GET",
"status": 403,
"page": "example.com/eight"
}
]
newList = []
for request in requestList:
  if request["type"] == "GET" and request["status"] == 403:
    newList.append(request)
print(newList)

```