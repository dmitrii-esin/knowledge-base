## Cloud Core Concepts

### What is the Cloud?

The cloud provides a way of abstracting, pooling, and sharing computing resources—like servers, switches, routers, operating systems, and security software—across a network of devices on or off the premises. Cloud computing refers to the use of these resources over the Internet. Typically, users rent computational resources like storage space or CPU power, while the cloud provider actively manages the hardware (e.g. storage drives and servers) that provide those computational resources. Cloud providers also offer higher level services that analyze data, support disaster recovery, or act as development environments—all of which run on cloud provider hardware.

It may be helpful to think of the cloud as a massive utility like a water or electricity service—there are many similarities.\
You use water and electricity at work and at home; usually, it is provided by a utility company via cables and pipes. You have a contract with a supplier, and you pay based on how much of these resources you use. The utility model maximizes the efficient use of resources and minimizes the associated costs.

With the cloud, you also have an up-front contract and pay based on the amount of cloud resources you consume. Typically, users rent computational resources like storage space or CPU power, while the cloud provider manages the hardware. Cloud providers also offer higher-level services that analyze data, support disaster recovery, or act as development environments.

### Cloud types - Deployment Models

Cloud types can be viewed from different perspectives—for example, according to the various deployment models or based on customer needs.

Private cloud | Public cloud | Hybrid cloud | Multi-cloud

Private cloud service runs on dedicated hardware. It often serves as a bridge between the public cloud and legacy on-premises systems. A private cloud's capacity is static, based on how much storage has been paid for; it can be run internally or by an independent contractor.
This is a step toward a public cloud for many organizations, allowing solutions around security and data sovereignty to be resolved before moving to a public cloud.

Public clouds are run by a specialist provider in their data centers and are accessible via the internet or private connections. They do not require an independent data center space for system maintenance or the purchase of hardware or software.\
Moving to a public cloud is an economical solution for organizations seeking to avoid capital expenses. However, if you are considering migration, you will want to thoroughly assess your cloud provider's security model; the public cloud is only a good deal if it keeps your data secure.

Hybrid clouds are computing environments that use a mixture of on-premises data storage, private cloud, and third-party public cloud services. These environments work together to perform a single task. A combination of these environments allows businesses to fulfill their unique needs by tailoring which services they use—for example, your organization may not be ready to move to the cloud entirely or may have some highly sensitive data that you'd rather store in a private cloud.

Multi-cloud is a strategy in which multiple computing and storage services are used in a single heterogeneous architecture. It aims to distribute cloud assets, software, and applications across several cloud-hosting environments, eliminating the need to rely on a single provider.\
This approach differs from a hybrid cloud in that the cloud services can function either independently or together, as opposed to multiple types of infrastructure functioning collectively (e.g., a data center, private cloud, and a public cloud).

*For example, an established organization with existing data centers might favor a hybrid cloud model or even a mixture of traditional on-premises infrastructure and some Agile cloud infrastructure. As your organizational needs change, your cloud strategy should also be reviewed to make sure it aligns with any changes in your business goals.

### Cloud types - Customer Needs

In addition to considering different deployment types, any strategy for moving to the cloud should take into account the customer's point of view as well. Why do they need a cloud (e.g., for business or personal use)? Are they planning to implement the system using in-house resources, or would it be better to outsource the task?
<img width="802" alt="image" src="https://user-images.githubusercontent.com/8881978/207671359-01950b04-73ff-46e6-bafc-900a637989f2.png">

### Cloud Service Models

- Software as a Service (SaaS)\
V
- Platform as a Service (PaaS)\
V
- Infrastructure as a Service (IaaS)

<img width="963" alt="image" src="https://user-images.githubusercontent.com/8881978/210117584-580fe0fb-d29b-43d2-94ae-83a5ac72178a.png">

### Migration to the Cloud

<img width="952" alt="image" src="https://user-images.githubusercontent.com/8881978/210265646-c8c1f963-fe68-41d7-8b5b-a581827ac73e.png">

### Public Cloud Platforms Overview

<img width="1384" alt="image" src="https://user-images.githubusercontent.com/8881978/210267330-e53e4282-310a-4286-8ee2-d00f99e7ace0.png">


***

## First thing to start working with AWS
1. Root account -> IAM user -> roleas and groups
2. Create billing alerts on billing page and CloudWatch

***

