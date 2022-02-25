# API SDK

API compatible with [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/API/Welcome.html) cloud storage service

## Endpoint

```
https://endpoint.4everland.co
```

generate API Key from [https://bucket.4everland.org/#/apikey](https://bucket.4everland.org/#/apikey)

## Supported Feature Set

Supported Bucket Calls:

| Name                   | Supported                      |
| ---------------------- | ------------------------------ |
| MakeBucketWithLocation | Yes (partial, ingore Location) |
| GetBucketInfo          | Yes (fully)                    |
| ListBuckets            | Yes (fully)                    |
| DeleteBucket           | Yes (fully)                    |

Supported Object Calls:

| Name                | Supported   |
| ------------------- | ----------- |
| ListObjects         | Yes (fully) |
| ListObjectsV2       | Yes (fully) |
| GetObjectNInfo      | Yes (fully) |
| GetObject           | Yes (fully) |
| GetObjectInfo       | Yes (fully) |
| PutObject           | Yes (fully) |
| CopyObject          | Yes (fully) |
| DeleteObject        | Yes (fully) |
| DeleteObjects       | Yes (fully) |
| GetObjectTagging    | Yes (fully) |
| PutObjectTagging    | Yes (fully) |
| DeleteObjectTagging | Yes (fully) |

Supported Multipart Calls:

| Name                    | Supported   |
| ----------------------- | ----------- |
| ListMultipartUploads    | Yes (fully) |
| NewMultipartUpload      | Yes (fully) |
| PutObjectPart           | Yes (fully) |
| CopyObjectPart          | Yes (fully) |
| ListObjectParts         | Yes (fully) |
| AbortMultipartUpload    | Yes (fully) |
| CompleteMultipartUpload | Yes (fully) |

Supported Policy Calls:

| Name               | Supported |
| ------------------ | --------- |
| SetBucketPolicy    | No        |
| GetBucketPolicy    | Yes       |
| DeleteBucketPolicy | No        |

Supported [S3 STS](https://docs.aws.amazon.com/STS/latest/APIReference/welcome.html)

## Limits of S3 API

| Item                                                                            | Specification                                 |
| ------------------------------------------------------------------------------- | --------------------------------------------- |
| Maximum number of buckets                                                       | 200                                           |
| Maximum number of objects per bucket                                            | no-limit                                      |
| Maximum object size                                                             | 5 TiB                                         |
| Minimum object size                                                             | 0 B                                           |
| Maximum object size per PUT operation                                           | 5 GiB                                         |
| Maximum number of parts per upload                                              | 1000                                          |
| Part size range                                                                 | 5 MiB to 5 GiB. Last part can be 0 B to 5 GiB |
| Maximum number of parts returned per list parts request                         | 1000                                          |
| Maximum number of objects returned per list objects request                     | 1000                                          |
| Maximum number of multipart uploads returned per list multipart uploads request | 1000                                          |
| Maximum length for bucket names                                                 | 48                                            |
| Maximum length for object names                                                 | 1024                                          |
| Maximum length for '/' separated object name segment                            | 19                                            |
