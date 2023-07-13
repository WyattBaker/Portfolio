<a id="backtotop"></a>

<h1>Documentation for AWS CloudWatch</h1>

<hr class="solid">

<h2>Table of contents</h2>

<ol style="1">
  <li><a href="#purpose">Motivations and Purpose</a></li>
  <li><a href="#collection">Data Collection</a></li>
  <li><a href="#usage">Data Usage and Processing</a></li>
  <li><a href="#table">Table Details</a></li>
  
  <ul style="list-style-type:none;">
   <li>4.1. <a href="#datatypes">CloudWatch Logs Data Types</a></li>
   <li>4.2. <a href="#flowlogfields">VPC Flow Log Fields</a></li>
  </ul>


<li><a href="#code">Code Samples</a></li>

   <ul style="list-style-type:none;">
    <li>5.1. <a href="#awscloud">AWS CloudWatch</a></li>
      <ul style="list-style-type:none;">
        <li>5.1.1. <a href="#actionscode">Actions</a></li>
      </ul>
       5.2. <a href="#awsvpc">AWS VPC Flow Logs</a>
   </ul>
 
<li><a href="#limitations">Limitations</a></li>
<li><a href="#resources">Resources</a></li>

</ol>

<hr class="solid">

<a id="purpose"></a>

<h2>Motivations and Purpose</h2>

AWS Cloudwatch is a metrics repository and provides system-wide visibility into resource utilization, application performance, and operational health. AWSCloudwatch data source in nextgen consists of two tables:

<ul>
  <li><h3><a href="https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html"><code>aws_vpc_flowlogs</code></a></h3></li>
  <li><h3><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html"><code>cloudwatchlogs</code></h3></a>
</ul>


<h3>AWS VPC Flow Logs</h3>
<p>VPC Flow Logs is a feature that captures information about the IP traffic going to and from network interfaces in VPC. Flow log data can be published to the following locations: Amazon CloudWatch Logs, Amazon S3, or Amazon Kinesis Data Firehose. After a flow log is created, it can retrieved and viewed in the log group, bucket, or delivery stream.</p>

<p>Flow logs are used for a number of tasks, including:</p>
<ul>
  <li>Diagnosing overly restrictive security group rules</li>
  <li>Monitoring the traffic that is reaching your instance</li>
  <li>Determining the direction of the traffic to and from the network interfaces</li>
  <li>Flow log data is collected outside of the path of your network traffic, and therefore does not affect network throughput or latency. You can create or delete flow logs without any risk of impact to network performance.</li>
</ul>

<p>VPC Flow logs are enabled by default for all AWS accounts.</p> 

<h4>AWS VPC Flow Logs Documentation</h4>

<p>VPC flow logs provide netflow within the AWS ecosystem. Read more about flow logs, data structure and limitations <a href="https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html">here</a>.</p>

<br>

<h3>AWS CloudWatch Logs</h3>
<p>CloudWatch Logs is integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in CloudWatch Logs. CloudTrail captures API calls made by or on behalf of your AWS account. The calls captured include calls from the CloudWatch console and code calls to the CloudWatch Logs API operations. If a trail is created, continuous delivery of CloudTrail events to an Amazon S3 bucket can be enabled, including events for CloudWatch Logs.</p>

<p>AWS CloudWatch can include application logs and system-level metrics from Amazon EC2 instances. See more information <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html">here</a>.</p>

<p>More general information about AWS CloudWatch <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html">here</a>.</p>

<hr class="solid">

<a id="collection"></a>

<h2>Data Collection</h2>

<h3>VPC Flow Logs Data Collection</h3>

<p>A flow log record represents a network flow in your VPC. By default, each record captures a network internet protocol (IP) traffic flow (characterized by a 5-tuple on a per network interface basis) that occurs within an aggregation interval, also referred to as a capture window.</p>

<p>Each record is a string with fields separated by spaces. A record includes values for the different components of the IP flow, for example, the source, destination, and protocol.</p>

<hr class="solid">

<a id="usage"></a>

<h2>Data Usage and Processing</h2>


<p>AWS CloudWatch Logs can be used to monitor, store, and access your log files from Amazon Elastic Compute Cloud (Amazon EC2) instances, AWS CloudTrail, and other sources.</p>

<p>CloudWatch Logs enables the centralization of logs from all systems, applications, and AWS services used by AIS. These Logs can then be viewed, searched for specific error codes or patterns, filtered them based on specific fields, or archived securely for future analysis.</p>


<hr class="solid">


<a id="table"></a>

<h2>Table Details</h2> 

<a id="flowlogfields"></a>

<blockquote>
<h3>VPC Flow Logs Fields</h3>

<details><summary><em>Click here to see detailed descriptions for each field within by VPC Flow Logs.</em></summary>


<table>
    <tr>
      <th>Field</th>
      <th>Description</th>
      <th>Version</th>
    </tr>
    <tr>
      <td>version</td>
      <td><p>The VPC Flow Logs version. If you use the default format, the version is 2. If you use a custom format, the version is the highest version among the specified fields. For example, if you specify only fields from version 2, the version is 2. If you specify a mixture of fields from versions 2, 3, and 4, the version is 4.</p>

<p>Parquet data type: INT_32</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>account-id</td>
      <td><p>The AWS account ID of the owner of the source network interface for which traffic is recorded. If the network interface is created by an AWS service, for example when creating a VPC endpoint or Network Load Balancer, the record might display unknown for this field.</p>

</p>Parquet data type: STRING</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>interface-id</td>
      <td><p>The ID of the network interface for which the traffic is recorded.</p>

<p>Parquet data type: STRING</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>srcaddr</td>
      <td><p>The source address for incoming traffic, or the IPv4 or IPv6 address of the network interface for outgoing traffic on the network interface. The IPv4 address of the network interface is always its private IPv4 address. See also pkt-srcaddr.</p>

<p>Parquet data type: STRING</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>dstaddr</td>
      <td><p>The destination address for outgoing traffic, or the IPv4 or IPv6 address of the network interface for incoming traffic on the network interface. The IPv4 address of the network interface is always its private IPv4 address. See also pkt-dstaddr.</p>

<p>Parquet data type: STRING</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>srcport</td>
      <td><p>The source port of the traffic.</p>

<p>Parquet data type: INT_32</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>dstport</td>
      <td><p>The destination port of the traffic.</p>

<p>Parquet data type: INT_32</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>protocol</td>
      <td><p>The IANA protocol number of the traffic. For more information, see <a href="http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml">Assigned Internet Protocol Numbers</a>.</p>

<p>Parquet data type: INT_32</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>packets</td>
      <td><p>The number of packets transferred during the flow.</p>

