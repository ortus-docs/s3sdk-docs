# Usage

## deleteObject

Deletes an object.

```javascript
/**
 * @bucketName The bucket name the object resides in.
 * @uri        The file object uri to delete.
 *
 * @return Returns true if the object is deleted successfully.
 */
boolean function deleteObject( required string bucketName = variables.defaultBucketName, required string uri );
```

## downloadObject

Downloads an object from a bucket.

```javascript
/**
 * @bucketName          The bucket in which to store the object.
 * @uri                 The destination uri key to use when saving the object.
 * @filepath            The file path write the object to, if no filename given filename from uri is used.
 * @HTTPTimeout         The HTTP timeout to use.
 * @getAsBinary         Treat the response body as binary instead of text.
 * @encryptionAlgorithm The server side encryption algorithm to use.  Usually "AES256". Not needed if using custom encryptionKey
 * @encryptionKey       The base64 encoded AES 356 bit key for server side encryption.
 *
 * @return The object's eTag.
 */
struct function downloadObject(
	required string bucketName = variables.defaultBucketName,
	required string uri,
	required string filepath,
	numeric HTTPTimeout        = variables.defaultTimeOut,
	boolean getAsBinary        = "no",
	string encryptionAlgorithm = variables.defaultEncryptionAlgorithm,
	string encryptionKey       = variables.defaultEncryptionKey
)
```

## getAccessControlPolicy

Gets a bucket's or object's ACL policy.

```javascript
/**
 * @bucketName The bucket to get the ACL.
 * @uri        An optional resource uri to get the ACL.
 *
 * @return An array containing the ACL for the given resource.
 */
array function getAccessControlPolicy(
	required string bucketName = variables.defaultBucketName,
	string uri                 = ""
);
```

## getBucket

Lists information about the objects of a bucket.

```javascript
/**
 * @bucketName The bucket name to list.
 * @prefix     Limits the response to keys which begin with the indicated prefix, if any.
 * @marker     Indicates where in the bucket to begin listing, if any.
 * @maxKeys    The maximum number of keys you'd like to see in the response body, if any.
 * @delimiter  The delimiter to use in the keys, if any.
 * @see        https://docs.aws.amazon.com/AmazonS3/latest/API/API_ListObjectsV2.html
 *
 * @return The bucket contents.
 */
array function getBucket(
	required string bucketName = variables.defaultBucketName,
	string prefix              = "",
	string marker              = "",
	string maxKeys             = "",
	string delimiter           = variables.defaultDelimiter
)
```

## getBucketLocation

Gets the S3 region for the provided bucket name.

<pre class="language-javascript"><code class="lang-javascript">/**
 * @bucketName The bucket for which to fetch the region.
 *
 * @return The region code for the bucket.
 */
<strong>string function getBucketLocation( required string bucketName = variables.defaultBucketName );
</strong></code></pre>

## getBucketVersionStatus

Get the versioning status of a bucket.

```javascript
/**
 * @bucketName The bucket for which to fetch the versioning status.
 *
 * @return The bucket version status or an empty string if there is none.
 */
string function getBucketVersionStatus( required string bucketName = variables.defaultBucketName );
```

## getFileMimeType

Determines the MIME type from the file extension. If a type cannot be determined, it returns `binary/octet-stream` by default.

```javascript
/**
 * @filePath The path to the file stored in S3.
 *  
 * @return string
 */
string function getFileMimeType( required string filePath );
```

## getObjectInfo

Get an object's metadata information.

```javascript
/**
 * @bucketName    The bucket the object resides in.
 * @uri           The object URI to retrieve the info.
 * @encryptionKey The base64 encoded AES 356-bit key for server-side encryption.
 *
 * @return The object's metadata information.
 */
struct function getObjectInfo(
	required string bucketName = variables.defaultBucketName,
	required string uri,
	string encryptionKey = variables.defaultEncryptionKey
);
```

## listBuckets

List all the buckets associated with your Amazon credentials.

```javascript
/**
 * @return An array of structs containing the bucket name and creation date.
 */
array function listBuckets();
```

## objectExists

Check if an object exists in the bucket.

```javascript
/**
 * @bucketName The bucket the object resides in.
 * @uri        The object URI to check on.
 *
 * @return     True/false whether the object exists
 */
boolean function objectExists( required string bucketName = variables.defaultBucketName, required string uri )
```

## putBucket

Creates a new bucket.

