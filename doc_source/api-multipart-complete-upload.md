# Complete Multipart Upload \(POST uploadID\)<a name="api-multipart-complete-upload"></a>

## Description<a name="api-multipart-complete-upload-description"></a>

You call this multipart upload operation to inform Amazon Glacier that all the archive parts have been uploaded and Amazon Glacier can now assemble the archive from the uploaded parts\. 

For information about multipart upload, see [Uploading Large Archives in Parts \(Multipart Upload\)](uploading-archive-mpu.md)\.

After assembling and saving the archive to the vault, Amazon Glacier returns the archive ID of the newly created archive resource\. After you upload an archive, you should save the archive ID returned to retrieve the archive at a later point\. 

In the request, you must include the computed SHA256 tree hash of the entire archive you have uploaded\. For information about computing a SHA256 tree hash, see [Computing Checksums](checksum-calculations.md)\. On the server side, Amazon Glacier also constructs the SHA256 tree hash of the assembled archive\. If the values match, Amazon Glacier saves the archive to the vault; otherwise, it returns an error, and the operation fails\. The [List Parts \(GET uploadID\)](api-multipart-list-parts.md) operation returns list of parts uploaded for a specific multipart upload\. It includes checksum information for each uploaded part that can be used to debug a bad checksum issue\.

Additionally, Amazon Glacier also checks for any missing content ranges\. When uploading parts, you specify range values identifying where each part fits in the final assembly of the archive\. When assembling the final archive Amazon Glacier checks for any missing content ranges and if there are any missing content ranges, Amazon Glacier returns an error and the Complete Multipart Upload operation fails\. 

Complete Multipart Upload is an idempotent operation\. After your first successful complete multipart upload, if you call the operation again within a short period, the operation will succeed and return the same archive ID\. This is useful in the event you experience a network issue that causes an aborted connection or receive a 500 server error, in which case you can repeat your Complete Multipart Upload request and get the same archive ID without creating duplicate archives\. Note, however, that after the multipart upload completes, you cannot call the List Parts operation and the multipart upload will not appear in List Multipart Uploads response, even if idempotent complete is possible\.

## Requests<a name="api-multipart-complete-upload-requests"></a>

To complete a multipart upload, you send an HTTP POST request to the URI of the upload ID that Amazon Glacier created in response to your Initiate Multipart Upload request\. This is the same URI you used when uploading parts\. In addition to the common required headers, you must include the result of the SHA256 tree hash of the entire archive and the total size of the archive in bytes\.

### Syntax<a name="api-multipart-complete-upload-requests-syntax"></a>

```
1. POST /AccountId/vaults/VaultName/multipart-uploads/uploadID
2. Host: glacier.Region.amazonaws.com
3. Date: date
4. Authorization: SignatureValue
5. x-amz-sha256-tree-hash: SHA256 tree hash of the archive
6. x-amz-archive-size: ArchiveSize in bytes
7. x-amz-glacier-version: 2012-06-01
```

**Note**  
The `AccountId` value is the AWS account ID of the account that owns the vault\. You can either specify an AWS account ID or optionally a single '`-`' \(hyphen\), in which case Amazon Glacier uses the AWS account ID associated with the credentials used to sign the request\. If you use an account ID, do not include any hyphens \('\-'\) in the ID\.

### Request Parameters<a name="api-multipart-complete-upload-requests-parameters"></a>

This operation does not use request parameters\.

### Request Headers<a name="api-multipart-complete-upload-requests-headers"></a>

This operation uses the following request headers, in addition to the request headers that are common to all operations\. For more information about the common request headers, see [Common Request Headers](api-common-request-headers.md)\.


|  Name  |  Description  |  Required  | 
| --- | --- | --- | 
| x\-amz\-archive\-size   |  The total size, in bytes, of the entire archive\. This value should be the sum of all the sizes of the individual parts that you uploaded\. Type: String Default: None Constraints: None  |  Yes | 
|  x\-amz\-sha256\-tree\-hash​  |  The SHA256 tree hash of the entire archive\. It is the tree hash of SHA256 tree hash of the individual parts\. If the value you specify in the request does not match the SHA256 tree hash of the final assembled archive as computed by Amazon Glacier, Amazon Glacier returns an error and the request fails\. Type: String Default: None Constraints: None  |  Yes | 

### Request Elements<a name="api-multipart-complete-upload-requests-elements"></a>

This operation does not use request elements\.

## Responses<a name="api-multipart-complete-upload-responses"></a>