<p>Parquet data type: INT_64<p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>bytes</td>
      <td><p>The number of bytes transferred during the flow.</p>

<p>Parquet data type: INT_64</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>start</td>
      <td><p>The time, in Unix seconds, when the first packet of the flow was received within the aggregation interval. This might be up to 60 seconds after the packet was transmitted or received on the network interface.</p>

<p>Parquet data type: INT_64</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>end</td>
      <td><p>The time, in Unix seconds, when the last packet of the flow was received within the aggregation interval. This might be up to 60 seconds after the packet was transmitted or received on the network interface.</p>

<p>Parquet data type: INT_64</p></td>
      <td>2</td>
    </tr>
  <tr>
      <td>action</td>
      <td><p>The action that is associated with the traffic:</p>

<dl>
  <dt><code>ACCEPT</code></dt>
  <dd>The traffic was accepted.</dd>
  <dt><code>REJECT</code></dt>
  <dd>The traffic was rejected. For example, the traffic was not allowed by the security groups or network ACLs, or packets arrived after the connection was closed.</dd>
</dl>

<p>Parquet data type: STRING</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>log-status</td>
      <td><p>The logging status of the flow log:</p>
<dl>
  <dt>OK</dt>
  <dd>Data is logging normally to the chosen destinations.</dd>
  <dt>NODATA</dt>
  <dd>There was no network traffic to or from the network interface during the aggregation interval.</dd>
  <dt>SKIPDATA</dt>
  <dd>Some flow log records were skipped during the aggregation interval. This might be because of an internal capacity constraint, or an internal error.</dd>

<p>Parquet data type: STRING</p></td>
      <td>2</td>
    </tr>
    <tr>
      <td>vpc-id</td>
      <td><p>The ID of the VPC that contains the network interface for which the traffic is recorded.</p>

<p>Parquet data type: STRING</p></td>
      <td>3</td>
    </tr>
    <tr>
      <td>subnet-id</td>
      <td><p>The ID of the subnet that contains the network interface for which the traffic is recorded.</p>

<p>Parquet data type: STRING</p></td>
      <td>3</td>
    </tr>
    <tr>
      <td>instance-id</td>
      <td><p>The ID of the instance that's associated with network interface for which the traffic is recorded, if the instance is owned by you. Returns a '-' symbol for a <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/requester-managed-eni.html">requester-managed network interface</a>; for example, the network interface for a NAT gateway.</p>

<p>Parquet data type: STRING</p></td>
      <td>3</td>
    </tr>
    <tr>
      <td>tcp-flags</td>
      <td><p>The bitmask value for the following TCP flags:</p>
    <ul>
      <li>FIN — 1</li>
      <li>SYN — 2</li>
      <li>RST — 4</li>
      <li>SYN-ACK — 18</li>
    </ul>
    
    <p>If no supported flags are recorded, the TCP flag value is 0.</p>

    <p>TCP flags can be OR-ed during the aggregation interval. For short connections, the flags might be set on the same line in the flow log record, for example, 19 for SYN-ACK and FIN, and 3 for SYN and FIN. For an example, see <a href="https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs-records-examples.html#flow-log-example-tcp-flag">TCP flag sequence</a>.</p>

    <p> For general information about TCP flags (such as the meaning of flags like FIN, SYN, and ACK), see <a href="https://en.wikipedia.org/wiki/Transmission_Control_Protocol#TCP_segment_structure">TCP segment structure on Wikipedia</a>.</p>

<p>Parquet data type: INT_32</p></td>
      <td>3</td>
    </tr>
    <tr>
      <td>type</td>
      <td><p>The type of traffic. The possible values are: IPv4 | IPv6 | EFA. For more information, see <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/efa.html">Elastic Fabric Adapter</a>.</p>

<p>Parquet data type: STRING</p></td>
      <td>3</td>
    </tr>
    <tr>
      <td>pkt-srcaddr</td>
      <td><p>The packet-level (original) source IP address of the traffic. Use this field with the srcaddr field to distinguish between the IP address of an intermediate layer through which traffic flows, and the original source IP address of the traffic. For example, when traffic flows through <a href="https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs-records-examples.html#flow-log-example-nat">a network interface for a NAT gateway</a>, or where the IP address of a pod in Amazon EKS is different from the IP address of the network interface of the instance node on which the pod is running (for communication within a VPC).</p>

<p>Parquet data type: STRING</p></td>
      <td>3</td>
    </tr>
    <tr>
      <td>region</td>
      <td><p>The Region that contains the network interface for which traffic is recorded.</p>

<p>Parquet data type: STRING</p></td>
      <td>4</td>
    </tr>
    <tr>
      <td>az-id</td>
      <td><p>The ID of the Availability Zone that contains the network interface for which traffic is recorded. If the traffic is from a sublocation, the record displays a '-' symbol for this field.</p>

<p>Parquet data type: STRING</p></td>
      <td>4</td>
    </tr>
    <tr>
      <td>sublocation-type</td>
      <td><p>The type of sublocation that's returned in the sublocation-id field. The possible values are: wavelength | outpost | localzone. If the traffic is not from a sublocation, the record displays a '-' symbol for this field.</p>

<p>Parquet data type: STRING</p></td>
      <td>4</td>
    </tr>
    <tr>
      <td>sublocation-id</td>
      <td><p>The ID of the sublocation that contains the network interface for which traffic is recorded. If the traffic is not from a sublocation, the record displays a '-' symbol for this field.</p>

<p>Parquet data type: STRING</p></td>
      <td>4</td>
    </tr>
    <tr>
      <td>pkt-src-aws-service</td>
      <td><p>The name of the subset of IP address ranges for the pkt-srcaddr field, if the source IP address is for an AWS service.</p> 
      
      <p>The possible values are:</p> 
      <p>AMAZON | AMAZON_APPFLOW | AMAZON_CONNECT | API_GATEWAY | CHIME_MEETINGS | CHIME_VOICECONNECTOR | CLOUD9 | CLOUDFRONT | CODEBUILD | DYNAMODB | EBS | EC2 | EC2_INSTANCE_CONNECT | GLOBALACCELERATOR | KINESIS_VIDEO_STREAMS | ROUTE53 | ROUTE53_HEALTHCHECKS | ROUTE53_HEALTHCHECKS_PUBLISHING | ROUTE53_RESOLVER | S3 | WORKSPACES_GATEWAYS.</p>

<p>Parquet data type: STRING</p></td>
      <td>5</td>
    </tr>
    <tr>
      <td>pkt-dst-aws-service</td>
      <td><p>The name of the subset of IP address ranges for the pkt-dstaddr field, if the destination IP address is for an AWS service. For a list of possible values, see the pkt-src-aws-service field.</p>

