# Data Pipeline ShellCommandWithS3StagingDirectory Sample

## Overview

This sample shows how to build a Shell Command Activity pipeline that uses a S3 directory for staging. Specifically, this sample runs a script that is located in a s3 bucket and takes an argument string. The script simply prints out the argument to stdout.

## Prerequisites

You must have the AWS CLI and default IAM roles setup in order to run the sample. Please see the [readme](https://github.com/awslabs/data-pipeline-samples) for the base repository for instructions how to do this.

You must also provide the S3Path of a S3 bucket with write permissions. See [here](http://docs.aws.amazon.com/AmazonS3/latest/UG/CreatingaBucket.html) for instructions on how to create an S3 bucket.

You must also upload *bashscript.sh* to your s3 bucket.

## Run this sample pipeline using the AWS CLI

```sh 
  $> aws datapipeline create-pipeline --name shell_command_staging_pipeline --unique-id shell_command_staging_pipeline
```

You receive a pipelineId like this. 
```sh
  #   -----------------------------------------
  #   |             CreatePipeline             |
  #   +-------------+--------------------------+
  #   |  pipelineId |  <Your Pipeline ID>      |
  #   +-------------+--------------------------+
```

```sh
  $> aws datapipeline put-pipeline-definition --pipeline-definition file://shellcommandwiths3stagingdir.json --parameter-values myS3StagingPath=<s3://your/s3/staging/path> myS3LogsPath=<s3://your/s3/logs/path> --pipeline-id <Your Pipeline ID> 
```

You receive a validation messages like this
```sh
  #   ----------------------- 
  #   |PutPipelineDefinition|
  #   +-----------+---------+
  #   |  errored  |  False  |
  #   +-----------+---------+
```

Now activate the pipeline
```sh
  $> aws datapipeline activate-pipeline --pipeline-id <Your Pipeline ID>
```

Check the status of your pipeline 
```
  >$ aws datapipeline list-runs --pipeline-id <Your Pipeline ID>
```

You will receive status information on the pipeline.  
```sh
  #       Name                                                Scheduled Start      Status
  #       ID                                                  Started              Ended
  #---------------------------------------------------------------------------------------------------
  #   1.  ActivityId_6OGtu                                    2015-07-29T01:06:17  WAITING_ON_DEPENDENCIES
  #       @ActivityId_6OGtu_2015-07-29T01:06:17               2015-07-29T01:06:20
  #
  #   2.  ResourceId_z9RNH                                    2015-07-29T01:06:17  CREATING
  #       @ResourceId_z9RNH_2015-07-29T01:06:17               2015-07-29T01:06:20
  #
  #       @ActivityId_wQhxe_2015-07-29T01:06:17               2015-07-29T01:06:20
```


## Disclaimer

The samples in this repository are meant to help users get started with Data Pipeline. They may not be sufficient for production environments. Users should carefully inspect code samples before running them.

Use at your own risk.

Copyright 2011-2013 Amazon.com, Inc. or its affiliates. All Rights Reserved.

Licensed under the Amazon Software License (the "License"). You may not use this file except in compliance with the License. A copy of the License is located at

http://aws.amazon.com/asl/
