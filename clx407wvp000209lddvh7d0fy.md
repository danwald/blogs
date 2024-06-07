---
title: "AWS Summit Dubai '24: Notes"
datePublished: Fri Jun 07 2024 01:24:57 GMT+0000 (Coordinated Universal Time)
cuid: clx407wvp000209lddvh7d0fy
slug: aws-summit-dubai-24-notes
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/rymh7EZPqRs/upload/7af04dcdecce785e4b1544d298e7fec1.jpeg
tags: aws, amazon-web-services, generative-ai, amazon-bedrock, amazon-q-developers

---

I attended the AWS summit at the Dubai World Trade center's Sheikh Saeed Halls May 29th 2024. Here are some of the notes of the sessions that I was able to attend from over 30+ going on throughout the day.

[AWS Bedrock](https://aws.amazon.com/bedrock/) is a managed solution using commercially available ([Claude](https://claude.ai/), [llama](https://llama.meta.com/) etc) foundation models which can be fine tuned with your private corpus that respects embedded ACL (access control) of the content to allow for Generative AI applications to provide semantic answers to your questions. The data only augments the base model and is always kept private. Generative AI models train on complex data to produce a complex output which is unlike the simple output of its predecessors, deep learning and machine learning. Ubiquitous computing power, transformers and multi-headed attention techniques are the boon of these powerful foundation models.

A vendor, [Dynatrace](https://www.dynatrace.com/) ingests about 500TB/day of client's telemetry data into its proprietary database using an agent (API also available), that it analyzes to ofter context of your system accessible via a query language.

[AWS Q Developer](https://aws.amazon.com/q/developer/) (previously Code Whisperer) is part of its Generative AI tooling catered towards developers built on top of [AWS Bedrock](https://aws.amazon.com/bedrock/). Privacy is at the forefront, so your code and augmented model is kept private. Apparently, developers only spend 25% of their time creating code. They aim to increase that and reduce the friction within the SDLC (create/test/operate/maintain). It provides copilot support helping to debug, refactor, optimize, explain, analyze security vulnerabilities, add documentation, write tests and even upgrade (Java) code right within your IDE.

A [local web company](https://www.propertyfinder.ae/) utilizes [cloudfront](https://aws.amazon.com/cloudfront/) functions for straightforward use cases and lambda's at the edge for more complicated flows (even for agent detection to apply the appropriate headers to get more CDN hits) allowing them to decrease their response times by 30% effectively increasing their crawl hit rate and significantly improved their organic traffic. They also used [firehose](https://aws.amazon.com/firehose/) to aggregate their multi regional logs into a centralized S3 bucket leveraging [Athena's](https://aws.amazon.com/athena/) querying capabilities for real time view of stats.

A [local consulting company](https://bluepiit.com/), used the OpenAI's [Whisper](https://openai.com/index/whisper/) foundational model within [AWS Bedrock](https://aws.amazon.com/bedrock/) to overcome the hard problem of diarization to analyze customer multi-language/dialect support calls. They improved satisfaction scores and allowed agents to provide accurate upsell recommendations from their extensive product catalog. For another client they were able to ingest their [CloudTrail](https://docs.aws.amazon.com/cloudtrail/) and [CloudWatch](https://docs.aws.amazon.com/cloudwatch/) content to build a generative AI chat bot to answer billing and user access questions posed by the CFO or CTOs of the company. Working with structured data, they used generative AI to build SQL queries to answer aggregation (last week's, this quarter, etc) prompts for reports.

As opposed to fine tuning, Prompt engineering is an easier tactic to get the answers you're looking for from your pre-built model. You have to 'treat it like a child' providing clear and concise questions, with illustrative directives on what you expect as part of the instruction phase. You can also provide example output also known as one or multi-shot. There's also the option of going into a chain of thought dialogue.

Lastly, [Amplify](https://aws.amazon.com/amplify/) has moved to typescript which promises faster full stack development and deployments by your frontend engineers.

It was an informative day with way more going on than what I covered. There were a lot of vendors and some interesting exhibits too. The coffee was decent and the lunch was not too bad either.

I hope to catch it next year as well.

### References:

* [https://aws.amazon.com/bedrock/](https://aws.amazon.com/bedrock/)
    
* [https://claude.ai/](https://claude.ai/)
    
* [https://llama.meta.com/](https://llama.meta.com/)
    
* [https://www.dynatrace.com/](https://www.dynatrace.com/)
    
* [https://aws.amazon.com/q/developer/](https://aws.amazon.com/q/developer/)
    
* [https://www.propertyfinder.ae/](https://www.propertyfinder.ae/)
    
* [https://aws.amazon.com/cloudfront/](https://aws.amazon.com/cloudfront/)
    
* [https://aws.amazon.com/firehose/](https://aws.amazon.com/firehose/)
    
* [https://aws.amazon.com/athena/](https://aws.amazon.com/athena/)
    
* [https://bluepiit.com/](https://bluepiit.com/)
    
* [https://openai.com/index/whisper/](https://openai.com/index/whisper/)
    
* [https://docs.aws.amazon.com/cloudtrail/](https://docs.aws.amazon.com/cloudtrail/)
    
* [https://docs.aws.amazon.com/cloudwatch/](https://docs.aws.amazon.com/cloudwatch/)
    
* [https://aws.amazon.com/amplify/](https://aws.amazon.com/amplify/)