<p>Parquet data type: STRING</p></td>
      <td>5</td>
    </tr>
    <tr>
      <td>flow-direction</td>
      <td><p>The direction of the flow with respect to the interface where traffic is captured. The possible values are: ingress | egress.</p>

<p>Parquet data type: STRING</p></td>
      <td>5</td>
    </tr>
    <tr>
      <td>traffic-path</td>
      <td><p>The path that egress traffic takes to the destination. To determine whether the traffic is egress traffic, check the flow-direction field. The possible values are as follows. If none of the values apply, the field is set to -.</p>	
<ol>
  <li>Through another resource in the same VPC</li>
  <li>Through an internet gateway or a gateway VPC endpoint</li>
  <li>Through a virtual private gateway</li>
  <li>Through an intra-region VPC peering connection</li>
  <li>Through an inter-region VPC peering connection</li>
  <li>Through a local gateway</li>
  <li>Through a gateway VPC endpoint (Nitro-based instances only)</li>
  <li>Through an internet gateway (Nitro-based instances only)</li>
</ol>

<p>Parquet data type: INT_32</p>
  </td>
      <td>5</td>

</table>


</details>

</blockquote>



<a id="datatypes"></a>

<blockquote>

<h3>CloudWatch Logs Data Types</h3>

<p>The Amazon CloudWatch Logs API contains several data types that various actions use. This section describes each data type in detail.</p>

<p>Read more about the Log types and discoverable fields supported by <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_AnalyzeLogData-discoverable-fields.html">CloudWatch Insights</a>.</p>

<br>

<details><summary><em>Click here to see detailed descriptions for each data type supported by CloudWatch Logs.</em></summary>

<br>

<details>
  <summary><b>Destination</b> </summary>

<ul>
  <li>Represents a cross-account destination that receives subscription log events.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>accessPolicy</code> </dt>
  <dd>An IAM policy document that governs which AWS accounts can create subscription filters against this destination.</dd>
  <dt><code>arn</code></dt>
  <dd>The ARN of this destination.</dd>
  <dt><code>creationTime</code></dt>
  <dd>The creation time of the destination, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code></dd>
  <dt><code>destinationName</code></dt>
  <dd>The name of the destination.</dd>
  <dt><code>roleArn</code></dt>
  <dd>A role for impersonation, used when delivering log events to the target.</dd>
  <dt><code>targetArn</code></dt>
  <dd>The Amazon Resource Name (ARN) of the physical target where the log events are delivered (for example, a Kinesis stream).</dd>
</dl>

<br>

</details>

<details>
  <summary><b>ExportTask</b></summary>

<ul>
 <li>Represents an export task.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>destination</code></dt>
  <dd>The name of the S3 bucket to which the log data was exported.</dd>
  <dt><code>destinationPrefix</code></dt>
  <dd>The prefix that was used as the start of Amazon S3 key for every object exported.</dd>
  <dt><code>executionInfo</code></dt>
  <dd>Execution information about the export task.</dd>
  <dt><code>from</code></dt>
  <dd>The start time, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC</code>. Events with a timestamp before this time are not exported.</dd>
  <dt><code>logGroupName</code></dt>
  <dd>The name of the log group from which logs data was exported.</dd>
  <dt><code>status</code></dt>
  <dd>The status of the export task.</dd>
  <dt><code>taskId</code></dt>
  <dd>The ID of the export task.</dd>
  <dt><code>taskName</code></dt>
  <dd>The name of the export task.</dd>
  <dt><code>to</code></dt>
  <dd>The end time, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC</code>. Events with a timestamp later than this time are not exported.
  </dd>
</dl>

<br>

</details>


<details>
<summary><b>ExportTaskExecutionInfo </b></summary>

<ul>
 <li>Represents the status of an export task.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>completionTime</code></dt>
  <dd>The completion time of the export task, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code></dd>
  <dt><code>creationTime</code></dt>
  <dd>The creation time of the export task, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code></dd>
</dl>

<br>

</details>


<details>
<summary><b>ExportTaskStatus</b></summary>

<ul>
 <li>Represents the status of an export task.</li>
</ul>


<dl>
  <dt><code>code</code></dt>
  <dd>The status code of the export task.</dd>
  <dt><code>message</code></dt>
  <dd>The status message related to the status code.</dd>
</dl>

<br>

</details>


<details>
<summary><b>FilteredLogEvent</b></summary>

<ul>
 <li>Represents a matched event.</li>
</ul>


<p>Contents:</p>

<dl>
  <dt><code>eventId </code></dt>
  <dd>The ID of the event.</dd>
  <dt><code>ingestionTime</code></dt>
  <dd>The time the event was ingested, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code></dd>
  <dt><code>logStreamName </code></dt>
  <dd>The name of the log stream to which this event belongs.
</dd>
  <dt><code>message</code></dt>
  <dd>The data contained in the log event.</dd>
  <dt><code>timestamp</code></dt>
  <dd>The time the event occurred, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code></dd>
</dl>

<br>

</details>

<details>
<summary><b>InputLogEvent</b></summary>

<ul>
 <li>Represents a log event, which is a record of activity that was recorded by the application or resource being monitored.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code> message </code></dt>
  <dd>The raw event message.</dd>
  <dt><code> timestamp </code></dt>
  <dd>The time the event occurred, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code>
</dd>
  </dl>

<br>

</details>


<details>
<summary><b>LogGroup</b></summary>

<ul>
 <li>Represents a log group.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>arn</code></dt>
  <dd>The Amazon Resource Name (ARN) of the log group.</dd>
  <dt><code>creationTime</code></dt>
  <dd>The creation time of the log group, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code>
  </dd>
  <dt><code>dataProtectionStatus</code></dt>
  <dd>Displays whether this log group has a protection policy, or whether it had one in the past. For more information, see PutDataProtectionPolicy.
  </dd>
  <dt><code>kmsKeyId</code></dt>
  <dd>The Amazon Resource Name (ARN) of the AWS KMS key to use when encrypting log data.
  </dd>
  <dt><code>logGroupName</code></dt>
  <dd>The name of the log group.
  </dd>
  <dt><code>metricFilterCount</code></dt>
  <dd>The number of metric filters.
  </dd>
  <dt><code>retentionInDays</code></dt>
  <dd><p>The number of days to retain the log events in the specified log group. Possible values are: 1, 3, 5, 7, 14, 30, 60, 90, 120, 150, 180, 365, 400, 545, 731, 1827, 2192, 2557, 2922, 3288, and 3653.  </p>

