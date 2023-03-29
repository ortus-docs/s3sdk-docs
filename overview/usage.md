# Usage

## getBucketLocation

Gets the S3 region for the provided bucket name.

```javascript
string function getBucketLocation( required string bucketName = variables.defaultBucketName );
```

## getBucketVersionStatus

Get the versioning status of a bucket.

```javascript
string function getBucketVersionStatus( required string bucketName = variables.defaultBucketName );
```

## getFileMimeType

Determines the MIME type from the file extension. If a type cannot be determined, it returns `binary/octet-stream` by default.

```javascript
string function getFileMimeType( required string filePath );
```

## listBuckets

List all the buckets associated with your Amazon credentials.

```javascript
array function listBuckets();
```

## setBucketVersionStatus

Sets the versioning status for a bucket.

```javascript
boolean function setBucketVersionStatus(
	required string bucketName = variables.defaultBucketName,
	boolean version            = true
);
```