Amazon Glacier creates a SHA256 tree hash of the entire archive\. If the value matches the SHA256 tree hash of the entire archive you specified in the request, Amazon Glacier adds the archive to the vault\. In response it returns the HTTP `Location` header with the URL path of the newly added archive resource\. If the archive size or SHA256 that you sent in the request does not match, Amazon Glacier will return an error and the upload remains in the incomplete state\. It is possible to retry the Complete Multipart Upload operation later with correct values, at which point you can successfully create an archive\. If a multipart upload does not complete, then eventually Amazon Glacier will reclaim the upload ID\.

### Syntax<a name="api-multipart-complete-upload-responses-syntax"></a>

```
HTTP/1.1 201 Created
x-amzn-RequestId: x-amzn-RequestId
Date: Date
Location: Location
x-amz-archive-id: ArchiveId
```

### Response Headers<a name="api-multipart-complete-upload-responses-headers"></a>

A successful response includes the following response headers, in addition to the response headers that are common to all operations\. For more information about common response headers, see [Common Response Headers](api-common-response-headers.md)\.


|  Name  |  Description  | 
| --- | --- | 
|  Location  |  The relative URI path of the newly created archive\. This URL includes the archive ID that is generated by Amazon Glacier\.  Type: String  | 
|  x\-amz\-archive\-id  |  The ID of the archive\. This value is also included as part of the `Location` header\. Type: String  | 

### Response Fields<a name="api-multipart-complete-upload-responses-elements"></a>

This operation does not return a response body\.

## Example<a name="api-multipart-complete-upload-examples"></a>

### Example Request<a name="api-multipart-complete-upload-example-request"></a>

In this example, an HTTP POST request is sent to the URI that was returned by an Initiate Multipart Upload request\. The request specifies both the SHA256 tree hash of the entire archive and the total archive size\. 

```
1. POST /-/vaults/examplevault/multipart-uploads/OW2fM5iVylEpFEMM9_HpKowRapC3vn5sSL39_396UW9zLFUWVrnRHaPjUJddQ5OxSHVXjYtrN47NBZ-khxOjyEXAMPLE HTTP/1.1
2. Host: glacier.us-west-2.amazonaws.com
3. z-amz-Date: 20141123T120000Z
4. x-amz-sha256-tree-hash:1ffc0f54dd5fdd66b62da70d25edacd0
5. x-amz-archive-size:8388608
6. x-amz-glacier-version: 2012-06-01
7. Authorization: AWS4-HMAC-SHA256 Credential=AKIAIOSFODNN7EXAMPLE/20141123/us-west-2/glacier/aws4_request,SignedHeaders=host;x-amz-date;x-amz-glacier-version,Signature=9257c16da6b25a715ce900a5b45b03da0447acf430195dcb540091b12966f2a2
```

### Example Response<a name="api-multipart-complete-upload-example-response"></a>

The following example response shows that Amazon Glacier successfully created an archive from the parts you uploaded\. The response includes the archive ID with complete path\. 

```
1. HTTP/1.1 201 Created
2. x-amzn-RequestId: AAABZpJrTyioDC_HsOmHae8EZp_uBSJr6cnGOLKp_XJCl-Q
3. Date: Sun, 23 Nov 2014 12:00:00 GMT
4. Location: /111122223333/vaults/examplevault/archives/NkbByEejwEggmBz2fTHgJrg0XBoDfjP4q6iu87-TjhqG6eGoOY9Z8i1_AUyUsuhPAdTqLHy8pTl5nfCFJmDl2yEZONi5L26Omw12vcs01MNGntHEQL8MBfGlqrEXAMPLEArchiveId
5. x-amz-archive-id: NkbByEejwEggmBz2fTHgJrg0XBoDfjP4q6iu87-TjhqG6eGoOY9Z8i1_AUyUsuhPAdTqLHy8pTl5nfCFJmDl2yEZONi5L26Omw12vcs01MNGntHEQL8MBfGlqrEXAMPLEArchiveId
```

You can now send HTTP requests to the URI of the newly added resource/archive\. For example, you can send a GET request to retrieve the archive\. 

## Related Sections<a name="related-sections-complete-mpu"></a>

+ [Initiate Multipart Upload \(POST multipart\-uploads\)](api-multipart-initiate-upload.md)

+ [Upload Part \(PUT uploadID\)](api-upload-part.md)

+ [Abort Multipart Upload \(DELETE uploadID\)](api-multipart-abort-upload.md)

+ [List Multipart Uploads \(GET multipart\-uploads\)](api-multipart-list-uploads.md)

+ [List Parts \(GET uploadID\)](api-multipart-list-parts.md)

+ [Uploading Large Archives in Parts \(Multipart Upload\)](uploading-archive-mpu.md)

+  [Delete Archive \(DELETE archive\)](api-archive-delete.md)

+ [Authentication and Access Control for Amazon Glacier](auth-and-access-control.md)