<p>To set a log group so that its log events do not expire, use <a href="https://docs.aws.amazon.com/AmazonCloudWatchLogs/latest/APIReference/API_PutDataProtectionPolicy.html">DeleteRetentionPolicy.</a></p></dd>
  <dt><code>storedBytes</code></dt>
  <dd>The number of bytes stored.</dd>
</dl>

<br>

</details>


<details>
<summary><b>LogGroupField </b></summary>

<ul>
 <li>The fields contained in log events found by a GetLogGroupFields operation, along with the percentage of queried log events in which each field appears.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code> name </code></dt>
  <dd>The name of a log field.
</dd>
  <dt><code>percent</code></dt>
  <dd>The percentage of log events queried that contained the field.</dd>
</dl>

<br>

</details>

<details>
<summary><b>LogStream</b></summary>

<ul>
 <li>Represents a log stream, which is a sequence of log events from a single emitter of logs.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>arn</code></dt>
  <dd>The Amazon Resource Name (ARN) of the log stream.
</dd>
  <dt><code>creationTime</code></dt>
  <dd>The creation time of the stream, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code>
</dd>
  <dt><code>firstEventTimestamp</code></dt>
  <dd>The time of the first event, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code>
</dd>
  <dt><code>lastEventTimestamp</code></dt>
  <dd>The time of the most recent log event in the log stream in CloudWatch Logs. This number is expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code> The lastEventTime value updates on an eventual consistency basis. It typically updates in less than an hour from ingestion, but in rare situations might take longer.
</dd>
  <dt><code>lastIngestionTime</code></dt>
  <dd>The ingestion time, expressed as the number of milliseconds after Jan 1, 1970 00:00:00 UTC The lastIngestionTime value updates on an eventual consistency basis. It typically updates in less than an hour after ingestion, but in rare situations might take longer.
</dd>
  <dt><code>logStreamName</code></dt>
  <dd>The name of the log stream.
</dd>
  <dt><code>storedBytes</code></dt>
  <dd><p><i>This member has been deprecated.</i></p>

<p>The number of bytes stored.</p>

<p><b>Important:</b> As of June 17, 2019, this parameter is no longer supported for log streams, and is always reported as zero. This change applies only to log streams. The <code>storedBytes</code> parameter for log groups is not affected.</p>
</dd>
  <dt><code> uploadSequenceToken </code></dt>
  <dd><p>The sequence token.</p>
<p><b>Important:</b> The sequence token is now ignored in PutLogEvents actions. PutLogEvents actions are always accepted regardless of receiving an invalid sequence token. You don't need to obtain uploadSequenceToken to use a PutLogEvents action.</p>
</dd>
</dl>

<br>

</details>


<details>
<summary><b>MetricFilter</b></summary>

<ul>
 <li>Metric filters express how CloudWatch Logs would extract metric observations from ingested log events and transform them into metric data in a CloudWatch metric.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>creationTime</code></dt>
  <dd>The creation time of the metric filter, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code>
</dd>
  <dt><code>filterName</code></dt>
  <dd>The name of the metric filter.
</dd>
  <dt><code>filterPattern</code></dt>
  <dd>A symbolic description of how CloudWatch Logs should interpret the data in each log event. For example, a log event can contain timestamps, IP addresses, strings, and so on. You use the filter pattern to specify what to look for in the log event message.
</dd>
  <dt><code>logGroupName</code></dt>
  <dd>The name of the log group.
</dd>
  <dt><code>metricTransformations</code></dt>
  <dd>The metric transformations.
</dd>
</dl>

<br>

</details>



<details>
<summary><b>MetricFilterMatchRecord</b></summary>

<ul>
 <li>Represents a matched event.</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>eventMessage</code></dt>
  <dd>The raw event data.</dd>
  <dt><code>eventNumber</code></dt>
  <dd>The event number.
</dd>
  <dt><code>extractedValues
</code></dt>
  <dd>The values extracted from the event data by the filter.
</dd>
</dl>

<br>

</details>


<details>
<summary><b>MetricTransformation</b></summary>

<ul>
 <li>Indicates how to transform ingested log events to metric data in a CloudWatch metric.</li>
</ul>


<p>Contents:</p>

<dl>
  <dt><code>defaultValue</code></dt>
  <dd>(Optional) The value to emit when a filter pattern does not match a log event. This value can be null.
  </dd>
  <dt><code>dimensions</code></dt>
  <dd><p>The fields to use as dimensions for the metric. One metric filter can include as many as three dimensions.</p>

<p><b>Important: </b>Metrics extracted from log events are charged as custom metrics. To prevent unexpected high charges, do not specify high-cardinality fields such as IPAddress or requestID as dimensions. Each different value found for a dimension is treated as a separate metric and accrues charges as a separate custom metric.</p>

<p>CloudWatch Logs disables a metric filter if it generates 1000 different name/value pairs for your specified dimensions within a certain amount of time. This helps to prevent accidental high charges.</p>

<p>You can also set up a billing alarm to alert you if your charges are higher than expected. For more information, see <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html">Creating a Billing Alarm to Monitor Your Estimated AWS Charges.</a></p></dd>
  <dt><code>metricName</code></dt>
  <dd>The name of the CloudWatch metric.
  </dd>
  <dt><code>metricNamespace</code></dt>
  <dd><p>A custom namespace to contain your metric in CloudWatch. Use namespaces to group together metrics that are similar. For more information, see <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Namespace">Namespaces.</a></p>
  </dd>
  <dt><code>metricValue</code></dt>
  <dd>The value to publish to the CloudWatch metric when a filter pattern matches a log event.
  </dd>
  <dt><code>unit</code></dt>
  <dd>The unit to assign to the metric. If you omit this, the unit is set as <code>None</code>.
</dd>
</dl>

<br>

</details>


<details>
<summary><b>OutputLogEvent</b></summary>

<ul>
 <li>Represents a log event</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>ingestionTime</code></dt>
  <dd>The time the event was ingested, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code>
  </dd>
  <dt><code>message</code></dt>
  <dd>The data contained in the log event.
  </dd>
  <dt><code>timestamp</code></dt>
  <dd>The time the event occurred, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code>
  </dd>
</dl>

<br>

</details>




<details>
<summary><b>QueryCompileError</b></summary>

<ul>
 <li>Reserved</li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>location</code></dt>
  <dd>Reserved.
</dd>
  <dt><code>message</code></dt>
  <dd>Reserved.
</dd>
</dl>

<br>

</details>




<details>
<summary><b>QueryCompileErrorLocation</b></summary>

<ul>
 <li> Reserved </li>
</ul>

<p>Contents:</p>

<dl>
  <dt><code>endCharOffset</code></dt>
  <dd>Reserved.
</dd>
  <dt><code>startCharOffset</code></dt>
  <dd>Reserved.
