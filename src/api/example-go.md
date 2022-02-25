# Example for GO

## Installing

```
go get github.com/aws/aws-sdk-go-v2/aws
```

## Example

### init s3 client

```go
func main()  {
	var key, secret, token, endpoint string
	cfg, err := config.LoadDefaultConfig(context.TODO(),
		config.WithCredentialsProvider(credentials.NewStaticCredentialsProvider(key, secret, token)),
		config.WithEndpointResolverWithOptions(aws.EndpointResolverWithOptionsFunc(func(service, region string, options ...interface{}) (aws.Endpoint, error) {
			return aws.Endpoint{
				URL: endpoint,
			}, nil
		})),
	)
	if err != nil {
		log.Fatalf("unable to load SDK config, %v", err)
	}
	client := s3.NewFromConfig(cfg)
}
```

### create bucket and put object

```go
var (
    bucket = "bucketname"
    objectKey = "object/key"
)
_ , err = client.CreateBucket(context.TODO(), &s3.CreateBucketInput{
    Bucket: &bucket,
})

if err != nil {
    log.Fatalf("unable CreateBucket %s, %v", bucket, err)
}

f, err := os.Open("/tmp/dat")
info, err := f.Stat()
if err != nil {
    log.Fatalf("unable stat file,  %v",  err)
}
// putobject
_, err = client.PutObject(context.TODO(), &s3.PutObjectInput{
    Bucket: &bucket,
    Key: &objectKey,
    Body: f,
    ContentLength: info.Size(),

})
if err != nil {
    log.Fatalf("unable put object: , %v", err)
}

ff, err := os.Open("/tmp/dat")
finfo, err := ff.Stat()
if err != nil {
    log.Fatalf("unable stat file, %v", err)
}
// multipart upload
uploader := manager.NewUploader(client, func(u *manager.Uploader) {
    u.PartSize = 16 * 1024 * 1024 // 16MB per part
})

_, err = uploader.Upload(context.TODO(),&s3.PutObjectInput{
    Bucket: &bucket,
    Key: &objectKey,
    Body: ff,
    ContentLength: finfo.Size(),
})
```

### list buckets and list objects

```go
listBucketOutPut, err := client.ListBuckets(context.TODO(), &s3.ListBucketsInput{})

if err != nil {
    log.Fatalf("unable ListBuckets: , %v", err)
}
    //listObjectV2
listObjectsV2Output, err := client.ListObjectsV2(context.TODO(), &s3.ListObjectsV2Input{
    Bucket: &bucket,
})

if err != nil {
    log.Fatalf("unable listObjectsV2: , %v", err)
}
fmt.Println(listObjectsV2Output)
```