```javascript
/**
 * @bucketName The name for the new bucket.
 * @acl        The security policy to use. Specify a canned ACL like "public-read" as a string, or provide a struct in the format of the "grants" key returned by getObjectACL()
 * @location   The bucket location.
 *
 * @return True if the bucket was created successfully.
 */
boolean function putBucket(
	required string bucketName = variables.defaultBucketName,
	string acl                 = variables.defaultACL,
	string location            = "USA"
);
```

## putObject

Puts an object into a bucket.&#x20;

```javascript
/**
 * @bucketName          The bucket in which to store the object.
 * @uri                 The destination uri key to use when saving the object.
 * @data                The content to save as data.
 * @contentDisposition  The content-disposition header to use when downloading the file.
 * @contentType         The file/data content type. Defaults to text/plain.
 * @contentEncoding     The file content encoding, useful to gzip data.
 * @HTTPTimeout         The HTTP timeout to use.
 * @cacheControl        The caching header to send. Defaults to no caching.
 * @expires             Sets the expiration header of the object in days.
 * @acl                 The security policy to use. Specify a canned ACL like "public-read" as a string, or provide a struct in the format of the "grants" key returned by getObjectACL()
 * @metaHeaders         Additional metadata headers to add.
 * @md5                 Set the MD5 hash which allows aws to checksum the object
 * @storageClass        Sets the S3 storage class which affects cost, access speed and durability.
 * @encryptionAlgorithm The server side encryption algorithm to use.  Usually "AES256". Not needed if using custom encryptionKey
 * @encryptionKey       The base64 encoded AES 356 bit key for server side encryption.
 *
 * @return The object's eTag.
 */
string function putObject(
	required string bucketName = variables.defaultBucketName,
	required string uri,
	any data                   = "",
	string contentDisposition  = "",
	string contentType         = ( variables.autoContentType ? "auto" : "text/plain" ),
	string contentEncoding     = "",
	numeric HTTPTimeout        = variables.defaultTimeOut,
	string cacheControl        = variables.defaultCacheControl,
	string expires             = "",
	any acl                    = variables.defaultACL,
	struct metaHeaders         = {},
	string md5                 = variables.autoMD5,
	string storageClass        = variables.defaultStorageClass,
	string encryptionAlgorithm = variables.defaultEncryptionAlgorithm,
	string encryptionKey       = variables.defaultEncryptionKey
)
```

## putObjectFile

Puts an object from a local file into a bucket.

```javascript
/**
 * @bucketName          The bucket in which to store the object.
 * @filepath            The absolute file path to read in the binary.
 * @uri                 The destination uri key to use when saving the object.
 * @contentType         The file content type. Defaults to binary/octet-stream.
 * @contentEncoding     The file content encoding, useful to gzip data.
 * @HTTPTimeout         The HTTP timeout to use
 * @cacheControl        The caching header to send. Defaults to no caching.
 * @expires             Sets the expiration header of the object in days.
 * @acl                 The security policy to use. Specify a canned ACL like "public-read" as a string, or provide a struct in the format of the "grants" key returned by getObjectACL()
 * @metaHeaders         Additional metadata headers to add.
 * @md5                 Set the MD5 hash, which allows aws to checksum the object
 * @storageClass        Sets the S3 storage class which affects cost, access speed and durability.
 * @encryptionAlgorithm The server-side encryption algorithm to use.  Usually "AES256". Not needed if using custom encryptionKey
 * @encryptionKey       The base64 encoded AES 356-bit key for server-side encryption.
 *
 * @return The file's eTag
 */
string function putObjectFile(
	required string bucketName = variables.defaultBucketName,
	required string filepath,
	string uri                 = "",
	string contentType         = "",
	string contentEncoding     = "",
	numeric HTTPTimeout        = variables.defaultTimeout,
	string cacheControl        = variables.defaultCacheControl,
	string expires             = "",
	any acl                    = variables.defaultACL,
	struct metaHeaders         = {},
	string md5                 = variables.autoMD5,
	string storageClass        = variables.defaultStorageClass,
	string encryptionAlgorithm = variables.defaultEncryptionAlgorithm,
	string encryptionKey       = variables.defaultEncryptionKey
)
```

## setBucketVersionStatus

Sets the versioning status for a bucket.

<pre class="language-javascript"><code class="lang-javascript">/**
 * @bucketName The bucket to set the versioning status.
 * @version    The status for the versioning property.
 *
 * @return True if the request was successful.
 */
<strong>boolean function setBucketVersionStatus(
</strong>	required string bucketName = variables.defaultBucketName,
	boolean version            = true
);
</code></pre>

\
