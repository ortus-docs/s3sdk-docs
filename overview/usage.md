# Usage

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

## listBuckets

List all the buckets associated with your Amazon credentials.

```javascript
/**
 * @return An array of structs containing the bucket name and creation date.
 */
array function listBuckets();
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
