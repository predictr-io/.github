# Predictr.io GitHub Actions

A collection of reusable GitHub Actions for **AWS** and **GCP** cloud services. Build powerful CI/CD workflows with infrastructure automation, messaging, storage, and monitoring integrations across multiple clouds.

## 🌩️ Multi-Cloud Support

### Amazon Web Services (AWS)

#### Messaging & Streaming
- **[aws-sqs-create-queue](https://github.com/predictr-io/aws-sqs-create-queue)** - Create Amazon SQS queues
- **[aws-sqs-delete-queue](https://github.com/predictr-io/aws-sqs-delete-queue)** - Delete Amazon SQS queues
- **[aws-sqs-send-message](https://github.com/predictr-io/aws-sqs-send-message)** - Send messages to SQS queues
- **[aws-sns-create-topic](https://github.com/predictr-io/aws-sns-create-topic)** - Create SNS topics
- **[aws-sns-delete-topic](https://github.com/predictr-io/aws-sns-delete-topic)** - Delete SNS topics
- **[aws-sns-send-message](https://github.com/predictr-io/aws-sns-send-message)** - Publish messages to SNS topics
- **[aws-kinesis-send-message](https://github.com/predictr-io/aws-kinesis-send-message)** - Send records to Kinesis streams
- **[aws-firehose-create-stream](https://github.com/predictr-io/aws-firehose-create-stream)** - Create Kinesis Data Firehose delivery streams
- **[aws-firehose-delete-stream](https://github.com/predictr-io/aws-firehose-delete-stream)** - Delete Firehose delivery streams
- **[aws-firehose-send-message](https://github.com/predictr-io/aws-firehose-send-message)** - Send records to Firehose streams

#### Data & Analytics
- **[aws-glue-crawler](https://github.com/predictr-io/aws-glue-crawler)** - Run AWS Glue crawlers
- **[aws-glue-partition-manager](https://github.com/predictr-io/aws-glue-partition-manager)** - Manage Glue table partitions

#### Monitoring
- **[aws-cloudwatch-put-metrics](https://github.com/predictr-io/aws-cloudwatch-put-metrics)** - Send custom metrics to CloudWatch

#### Storage
- **[url-to-s3](https://github.com/predictr-io/url_to_s3)** - Download files from URLs and upload to S3

### Google Cloud Platform (GCP)

#### Messaging
- **[gcp-pubsub-send-message](https://github.com/predictr-io/gcp-pubsub-send-message)** - Publish messages to Google Cloud Pub/Sub topics

#### Storage
- **[url-to-gcs](https://github.com/predictr-io/url-to-gcs)** - Download files from URLs and upload to Google Cloud Storage

## 🚀 Getting Started

All actions are available on the GitHub Marketplace and can be used in your workflows:

```yaml
- name: Send message to GCP Pub/Sub
  uses: predictr-io/gcp-pubsub-send-message@v0
  with:
    project-id: 'my-gcp-project'
    topic-name: 'my-topic'
    message: 'Hello from GitHub Actions!'

- name: Send message to AWS SQS
  uses: predictr-io/aws-sqs-send-message@v0
  with:
    queue-url: 'https://sqs.us-east-1.amazonaws.com/123456789/my-queue'
    message-body: 'Hello from GitHub Actions!'
```

## 📚 Documentation

Each action has comprehensive documentation including:
- ✅ Usage examples
- ✅ Input parameters
- ✅ Authentication setup
- ✅ Local development/testing guides

Visit individual repositories for detailed documentation.

## 🤝 Contributing

We welcome contributions! Please feel free to submit issues or pull requests.

## 📄 License

All actions are licensed under the MIT License.