</dd>
</dl>

<br>

</details>



<details>
<summary><b>QueryDefinition</b></summary>

<ul>
 <li>This structure contains details about a saved CloudWatch Logs Insights query definition.
 </li>
</ul>

<p><b>Contents:</b></p>

<dl>
  <dt><code>lastModified</code></dt>
  <dd>The date that the query definition was most recently modified.
</dd>
  <dt><code>logGroupNames</code></dt>
  <dd>If this query definition contains a list of log groups that it is limited to, that list appears here.
</dd>
  <dt><code>name</code></dt>
  <dd>The name of the query definition.
</dd>
  <dt><code>queryDefinitionId</code></dt>
  <dd>The unique ID of the query definition.
</dd>
  <dt><code>queryString</code></dt>
  <dd>The query string to use for this definition. For more information, see <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_QuerySyntax.html">CloudWatch Logs Insights Query Syntax.</a></dd>
</dl>

<br>

</details>


<details>
<summary><b>QueryInfo</b></summary>

<ul>
 <li>Information about one CloudWatch Logs Insights query that matches the request in a DescribeQueries operation.
 </li>
</ul>

<p><b>Contents:</b></p>

<dl>
  <dt><code>createTime</code></dt>
  <dd>The date and time that this query was created.
</dd>
  <dt><code>logGroupName</code></dt>
  <dd>The name of the log group scanned by this query.
</dd>
  <dt><code>queryId</code></dt>
  <dd>The unique ID number of this query.
</dd>
  <dt><code>queryString</code></dt>
  <dd>The query string used in this query.
</dd>
  <dt><code>status</code></dt>
  <dd>The status of this query. Possible values are Cancelled, Complete, Failed, Running, Scheduled, and Unknown.
</dd>
</dl>

<br>

</details>


<details>
<summary><b>QueryStatistics</b></summary>

<ul>
 <li>Contains the number of log events scanned by the query, the number of log events that matched the query criteria, and the total number of bytes in the log events that were scanned.</li>
</ul>

<p><b>Contents:</b></p>

recordsScanned
The total number of log events scanned during the query.

<dl>
  <dt><code>bytesScanned</code></dt>
  <dd>The total number of bytes in the log events scanned during the query.
</dd>
  <dt><code>recordsMatched
</code></dt>
  <dd>The number of log events that matched the query string.
</dd>
  <dt><code>recordsScanned
</code></dt>
  <dd>The total number of log events scanned during the query.
</dd>
</dl>

<br>

</details>


<details>
<summary><b>RejectedLogEventsInfo</b></summary>

<ul>
  <li>Represents the rejected events.</li>
</ul>

<p><b>Contents:</b></p>

<dl>
  <dt><code>expiredLogEventEndIndex</code></dt>
  <dd>The expired log events.</dd>
  <dt><code>tooNewLogEventStartIndex</code></dt>
  <dd>The log events that are too new.</dd>
  <dt><code>tooOldLogEventEndIndex</code></dt>
  <dd>The log events that are dated too far in the past.</dd>
</dl>

<br>

</details>




<details>
<summary><b>ResourcePolicy</b></summary>

<ul>
 <li>A policy enabling one or more entities to put logs to a log group in this account.</li>
</ul>

<p><b>Contents:</b></p>

<dl>
  <dt><code>lastUpdatedTime</code></dt>
  <dd>Timestamp showing when this policy was last updated, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code></dd>
  <dt><code>policyDocument</code></dt>
  <dd>The details of the policy.</dd>
  <dt><code>policyName</code></dt>
  <dd>The name of the resource policy.</dd>
</dl>

<br>

</details>



<details>
<summary><b>ResultField</b></summary>

<ul>
  <li><p>Contains one field from one log event returned by a CloudWatch Logs Insights query, along with the value of that field.</p>
  <p>For more information about the fields that are generated by CloudWatch logs, see <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_AnalyzeLogData-discoverable-fields.html">Supported Logs and Discovered Fields.</a></p></li>
</ul>

<p><b>Contents:</b></p>

<dl>
  <dt><code>field</code></dt>
  <dd>The log event field.</dd>
  <dt><code>value</code></dt>
  <dd>The value of this field.</dd>
</dl>

<br>

</details>




<details>
<summary><b>SearchedLogStream</b></summary>

<ul>
 <li>Represents the search status of a log stream.</li>
</ul>

<p><b>Contents:</b></p>

<dl>
  <dt><code>logStreamName</code></dt>
  <dd>The name of the log stream.</dd>
  <dt><code>searchedCompletely</code></dt>
  <dd>Indicates whether all the events in this log stream were searched.</dd>
</dl>

<br>

</details>




<details>
<summary><b>SubscriptionFilter</b></summary>

<ul>
 <li>Represents a subscription filter.</li>
</ul>

<p><b>Contents:</b></p>

<dl>
  <dt><code>reationTime</code></dt>
  <dd>The creation time of the subscription filter, expressed as the number of milliseconds after <code>Jan 1, 1970 00:00:00 UTC.</code></dd>
  <dt><code>destinationArn</code></dt>
  <dd>The Amazon Resource Name (ARN) of the destination.</dd>
  <dt><code>distribution</code></dt>
  <dd>The method used to distribute log data to the destination, which can be either random or grouped by log stream.</dd>
  <dt><code>filterName</code></dt>
  <dd>The name of the subscription filter.</dd>
  <dt><code>filterPattern</code></dt>
  <dd>A symbolic description of how CloudWatch Logs should interpret the data in each log event. For example, a log event can contain timestamps, IP addresses, strings, and so on. You use the filter pattern to specify what to look for in the log event message.</dd>
  <dt><code>logGroupName</code></dt>
  <dd>The name of the log group.</dd>
  <dt><code>roleArn</code></dt>
  <dd>The ARN of an IAM role that grants CloudWatch Logs permissions to call the Amazon Kinesis PutRecord operation on the destination stream.</dd>
</dl>

<br>

</details>

</details>

</blockquote>



<a id="code"></a>

<hr class="solid">

<h2>Code Samples</h2>

<a id="awscloud"></a>

<blockquote>


<h3>AWS VPC Flow Logs</h3>

<details><summary><b>Flow Logs</b></summary>

