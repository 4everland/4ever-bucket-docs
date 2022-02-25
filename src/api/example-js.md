# Example for Javascript

## Installing

```
npm install @aws-sdk/client-s3
```

## Example

### init s3 client

```js
import { S3 } from "@aws-sdk/client-s3";

const { endpoint, accessKey, secretKey, sessionToken } = s3Params;
const s3 = new S3({
  endpoint,
  signatureVersion: "v4",
  credentials: {
    accessKeyId: accessKey,
    secretAccessKey: secretKey,
    sessionToken,
  },
  region: "us-west-2",
});
```

### create bucket and put object

```js
import { Upload } from "@aws-sdk/lib-storage";

const createBucketOutput = await s3.createBucket({
  Bucket: "bucketname",
});
const putObjectOutput = await s3.putObject({
  Bucket: "bucketname",
  Key: "key",
  Body: "data content",
});

// multipart upload
const params = {
  Bucket,
  Key: file.name,
  Body: file,
  ContentType: file.type,
};
try {
  const task = new Upload({
    client: s3,
    queueSize: 3, // 3 MiB
    params,
  });
  task.on("httpUploadProgress", (e) => {
    const progress = ((e.loaded / e.total) * 100) | 0;
    console.log(progress, e);
  });
  await task.done();
} catch (error) {
  if (error) {
    console.log("task", error.message);
  }
}
```

### listBucket and list objects

```js
const buckets = await s3.listBuckets();
console.log(buckets);

const objects = s3.listObjectsV2({ Bucket: "bucketname" });
console.log(objects);
```
