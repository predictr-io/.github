# predictr.io GitHub Actions

**Build ML-powered data pipelines in your CI/CD.**

GitHub Actions for creating **machine learning analyses** (forecasting, customer segmentation, market basket analysis) and building cloud-native data workflows on **AWS** and **GCP**. Stop mocking cloud services—spin them up for real in your CI/CD pipeline.

## 🚀 What We Build

Production-grade GitHub Actions that let you:
- **Create real infrastructure** in your workflows (SQS, SNS, Pub/Sub, Firehose, Glue)
- **Test against actual services** using LocalStack, Pub/Sub Emulator, or real cloud environments
- **Build ML analyses** via predictr.io (time series forecasting, customer clustering, market basket analysis)
- **Automate model training** and predictions as part of your data pipelines
- **Clean up automatically** with matching delete actions
- **Move fast** with simple, focused actions that do one thing well

## ✨ Workflow Editor

<a href="https://github.com/marketplace/actions-editor" target="_blank"><img src="https://gate.predictr.io/gate.png" alt="GATE" height="60" align="left" style="margin-right: 15px;"></a>

Want context-aware editing with inline documentation? Try **<a href="https://github.com/marketplace/actions-editor" target="_blank">GATE - the GitHub Actions Template Editor</a>** - a specialized editor for GitHub Actions workflows with built-in parameter documentation and action discovery.

## 🤔 Why Use These Actions?

**"Why not just run `aws` or `gcloud` commands in a script step? Or call ML APIs directly?"**

Good question! Here's why actions are better:

### ✅ **Better Developer Experience**
- **Type-safe inputs** - Catch mistakes before runtime (no more typos in column names or thresholds)
- **Clear error messages** - Know exactly what went wrong, no cryptic cloud provider or API errors
- **Self-documenting** - Your workflow explains what it does (both infrastructure and ML models)
- **IDE support** - Autocomplete and validation in your editor

### ✅ **Cleaner Workflows**
```yaml
# ❌ Script approach - hard to read, easy to break
- run: |
    aws sqs create-queue --queue-name test-queue \
      --attributes VisibilityTimeout=60,MessageRetentionPeriod=345600 \
      --tags Environment=test Team=backend
    QUEUE_URL=$(aws sqs get-queue-url --queue-name test-queue --query 'QueueUrl' --output text)
    echo "queue_url=$QUEUE_URL" >> $GITHUB_OUTPUT

# ✅ Action approach - obvious and maintainable
- uses: predictr-io/aws-sqs-create-queue@v0
  id: queue
  with:
    queue-name: 'test-queue'
    visibility-timeout: '60'
    message-retention-period: '345600'
    tags: '{"Environment": "test", "Team": "backend"}'
```

### ✅ **Consistent & Reusable**
- Same patterns across all cloud services (AWS & GCP) and ML actions
- No need to remember CLI syntax or API endpoints for each service
- Copy examples from README, adapt, done
- Works the same way in every repository

### ✅ **Built-in Best Practices**
- Proper error handling and retries
- Input validation before hitting cloud APIs or training models
- Output formatting ready for next steps (queue URLs, analysis IDs, model metrics)
- Emulator/LocalStack support out of the box for infrastructure testing

### ✅ **No CLI Installation**
- Actions use cloud SDKs directly (faster, smaller)
- No need to install/update CLI tools
- Consistent SDK versions
- Better performance in GitHub Actions runners

### ✅ **Tested & Maintained**
- Manually tested against real cloud services and emulators
- Bugs fixed once, benefit everyone
- Version pinning for stability
- Active maintenance and updates

## 📦 Available Actions

### 🤖 Machine Learning Analysis