<pre>

    spark.table("awscloudwatch.vpc_1w")
    .groupBy("srcaddr", "dstaddr","instanceId","accountId")
    .agg(
    min($"ts").as("Start"),
    max($"ts").as("End"),
    sum($"bytes").as("bytesTransferred"),
    collect_set($"dstport").as("target_ports"),
    collect_set($"tcpFlags") as "FlagsinDec",
    collect_set($"interfaceId").as("eni"),
    collect_set($"vpcId") as ("VPCId"),
    collect_set($"subnetId") as ("subnetIds"),
    count("*").as("count")
    )
    .withColumn("stringDstPorts", concat_ws(", ", $"target_ports"))
    .withColumn("stringAcctId", concat_ws(", ", $"acctId"))
    .withColumn("stringEni", concat_ws(", ", $"eni"))
    .withColumn("MB",$"bytesTransferred"/1024/1024)
    .drop("target_ports")
    .drop("acctId")
    .drop("eni")

</pre>


</details>

</blockquote>




<blockquote>

<h3>AWS CloudWatch Logs</h3>


<a id="awsvpc"></a>

Click below for a list of code examples on how to use CloudWatch Logs with an AWS software development kit (SDK):

<a id="actionscode"></a>

<details><summary><b>Actions</b></summary>

 
  <ul>

<li><details><summary><b>Associate a key with a log group</b></summary>
    
The following code example shows how to associate an AWS KMS key with an existing CloudWatch Logs log group. 

<pre style="white-space: pre-wrap; word-break: break-all;">

using System;
using System.Threading.Tasks;
using Amazon.CloudWatchLogs;
using Amazon.CloudWatchLogs.Model;

  
/// Shows how to associate an AWS Key Management Service (AWS KMS) key with
/// an Amazon CloudWatch Logs log group. The example was created using the
/// AWS SDK for .NET version 3.7 and .NET Core 5.0.

public class AssociateKmsKey
{
    public static async Task Main()
    {
        // This client object will be associated with the same AWS Region
        // as the default user on this system. If you need to use a
        // different AWS Region, pass it as a parameter to the client
        // constructor.
        var client = new AmazonCloudWatchLogsClient();

        string kmsKeyId = "arn:aws:kms:us-west-2:<account-number>:key/7c9eccc2-38cb-4c4f-9db3-766ee8dd3ad4";
        string groupName = "cloudwatchlogs-example-loggroup";

        var request = new AssociateKmsKeyRequest
        {
                KmsKeyId = kmsKeyId,
                LogGroupName = groupName,
        };

        var response = await client.AssociateKmsKeyAsync(request);

        if (response.HttpStatusCode == System.Net.HttpStatusCode.OK)
        {
                Console.WriteLine($"Successfully associated KMS key ID: {kmsKeyId} with log group: {groupName}.");
        }
            
        {
            Console.WriteLine("Could not make the association between: {kmsKeyId} and {groupName}.");
        }
    }

}
  
</pre>



<ul>
  <li>For API details, see <a href="https://docs.aws.amazon.com/goto/DotNetSDKV3/logs-2014-03-28/AssociateKmsKey">AssociateKmsKey</a> in AWS SDK for .NET API Reference.</li>
</ul>

<br>

</details>

    
</li>
    <li><details><summary><b>Cancel an export task</b></summary>
   
The following code example shows how to cancel an existing CloudWatch Logs export task.

<pre style="white-space: pre-wrap;">

    using System;
    using System.Threading.Tasks;
    using Amazon.CloudWatchLogs;
    using Amazon.CloudWatchLogs.Model;

    /// <summary>
    /// Shows how to cancel an Amazon CloudWatch Logs export task. The example
    /// uses the AWS SDK for .NET version 3.7 and .NET Core 5.0.
    /// </summary>
    public class CancelExportTask
    {
        public static async Task Main()
        {
            // This client object will be associated with the same AWS Region
            // as the default user on this system. If you need to use a
            // different AWS Region, pass it as a parameter to the client
            // constructor.
            var client = new AmazonCloudWatchLogsClient();
            string taskId = "exampleTaskId";

            var request = new CancelExportTaskRequest
            {
                TaskId = taskId,
            };

            var response = await client.CancelExportTaskAsync(request);

            if (response.HttpStatusCode == System.Net.HttpStatusCode.OK)
            {
                Console.WriteLine($"{taskId} successfully canceled.");
            }
            else
            {
                Console.WriteLine($"{taskId} could not be canceled.");
            }
        }
    }

</pre>

<ul>  
  <li>For API details, see <a href="https://docs.aws.amazon.com/goto/DotNetSDKV3/logs-2014-03-28/CancelExportTask">CancelExportTask</a> in AWS SDK for .NET API Reference.</li>
</ul>


<br>

</details>

</li>



  <li><details><summary><b>Create a log group</b></summary>
    
The following code examples show how to create a new CloudWatch Logs log group.

<pre style="white-space: break-spaces;">

    using System;
    using System.Threading.Tasks;
    using Amazon.CloudWatchLogs;
    using Amazon.CloudWatchLogs.Model;

    /// <summary>
    /// Shows how to create an Amazon CloudWatch Logs log group. The example
    /// was created using the AWS SDK for .NET version 3.7 and .NET Core 5.0.
    /// </summary>
    public class CreateLogGroup
    {
        public static async Task Main()
        {
            // This client object will be associated with the same AWS Region
            // as the default user on this system. If you need to use a
            // different AWS Region, pass it as a parameter to the client
            // constructor.
            var client = new AmazonCloudWatchLogsClient();

            string logGroupName = "cloudwatchlogs-example-loggroup";

            var request = new CreateLogGroupRequest
            {
                LogGroupName = logGroupName,
            };

            var response = await client.CreateLogGroupAsync(request);

            if (response.HttpStatusCode == System.Net.HttpStatusCode.OK)
            {
                Console.WriteLine($"Successfully create log group with ID: {logGroupName}.");
            }
            else
            {
                Console.WriteLine("Could not create log group.");
            }
        }
    }

</pre>

<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/goto/DotNetSDKV3/logs-2014-03-28/CreateLogGroup">CreateLogGroup</a> in AWS SDK for .NET API Reference.</li>
</ul>

<br>

</details>
    
  </li>
    
    
<li><details><summary><b>Create a new log stream</b></summary>

The following code example shows how to create a new CloudWatch Logs log stream.

<pre style="white-space: break-spaces;">

    using System;
    using System.Threading.Tasks;
    using Amazon.CloudWatchLogs;
    using Amazon.CloudWatchLogs.Model;

    /// <summary>
    /// Shows how to create an Amazon CloudWatch Logs stream for a CloudWatch
    /// log group. The example was created using the AWS SDK for .NET version
    /// 3.7 and .NET Core 5.0.
    /// </summary>
    public class CreateLogStream
    {
        public static async Task Main()
        {
            // This client object will be associated with the same AWS Region
            // as the default user on this system. If you need to use a
            // different AWS Region, pass it as a parameter to the client
            // constructor.
            var client = new AmazonCloudWatchLogsClient();
            string logGroupName = "cloudwatchlogs-example-loggroup";
            string logStreamName = "cloudwatchlogs-example-logstream";

            var request = new CreateLogStreamRequest
            {
                LogGroupName = logGroupName,
                LogStreamName = logStreamName,
            };

            var response = await client.CreateLogStreamAsync(request);

            if (response.HttpStatusCode == System.Net.HttpStatusCode.OK)
            {
                Console.WriteLine($"{logStreamName} successfully created for {logGroupName}.");
            }
            else
            {
                Console.WriteLine("Could not create stream.");
            }
        }
    }