## what is a cloud
types of arch (monolith, microservices)\
types of services (On-premise, IAAS, PAAS, SAAS)\
concepts (what for, 5 pillars, regions and az, etc.: https://aws.amazon.com/ru/getting-started/fundamentals-core-concepts/ \
architecture: http://d0.awsstatic.com/whitepapers/International/ru/AWS_Serverless_Multi-Tier_Architectures_RU

## По микросервисам:
Shared БД, вынесение утилитарных функций и отделение инфры от бизнес-логики - это не микросервисы, микросервисы это именно деление домена (например, отдельно getProducts, отдельно getProductById)\
Есть проблемы с шарингом утилитарных функций = поменяем общую функцию и все сервисы передеплоятся иди что-то сломается

## services
### IAM 
(user, role, group, root user, policies)
https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
### S3 
(bucket, object)
### Cloudfront 
(origin, distribution list, edge locations)
### CloudFormation 
(IaC, json\yaml, stacks)
### Lambda 
(дёшево, но есть проблемы: cold start + ограничения типа stateless и природы event-bases, лечится соблюдением правил + оптимизацией кода + доп. приблудами вроде lambda warmup) \
Отдельно про Lambda стоит отметить разницу между использованием фреймворка внутри одной лямбды (упростили роутинг, но должны контролировать логирование и прочее сами) от разных лямбд на каждый тип запроса (всё логируется нативно aws'ом), разные роли, дешевле разные лямбы
### lambda warmup:
https://aws.amazon.com/ru/blogs/compute/new-for-aws-lambda-predictable-start-up-times-with-provisioned-concurrency/
https://medium.com/proud2becloud/a-comprehensive-analysis-of-aws-lambda-function-optimize-spikes-and-prevent-cold-starts-57942be5748e
https://lumigo.io/aws-lambda-performance-optimization/how-to-improve-aws-lambda-cold-start-performance/
### Как лямбда попадает в aws: транспиляция, затем при помощи serverless создаётся cloud formation, затем т.к. машина связана с аккаунтом происходит разворачивание ресурсов в aws (cloudformation создает граф заивисомости или стэк ресурсов - cloudwatch, lambda, api gateway)
lambda TS -> lambda JS -> cloudformation -> blue-green deployment
### Оптимизация, позволяющая переиспользовать код между лямбами: 
https://www.serverless.com/blog/publish-aws-lambda-layers-serverless-framework/
### Тестирования лямбды локально и изолированно: 
serverless-offline (протестировать полность), cli serverless invoke local (тестируем конкретную лямбду с передачей параметров)
### Тестирование сервисов полностью: 
serverless local plugin (как-то так)
### API Gateway
(прокси для связывания сервисов по api)

## documentation
https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-export-api.html
https://www.serverless.com/plugins/serverless-openapi-documentation

## communication with cloud 
console (registration, budget, services, etc.)\
sdk (serverless, serverless-finch, serverless.yml, etc.)\
api\
cli (aws configure)\
credentials: ~/.aws/credentials\
способы работы с aws: serverless, aws cli, aws sam, terraform, cloudformation

## serverless
IAC
serverless.yml - парсится пакетом serverless и далее serverless создает более многословные файлы-конфиги для CloudFormation\
использование переменных окружения и профилей в serverless.yml - пробросить переменную окружения  и настройку --aws-profile при деплое (CLI: sls deplout --aws- ...)

## node packages
есть 2 способа доабвления пакета - указать в dependeices адрес как "file://.kokoko" либо установить в node_modules (для serverless достаточно положить плагин в ./serverless_plugins

## billing
https://calculator.s3.amazonaws.com/index.html
https://calculator.aws/#/

## aws examples and arch templates:
https://github.com/aws-samples
https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html?icmpid=docs_lambda_console
https://github.com/awsdocs/aws-lambda-developer-guide/blob/main/sample-apps/nodejs-apig/function/index.js
https://aws.amazon.com/ru/architecture/

## VSCode and AWS: 
https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/welcome.html

## Best practices for organizing larger serverless applications
https://aws.amazon.com/ru/blogs/compute/best-practices-for-organizing-larger-serverless-applications/

## DB theory
типы бд, утройство бд, отличия, сервер бд, шардинг и репликация
индексы в реаляционках (типы индексов)\
отношения (one-to-one, one-to-many - пример: некоторых из коллекции users есть разные наборы settings, many-to-many)\
SQL (query types: DDL - data definition, DML - data manipulation, TCL - transaction control, DCL - data control), joins
Db in cloud: EC2, rds, eks 
(всё хорошо с консистентностью, быстрое чтение, долгая запись)\
NOSQL (быстрая запись, конкретно у MongoDB большие возможности по агрегации, но у таких бд есть проблемы с консистентностью данных)
BidData (Redshift)\
Виды бд в aws: RDS (relational db service supports multiple engines - posgres, mysql, oracle, etc.), DynamoDB (nosql key-value, like Cassandra), Aurora, Aurora Serverless (relational), Neptune (graph DB), DocumentDB (nosql document db, mongodb-compatibe), Redshift (columnar db, using for bigdata), ElasticCahe (redis or memcached db)

## AWS storages
EBS, EFS, S3, Backup, CloudFront, etc.\
S3 use cases: storing static content and serving for the users, internal project data, logs and audit, bakups, etc.\
S3 details: permissions and policies (IAM policies, S3 policies), replication (cross-region or same-region), types of encryption, types of storages, versioning, working with data using sql, etc.

## Для коммуникации lambda c S3 нужно много параметров: 
1. в serverless.ts необходимо указать iam.role.statements со списком действий, которые может совершать с бакетом лямбда
2. в настройках самого бакета необходимо указать bucket policy (какие действия можно совершать с бакетом) и cors (если надо)
3. В настройках конкретной лямбды указать нужный триггер, например event: "s3:ObjectCreated:*".\
*метод s3.getSignedUrl позволяет создать ссылку для передачи файла в бакет (нужно использовать, т.к. лямда имеет ограничение на payload 6mb)

## SQS & SNS
Сервисы для управления очередями сообщений.\
Async communication between parts of the system via messages\
Альтернативы - Kafka, rabbit MQ, etc.
### SQS
Simple Queue Service - poll-based by queues, queuing service using messages with a queue for application integration and decouple apps to talk to each other (poll-based, тоесть сами достаём из очереди что нам нужно, сообщение будет удалено из очереди только когда consumer сообщит об окончании удачной обработки, имеет 2 типа очереди - standard, fifo).\
Части системы: queue, producer, consumer.\
Особенности и ограничания SQS - безлимитное кол-во очередей и сообщений, размер сообщения 256кб (можно увеличить, используя библиотеки с использованием S3 подкапотом), сообщения лучше отправлять "батчами", очередь поддерживает long-polling.
### SNS
Simple Notification Service - push-based by topics, pub\sub messaging system to decouple microservices, applications  and distributed systems (pub/sub, publishers sends messages to event bus and grouping, not to receiver, and subscribers can subscribe to interesting event groups)\
Части системы - topic, на него можно подписаться\
Есть 2 типа топиков - fifo, standard (по аналогии с SQS)

## Зачем нам нужен API Gateway всегда нужен для получения запросов
Очередь не говорит, что сразу же сообщение придёт к адресату, а api gateway гарантирует, со многими сервисами коммуникация через очереди, а не через api, т.к. immediate-респонс не всегда нужен.\
Очередями удобно решать проблемы упавших запросов к базе или к другим сервисам.\
Сообщения в очереди имеют настройку retry - т.е. при фейле они будут сохранены и применены снова.

## Разница синхронная - асинхронная коммуникация
- Синхронная - пользователь ждёт ответ сейчас.
- Асинхронная - как правило между сервисами (очереди итд).

## CloudWatch
alarm - умеет подписываться на зафейленные события типа очередей

## Авторизация 
### (3 этапа):
1. Идентификация (клиент называет себя)
2. Аутентификация (клиент предоставляет доказательства, что он это он, а сервер проверяет)
3. Авторизация (сервер предоставляет права на запрашиваемые ресурсы согласно правилам, после аутентификации)
### Основные типы авторизации http:
- Basic 
- Bearer
- Api keys
- Cookies
- Third party services (SSO через соцсети, например)
- Oauth

### Working with AWS Lambda authorizers for HTTP APIs
https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-lambda-authorizer.htm

### Use API Gateway Lambda authorizers
https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-use-lambda-authorizer.html

### Authorization in details
https://www.google.com/amp/s/m.habr.com/ru/amp/post/262817/

### Как работает авторизация в aws (своими словами):
1. Создаём и настраиваем авторизационную лямбду
2. Подключаем авторизационную лямбду в aws console или через serverless с необходимым маршрутам с необходимыми параметрами
3. Всё

### Cognito
aws-сервис для авториации\
состоит из 2-х частей: user pool (работает с пользователями), identity pool (работаем с доступами aws-сервисов)

### Способы имплементации авторизации в AWS
- custom authorizer lambda
- cognito authorizer

## Docker
матчасть\
отличие от виртуальных машин\
слои в образе

## Elastic Beanstalk
средство развертывания готовых написанных приложений из докер-образов (сам масштабирует, выделяет ресурсы и т.д.)\
в сравнении с ECS -  имеет меньшее кол-во настроек и не требует подробной кастомизации\
есть свой eb cli\
Небольшая особенность в случае использования BFF nodejs - сам EB предоставляет порт для работы приложения, но чтобы запустить локально нам нужно указать свой порт вот так: const PORT = process.env.PORT || 3001.