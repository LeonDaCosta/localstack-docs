---
title: "Openflow"
description: Get started with Openflow in LocalStack for Snowflake
tags: ["Base"]
---

## Introduction
Openflow is Snowflake’s data movement service that provides a unified platform for building, scaling, and managing data pipelines. It is powered by Apache NiFi and enables flexible data ingestion, transformation, and integration across diverse sources and destinations.

The Snowflake emulator in LocalStack supports **basic Openflow functionality** by exposing an Apache NiFi–based UI. This allows you to experiment locally with Openflow concepts, such as creating processors and running SQL queries against the Snowflake emulator.

You can access the Openflow UI when the emulator is running at:

```
https://snowflake.localhost.localstack.cloud:4566/openflow/
```

:::note
Openflow is Snowflake is intended for local experimentation. It does not provide the full set of managed Openflow capabilities available in Snowflake’s cloud platform.
:::

## Getting started
To begin using Openflow in LocalStack:

1. Start your Snowflake emulator.
2. Open the following URL in your browser: `https://snowflake.localhost.localstack.cloud:4566/openflow/`


The first load may take some time, as Apache NiFi dependencies are downloaded and initialized.

Once the UI is available, you can create and configure NiFi processors directly in your browser.

## Example: Running a query with ExecuteSQL
The following example demonstrates how to run a simple query against the Snowflake emulator using the `ExecuteSQL` processor.

1. Add an ExecuteSQL processor: Drag the `ExecuteSQL` processor onto the canvas in the Openflow UI.

2. Configure the processor:
- Set the **Database Connection Pooling Service** to use the default `Snowflake Connection Pool`.
- Enter a query, for example:

```sql
SELECT 123;
```

- In the **Relationships** tab, configure the processor to terminate or retry on `failure` and `success`.

3. Start the processor: Right-click the processor and choose **Start**. The processor will run the SQL query against the Snowflake emulator.

4. Verify execution: In the emulator logs, you should see the executed query:

```
Running query (account/DB/schema TEST/TEST/public): SELECT 123
```

:::note
## Limitations
- The initial download of Apache NiFi is large (~750 MB) and may take several minutes.  
- Integration tests for this feature are disabled in CI due to the heavy binary size.  
- Only basic UI and processor creation are supported. Advanced Openflow functionality, including governance, AI capabilities, and managed connectors, is not included in the local emulator.
:::