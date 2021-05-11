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

## LIST TOPICS
```
aws --endpoint-url=http://localhost:4566 sns list-topics
```