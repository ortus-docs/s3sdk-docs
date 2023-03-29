# Configuration

You can configure s3sdk under moduleSettings within your config/ColdBox.cfc file.

```cfc
moduleSettings = {
	s3sdk = {
		// Your amazon, digital ocean access key
		accessKey = "",
		// Tries to determine content type of file by file extension when putting files. Defaults to false.
		autoContentType = false,
		// Calculates MD5 hash of content automatically. Defaults to false.
		autoMD5 = false,
		// Your AWS/Digital Ocean Domain Mapping: defaults to amazonaws.com
		awsDomain = "amazonaws.com",
		// Your AWS/Digital Ocean Region: Defaults to us-east-1
		awsregion = "us-east-1",
		// Used to turn debugging on or off outside of logbox. Defaults to false.
		debug = false,
		// Default access control policy for objects and buckets. Defaults to public-read.
		defaultACL = "public-read",
		// The default bucket name to root the operations on.
		defaultBucketName = "",
		// Default caching policy for objects. Defaults to: no-store, no-cache, must-revalidate
		defaultCacheControl = "no-store, no-cache, must-revalidate",
		// The default delimiter for folder operations
		defaultDelimiter = "/",
		// Default storage class for objects that affects cost, access speed and durability. Defaults to STANDARD.
		// AWS classes are: STANDARD,STANDARD_IA,INTELLIGENT_TIERING,ONEZONE_IA,GLACIER,DEEP_ARCHIVE
		// Google Cloud Storage Clases: regional,multi_regional,nearline,coldline,
		defaultStorageClass = "STANDARD",
		// Default HTTP timeout in seconds for all requests. Defaults to 300 seconds.
		defaultTimeOut = 300,
		// The default encryption character set: defaults to utf-8
		encryptionCharset = "utf-8",
		// How many times to retry the request before failing if the response is a 500 or 503
		retriesOnError		: 3,
		// Your amazon, digital ocean secret key
		secretKey = "",
		// Service name that is part of the service's endpoint (alphanumeric). Example: "s3"
		// Only used for the v4 signatures
		serviceName         : "s3",
		// The signature version to calculate, "V2" is deprecated but more compatible with other endpoints. "V4" requires Sv4Util.cfc & ESAPI on Lucee. Defaults to V4
		signature = "V4",
		// SSL mode or not on cfhttp calls and when generating put/get authenticated URLs: Defaults to true
		ssl = true,
		// Throw exceptions when s3 requests fail, else it swallows them up.
		throwOnRequestError : true
	}
};
```
