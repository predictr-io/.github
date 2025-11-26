# predictr.io GitHub Actions

**Test your data pipelines like you mean it.**

A collection of GitHub Actions for building, testing, and managing cloud-native data workflows. Stop mocking AWS services—spin them up for real in your CI/CD pipeline.

## 🚀 What We Build

Production-grade GitHub Actions that let you:
- **Create real infrastructure** in your workflows (SQS, SNS, Firehose, Glue)
- **Test against actual services** using LocalStack or AWS
- **Clean up automatically** with matching delete actions
- **Move fast** with simple, focused actions that do one thing well

## ✨ Workflow Editor

<a href="https://gate.predictr.io" target="_blank"><img src="https://gate.predictr.io/gate.png" alt="GATE" height="60"></a>

Want context-aware editing with inline documentation? Try **<a href="https://gate.predictr.io" target="_blank">gate.predictr.io</a>** - a specialized editor for GitHub Actions workflows with built-in parameter documentation and action discovery.

## 🤔 Why Use These Actions?

**"Why not just run `aws` commands in a script step?"**

Good question! Here's why actions are better:

### ✅ **Better Developer Experience**
- **Type-safe inputs** - Catch mistakes before runtime
- **Clear error messages** - Know exactly what went wrong, no cryptic AWS errors
- **Self-documenting** - Your workflow explains what it does
- **IDE support** - Autocomplete and validation in your editor

### ✅ **Cleaner Workflows**
```yaml
# ❌ Script approach - hard to read, easy to break
- run: |
    aws sqs create-queue --queue-name test-queue \
      --attributes VisibilityTimeout=60,MessageRetentionPeriod=345600 \
      --tags Environment=test,Team=backend
    QUEUE_URL=$(aws sqs get-queue-url --queue-name test-queue --query 'QueueUrl' --output text)
    echo "queue_url=$QUEUE_URL" >> $GITHUB_OUTPUT

# ✅ Action approach - obvious and maintainable
- uses: predictr-io/aws-sqs-create-queue@v0
  id: queue
  with:
    queue-name: 'test-queue'
    visibility-timeout: '60'
    tags: '{"Environment": "test", "Team": "backend"}'
```

### ✅ **Consistent & Reusable**
- Same patterns across all AWS services
- No need to remember AWS CLI syntax for each service
- Copy examples from README, adapt, done
- Works the same way in every repository

### ✅ **Built-in Best Practices**
- Proper error handling and retries
- Input validation before hitting AWS
- Output formatting ready for next steps
- LocalStack support out of the box

### ✅ **No AWS CLI Installation**
- Actions use AWS SDK directly (faster, smaller)
- No need to install/update CLI tools
- Consistent AWS SDK versions
- Better performance in GitHub Actions runners

### ✅ **Tested & Maintained**
- Manually tested against real AWS and LocalStack
- Bugs fixed once, benefit everyone
- Version pinning for stability
- Active maintenance and updates

## 📦 Available Actions

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

### Amazon Kinesis Data Firehose
- **[aws-firehose-create-stream](https://github.com/predictr-io/aws-firehose-create-stream)** - Create delivery streams (simplified for testing)
- **[aws-firehose-send-message](https://github.com/predictr-io/aws-firehose-send-message)** - Send records to streams
- **[aws-firehose-delete-stream](https://github.com/predictr-io/aws-firehose-delete-stream)** - Clean up test streams

### AWS Glue
- **[aws-glue-crawler](https://github.com/predictr-io/aws-glue-crawler)** - Run crawlers to discover & catalog data
- **[aws-glue-partition-manager](https://github.com/predictr-io/aws-glue-partition-manager)** - Add, delete, check partition existence

## 💡 Quick Example

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

      # Track metrics
      - name: Record test completion
        if: always()
        uses: predictr-io/aws-cloudwatch-put-metrics@v0
        with:
          namespace: 'MyApp/CI'
          metric-data: |
            [{"MetricName": "TestsCompleted", "Value": 1, "Unit": "Count"}]

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

## 🎯 Design Principles

- **Simple & Focused** - Each action does one thing well
- **Test-Friendly** - Works with LocalStack out of the box
- **Production-Ready** - All actions work with real AWS too
- **Clean Workflows** - Matching create/delete actions for easy cleanup
- **Consistent** - Same patterns across all services

## 🤝 Contributing

Found a bug? Want a new action? Contributions welcome!

1. Open an issue to discuss your idea
2. Submit a PR with tests
3. Follow our existing patterns for consistency

## 📝 License

All actions are MIT licensed. Use them freely!

---

Built with ☕ for teams who ship data products.