</pre>

<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/goto/DotNetSDKV3/logs-2014-03-28/CreateLogStream">CreateLogStream</a> in AWS SDK for .NET API Reference.</li>
</ul>

<br>

</details>


</li>
    

    
<li><details><summary><b>Create a subscription filter</summary></b>

The following code examples show how to create an Amazon CloudWatch Logs subscription filter.

<pre style="white-space: break-spaces;">

    import { PutSubscriptionFilterCommand } from "@aws-sdk/client-cloudwatch-logs";
    import { client } from "../libs/client.js";

    const run = async () => {
    const command = new PutSubscriptionFilterCommand({
    // An ARN of a same-account Kinesis stream, Kinesis Firehose
    // delivery stream, or Lambda function.
    // https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SubscriptionFilters.html
    destinationArn: process.env.CLOUDWATCH_LOGS_DESTINATION_ARN,

    // A name for the filter.
    filterName: process.env.CLOUDWATCH_LOGS_FILTER_NAME,

    // A filter pattern for subscribing to a filtered stream of log events.
    // https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/FilterAndPatternSyntax.html
    filterPattern: process.env.CLOUDWATCH_LOGS_FILTER_PATTERN,

    // The name of the log group. Messages in this group matching the filter pattern
    // will be sent to the destination ARN.
    logGroupName: process.env.CLOUDWATCH_LOGS_LOG_GROUP,
    });

    try {
    return await client.send(command);
    } catch (err) {
    console.error(err);
     }
     };

     export default run();

</pre>
    

<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-cloudwatch-logs/classes/putsubscriptionfiltercommand.html">PutSubscriptionFilter</a> in AWS SDK for JavaScript API Reference.</li>
</ul>

<br>

</details>

</li>




<li><details><summary><b>Create an export task</b></summary>

The following code example shows how to create a new CloudWatch Logs export task.

<pre style="white-space: break-spaces;">

            "eventVersion": "1.03",
        "userIdentity": {
            "type": "IAMUser",
            "principalId": "EX_PRINCIPAL_ID",
            "arn": "arn:aws:iam::123456789012:user/someuser",
            "accountId": "123456789012",
            "accessKeyId": "AKIAIOSFODNN7EXAMPLE",
            "userName": "someuser"
        },
        "eventTime": "2016-02-08T06:35:14Z",
        "eventSource": "logs.amazonaws.com",
        "eventName": "CreateExportTask",
        "awsRegion": "us-east-1",
        "sourceIPAddress": "127.0.0.1",
        "userAgent": "aws-sdk-ruby2/2.0.0.rc4 ruby/1.9.3 x86_64-linux Seahorse/0.1.0",
        "requestParameters": {
            "destination": "yourdestination",
            "logGroupName": "yourloggroup",
            "to": 123456789012,
            "from": 0,
            "taskName": "yourtask"
        },
        "responseElements": {
            "taskId": "15e5e534-9548-44ab-a221-64d9d2b27b9b"
        },
        "requestID": "1cd74c1c-ce2e-12e6-99a9-8dbb26bd06c9",
        "eventID": "fd072859-bd7c-4865-9e76-8e364e89307c",
        "eventType": "AwsApiCall",
        "apiVersion": "20140328",
        "recipientAccountId": "123456789012"

</pre>

<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/goto/DotNetSDKV3/logs-2014-03-28/CreateExportTask">CreateExportTask</a> in AWS SDK for JavaScript API Reference.</li>
</ul>
 
<br>

</details>

</li>



<li><details><summary><b>Delete a log group</b></summary>
 
The following code examples show how to delete an existing CloudWatch Logs log group.

<pre style="white-space: break-spaces;">
    
    import { DeleteLogGroupCommand } from "@aws-sdk/client-cloudwatch-logs";
    import { client } from "../libs/client.js";

    const run = async () => {
    const command = new DeleteLogGroupCommand({
    // The name of the log group.
    logGroupName: process.env.CLOUDWATCH_LOGS_LOG_GROUP,
    });

    try {
    return await client.send(command);
    } catch (err) {
    console.error(err);
    }
    };

    export default run();

</pre>

<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-cloudwatch-logs/classes/deleteloggroupcommand.html">DeleteLogGroup</a> in AWS SDK for JavaScript API Reference.</li>
</ul>
 
<br>

</detials>
   
</li>



<li><details><summary><b>Delete a subscription filter</b></summary>

The following code examples show how to delete an Amazon CloudWatch Logs subscription filter.

<pre style="white-space: break-spaces;">

    import { DeleteSubscriptionFilterCommand } from "@aws-sdk/client-cloudwatch-logs";
    import { client } from "../libs/client.js";

    const run = async () => {
    const command = new DeleteSubscriptionFilterCommand({
    // The name of the filter.
    filterName: process.env.CLOUDWATCH_LOGS_FILTER_NAME,
    // The name of the log group.
    logGroupName: process.env.CLOUDWATCH_LOGS_LOG_GROUP,
    });

    try {
    return await client.send(command);
    } catch (err) {
    console.error(err);
    }
    };

    export default run();

</pre>

<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-cloudwatch-logs/classes/deletesubscriptionfiltercommand.html">DeleteSubscriptionFilter</a> in AWS SDK for JavaScript API Reference.</li>
</ul>
 
<br>

</detials>


</li>




 <li><details><summary><b>Describe existing subscription filters</b></summary>
  
 The following code examples show how to describe Amazon CloudWatch Logs existing subscription filters.

