# LOCALSTACK DOCKER SQS AND SNS

## FIRST INSTALL AND CONFIGURE AWS CLI:
```
https://aws.amazon.com/pt/cli/
```

## DOCKER
docker run --rm -it -p 4566:4566 -p 4571:4571 localstack/localstack

## CREATE QUEUE:
```
Request (paste in the terminal)
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name test

Response
{
    "QueueUrl": "http://localhost:4566/queue/test"
}
```

## SEND MESSAGE TO QUEUE:
```
Request (paste in the terminal)
aws --endpoint-url=http://localhost:4566 sqs send-message --queue-url http://localhost:4566/queue/test --message-body "{\"contact\":{\"name\":\"Contato Teste 1\",\"email\":\"contact1@gmail.com\",\"phone\":\"5513999999999\"}}"

Response
{
    "MD5OfMessageBody": "4449beea32141ebd982d823daa49a542", 
    "MD5OfMessageAttributes": "d41d8cd98f00b204e9800998ecf8427e", 
    "MessageId": "e9dcd4ab-871b-4dd4-a7b7-8426a8bfb5e0"
}
```

## READ MESSAGES FROM QUEUE:
```
aws --endpoint-url=http://localhost:4566 sqs receive-message --queue-url http://localhost:4566/queue/test --max-number-of-messages 10
```

## LIST QUEUES
```
aws --endpoint-url=http://localhost:4566 sqs list-queues
```

## CREATE TOPIC:
```
aws --endpoint-url=http://localhost:4566 sns create-topic --name test_topic
```

## SUBSCRIBE TO A TOPIC USING EMAIL
```
aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn arn:aws:sns:us-east-1:000000000000:test_topic --protocol email --notification-endpoint test@email.com
```

## SUBSCRIBE TO A TOPIC USING HTTP
```
aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn arn:aws:sns:us-east-1:000000000000:test_topic --protocol http --notification-endpoint http://localhost:8080/sns-event
```

## SUBSCRIBE TO A TOPIC USING HTTPS
```
aws --endpoint-url=http://localhost:4566 sns subscribe --topic-arn arn:aws:sns:us-east-1:000000000000:test_topic --protocol https --notification-endpoint http://localhost:8080/sns-event
```

## PUBLISH TO A TOPIC
```
aws --endpoint-url=http://localhost:4566 sns publish --topic-arn arn:aws:sns:us-east-1:000000000000:test_topic --message "Hello World!"
```

## UNSUBSCRIBE FROM A TOPIC
```
aws --endpoint-url=http://localhost:4566 sns unsubscribe --subscription-arn *arn:aws:sns:us-east-1:000000000000:test_topic:43aa4105-85ba-4c11-8c7c-e4356e6fb419
*You can take this info using list subscriptions command
```

## LIST SUBSCRIPTIONS
```
aws --endpoint-url=http://localhost:4566 sns list-subscriptions
```

## LIST TOPICS
```
aws --endpoint-url=http://localhost:4566 sns list-topics
```

## DELETE TOPIC
```
aws --endpoint-url=http://localhost:4566 sns delete-topic --topic-arn arn:aws:sns:us-east-1:000000000000:test_topic
```