- **[predictr-forecast-analysis](https://github.com/predictr-io/predictr-forecast-analysis)** - Time series forecasting with Prophet (daily, weekly, hourly), holidays, seasonality, custom events, regressors
- **[predictr-mba-analysis](https://github.com/predictr-io/predictr-mba-analysis)** - Market Basket Analysis to discover product associations and purchase patterns
- **[predictr-rfm-clustering](https://github.com/predictr-io/predictr-rfm-clustering)** - Customer segmentation using RFM (Recency, Frequency, Monetary) clustering

### Amazon CloudWatch
- **[aws-cloudwatch-put-metrics](https://github.com/predictr-io/aws-cloudwatch-put-metrics)** - Publish custom metrics (track deployments, build times, test results)

### Amazon SQS
- **[aws-sqs-create-queue](https://github.com/predictr-io/aws-sqs-create-queue)** - Create standard & FIFO queues
- **[aws-sqs-send-message](https://github.com/predictr-io/aws-sqs-send-message)** - Send messages with attributes & deduplication
- **[aws-sqs-delete-queue](https://github.com/predictr-io/aws-sqs-delete-queue)** - Clean up test queues

### Amazon SNS
- **[aws-sns-create-topic](https://github.com/predictr-io/aws-sns-create-topic)** - Create standard & FIFO topics
- **[aws-sns-send-message](https://github.com/predictr-io/aws-sns-send-message)** - Publish messages to topics
- **[aws-sns-delete-topic](https://github.com/predictr-io/aws-sns-delete-topic)** - Clean up test topics

### Google Cloud Pub/Sub
- **[gcp-pubsub-create-topic](https://github.com/predictr-io/gcp-pubsub-create-topic)** - Create Pub/Sub topics with labels, retention, schemas
- **[gcp-pubsub-delete-topic](https://github.com/predictr-io/gcp-pubsub-delete-topic)** - Delete Pub/Sub topics
- **[gcp-pubsub-create-subscription](https://github.com/predictr-io/gcp-pubsub-create-subscription)** - Create pull/push subscriptions
- **[gcp-pubsub-delete-subscription](https://github.com/predictr-io/gcp-pubsub-delete-subscription)** - Delete subscriptions
- **[gcp-pubsub-send-message](https://github.com/predictr-io/gcp-pubsub-send-message)** - Publish messages to topics

### Amazon Kinesis Data Firehose
- **[aws-firehose-create-stream](https://github.com/predictr-io/aws-firehose-create-stream)** - Create delivery streams (simplified for testing)
- **[aws-firehose-send-message](https://github.com/predictr-io/aws-firehose-send-message)** - Send records to streams
- **[aws-firehose-delete-stream](https://github.com/predictr-io/aws-firehose-delete-stream)** - Clean up test streams

### AWS Glue
- **[aws-glue-create-database](https://github.com/predictr-io/aws-glue-create-database)** / **[aws-glue-delete-database](https://github.com/predictr-io/aws-glue-delete-database)** - Data catalog databases
- **[aws-glue-create-table](https://github.com/predictr-io/aws-glue-create-table)** / **[aws-glue-delete-table](https://github.com/predictr-io/aws-glue-delete-table)** - Data catalog tables
- **[aws-glue-crawler](https://github.com/predictr-io/aws-glue-crawler)** - Run crawlers to discover & catalog data
- **[aws-glue-partition-manager](https://github.com/predictr-io/aws-glue-partition-manager)** - Add, delete, check partition existence

### AWS Athena
- **[aws-athena-query](https://github.com/predictr-io/aws-athena-query)** - Run SQL queries on S3 data via Athena

### Cloud Storage
- **[aws-s3-create-bucket](https://github.com/predictr-io/aws-s3-create-bucket)** / **[aws-s3-delete-bucket](https://github.com/predictr-io/aws-s3-delete-bucket)** - S3 bucket management
- **[gcs-create-bucket](https://github.com/predictr-io/gcs-create-bucket)** / **[gcs-delete-bucket](https://github.com/predictr-io/gcs-delete-bucket)** - GCS bucket management
- **[url-to-s3](https://github.com/predictr-io/url_to_s3)** / **[url-to-gcs](https://github.com/predictr-io/url-to-gcs)** - Stream data from URLs to cloud storage

## 💡 Examples

### ML + Infrastructure: Complete Forecast Pipeline
```yaml
name: Daily Forecast Pipeline

on:
  schedule:
    - cron: '0 2 * * *'

jobs:
  forecast:
    runs-on: ubuntu-latest
    steps:
      # 1. Create/update forecast
      - name: Update Sales Forecast
        id: forecast
        uses: predictr-io/predictr-forecast-analysis@v0
        with:
          api-key: ${{ secrets.PREDICTR_API_KEY }}
          organisation: my-company
          analysis-name: daily-sales
          connection-id: ${{ secrets.CONNECTION_ID }}
          table-name: SALES_DATA
          date-column: DATE
          value-column: SALES
          frequency: D
          holidays: US

      # 2. Send to downstream systems
      - name: Notify via SQS
        uses: predictr-io/aws-sqs-send-message@v0
        with:
          queue-url: ${{ secrets.QUEUE_URL }}
          message-body: |
            {
              "analysis_id": "${{ steps.forecast.outputs.analysis-id }}",
              "model_id": "${{ steps.forecast.outputs.model-id }}"
            }

      # 3. Track metrics
      - name: Publish Metrics
        uses: predictr-io/aws-cloudwatch-put-metrics@v0
        with:
          namespace: 'ML-Pipeline'
          metrics: |
            [{"metric_name": "ForecastCompleted", "value": 1, "unit": "Count"}]
```

## 💡 Quick Example

### AWS with LocalStack
```yaml
name: Test Data Pipeline

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    services:
      localstack:
        image: localstack/localstack
        ports:
          - 4566:4566
        env:
          SERVICES: sqs,sns

    steps:
      - uses: actions/checkout@v4

      # Create test infrastructure
      - name: Create SQS queue
        id: queue
        uses: predictr-io/aws-sqs-create-queue@v0
        env:
          AWS_ENDPOINT_URL: http://localhost:4566
          AWS_ACCESS_KEY_ID: test
          AWS_SECRET_ACCESS_KEY: test
          AWS_DEFAULT_REGION: us-east-1
        with:
          queue-name: 'test-queue'

      # Run your tests
      - name: Test pipeline
        run: |
          export QUEUE_URL="${{ steps.queue.outputs.queue-url }}"
          npm test

      # Clean up (always runs)
      - name: Delete test queue
        if: always()
        uses: predictr-io/aws-sqs-delete-queue@v0
        env:
          AWS_ENDPOINT_URL: http://localhost:4566
          AWS_ACCESS_KEY_ID: test
          AWS_SECRET_ACCESS_KEY: test
          AWS_DEFAULT_REGION: us-east-1
        with:
          queue-url: ${{ steps.queue.outputs.queue-url }}
```

### GCP with Pub/Sub Emulator
```yaml
name: Test GCP Pipeline

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    services:
      pubsub-emulator:
        image: gcr.io/google.com/cloudsdktool/google-cloud-cli:emulators
        ports:
          - 8085:8085

    steps:
      - uses: actions/checkout@v4

      # Create Pub/Sub topic
      - name: Create topic
        id: topic
        uses: predictr-io/gcp-pubsub-create-topic@v0
        env:
          PUBSUB_EMULATOR_HOST: localhost:8085
        with:
          project-id: 'test-project'
          topic-name: 'test-topic'

      # Create subscription
      - name: Create subscription
        uses: predictr-io/gcp-pubsub-create-subscription@v0
        env:
          PUBSUB_EMULATOR_HOST: localhost:8085
        with:
          project-id: 'test-project'
          topic-name: 'test-topic'
          subscription-name: 'test-sub'

      # Run your tests
      - name: Test pipeline
        run: npm test
```

## 🎯 Design Principles

- **Simple & Focused** - Each action does one thing well (build a model, create a queue, etc.)
- **ML + Infrastructure** - Combine machine learning with cloud infrastructure in the same workflow
- **Test-Friendly** - Infrastructure actions work with emulators and LocalStack out of the box
- **Production-Ready** - All actions work with real cloud environments and production ML pipelines
- **Clean Workflows** - Matching create/delete actions for easy cleanup
- **Multi-Cloud** - Same patterns across AWS and GCP services

## 🤝 Contributing

Found a bug? Want a new action? Contributions welcome!

1. Open an issue to discuss your idea
2. Submit a PR with tests
3. Follow our existing patterns for consistency

## 📝 License

All actions are MIT licensed. Use them freely!

---

Built with ☕ for teams who ship ML-powered data products.