<pre style="white-space: break-spaces;">

    import { DescribeSubscriptionFiltersCommand } from "@aws-sdk/client-cloudwatch-logs";
    import { client } from "../libs/client.js";

    const run = async () => {
    // This will return a list of all subscription filters in your account
    // matching the log group name.
    const command = new DescribeSubscriptionFiltersCommand({
    logGroupName: process.env.CLOUDWATCH_LOGS_LOG_GROUP,
    limit: 1,
    });

    try {
    return await client.send(command);
    } catch (err) {
    console.error(err);
    }
    ;

    export default run();

</pre>
      
<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-cloudwatch-logs/classes/describesubscriptionfilterscommand.html">DescribeSubscriptionFilters</a> in AWS SDK for JavaScript API Reference.</li>
</ul>
 
<br>

</detials>
  
  </li>



  <li><details><summary><b>Describe export tasks</b></summary>
  
  The following code example shows how to describe CloudWatch Logs export tasks.

<pre style="white-space: break-spaces;">

    using System;
    using System.Threading.Tasks;
    using Amazon.CloudWatchLogs;
    using Amazon.CloudWatchLogs.Model;

    /// <summary>
    /// Shows how to retrieve a list of information about Amazon CloudWatch
    /// Logs export tasks. The example was created using the AWS SDK for .NET
    /// version 3.7 and .NET Core 5.0.
    /// </summary>
    public class DescribeExportTasks
    {
        public static async Task Main()
        {
            // This client object will be associated with the same AWS Region
            // as the default user on this system. If you need to use a
            // different AWS Region, pass it as a parameter to the client
            // constructor.
            var client = new AmazonCloudWatchLogsClient();

            var request = new DescribeExportTasksRequest
            {
                Limit = 5,
            };

            var response = new DescribeExportTasksResponse();

            do
            {
                response = await client.DescribeExportTasksAsync(request);
                response.ExportTasks.ForEach(t =>
                {
                    Console.WriteLine($"{t.TaskName} with ID: {t.TaskId} has status: {t.Status}");
                });
            }
            while (response.NextToken is not null);
        }
    }

</pre>

<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/goto/DotNetSDKV3/logs-2014-03-28/DescribeExportTasks">DescribeExportTasks</a> in AWS SDK for .NET API Reference.</li>
</ul>
 
<br>

</detials>

 </li>


   
<li><details><summary><b>Describe log groups</b></summary>
  
The following code examples show how to describe CloudWatch Logs log groups.

<pre style="white-space: pre-line;">

using System;
using System.Threading.Tasks; 
using Amazon.CloudWatchLogs;
using Amazon.CloudWatchLogs.Model;

/// <summary>
/// Retrieves information about existing Amazon CloudWatch Logs log groups
/// and displays the information on the console. The example was created 
/// using the AWS SDK for .NET version 3.7 and .NET Core 5.0  
/// </summary>
public class DescribeLogGroups
{
    public static async Task Main()
    {
        // Creates a CloudWatch Logs client using the default
        // user. If you need to work with resources in another
        // AWS Region than the one defined for the default user,
        // pass the AWS Region as a parameter to the client constructor.
        var client = new AmazonCloudWatchLogsClient();

        var request = new DescribeLogGroupsRequest
        {
           Limit = 5,
        };

        var response = await client.DescribeLogGroupsAsync(request);

       if (response.LogGroups.Count > 0)
        {
            do
            {
                response.LogGroups.ForEach(lg =>
                {
                    Console.WriteLine($"{lg.LogGroupName} is associated with the key: {lg.KmsKeyId}.");
                    Console.WriteLine($"Created on: {lg.CreationTime.Date.Date}");
                    Console.WriteLine($"Date for this group will be stored for: {lg.RetentionInDays} days.\n");
                });
            }
            while (response.NextToken is not null);
        }
   }
}

</pre>

<ul>
  <li> For API details, see <a ref="https://docs.aws.amazon.com/goto/DotNetSDKV3/logs-2014-03-28/DescribeLogGroups">DescribeLogGroups</a> in AWS SDK for .NET API Reference.</li>
</ul>

</ul>
</details>
  
</blockquote>

<a id="limitations"></a>

<hr class="solid">

<h2>Limitations</h2>

<h3>Limitations with VPC Flow Logs</h3>

<p>you need to be aware of the following limitations:</p>

<ul>
  <li>Flow logs cannot be enabled for network interfaces that are in the EC2-Classic platform. This includes EC2-Classic instances that have been linked to a VPC through ClassicLink.</li>
  <li>Flow logs for VPCs that are peered with your VPC cannot be enabled unless the peer VPC is in your account.</li>
  <li>After a Flow log is created, you cannot change its configuration or the flow log record format. For example, different IAM roles cannot be associated with the flow log, or can fields be added or removed in the flow log record. Instead, the flow log must be deleted and a new one created in its place with the required configuration.</li>
  <li>If your network interface has multiple IPv4 addresses and traffic is sent to a secondary private IPv4 address, the flow log displays the primary private IPv4 address in the dstaddr field. To capture the original destination IP address, create a flow log with the <code>pkt-dstaddr</code> field.</li>
  <li>If traffic is sent to a network interface and the destination is not any of the network interface's IP addresses, the flow log displays the primary private IPv4 address in the dstaddr field. To capture the original destination IP address, create a flow log with the <code>pkt-dstaddr</code> field.</li>
  <li>If traffic is sent from a network interface and the source is not any of the network interface's IP addresses, the flow log displays the primary private IPv4 address in the srcaddr field. To capture the   original source IP address, create a flow log with the <code>pkt-srcaddr</code> field.</li>
  <li>If traffic is sent to or sent from a network interface, the <code>srcaddr</code> and <code>dstaddr</code> fields in the flow log always display the primary private IPv4 address, regardless of the packet source or destination. To capture the packet source or destination, create a flow log with the <code>pkt-srcaddr</code> and <code>pkt-dstaddr</code> fields.
  <li>When your network interface is attached to a Nitro-based instance, the aggregation interval is always 1 minute or less, regardless of the specified maximum aggregation interval.
Flow logs do not capture all IP traffic.</li>
</ul>

<p>The following types of traffic are not logged:</p>

<ul>
  <li>Traffic generated by instances when they contact the Amazon DNS server. If you use your own DNS server, then all traffic to that DNS server is logged.</li>
  <li>Traffic generated by a Windows instance for Amazon Windows license activation.<l/i>
  <li>Traffic to and from 169.254.169.254 for instance metadata.</li>
  <li>Traffic to and from 169.254.169.123 for the Amazon Time Sync Service.</li>
  <li>DHCP traffic.</li>
  <li>Mirrored traffic.</li>
  <li>Traffic to the reserved IP address for the default VPC router.</li>
  <li>Traffic between an endpoint network interface and a Network Load Balancer network interface.</li>
</ul>

<a id="resources"></a>

<hr class="solid">

<h2>Resources</h2>

<ul>
<li><a href="https://docs.aws.amazon.com/AmazonCloudWatchLogs/latest/APIReference/API_Types.html">Amazon CloudWatch Logs API - Data Types</a></li>
<li><a href="https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/dotnetv3/CloudWatchLogs#code-examples">CloudWatch Logs code examples for the SDK for .NET</a></li>

<br>

<a href="#backtotop"><h4>Back To Top</h4></a>

