# Common Response Headers<a name="api-common-response-headers"></a>

The following table describes response headers that are common to most Amazon Glacier responses\.


|  Name  |  Description  | 
| --- | --- | 
| Content\-Length |  The length in bytes of the response body\. Type: String  | 
| Date |  The date and time Amazon Glacier responded, for example, `Sun, 23 Nov 2014 12:00:00 GMT`\. The format of the date must be one of the full date formats specified by [RFC 2616](http://tools.ietf.org/html/rfc2616#section-3.3), section 3\.3\. Note that `Date` returned may drift slightly from other dates, so for example, the date returned from an [Upload Archive \(POST archive\)](api-archive-post.md) request may not match the date shown for the archive in an inventory list for the vault\.  Type: String  | 
| x\-amzn\-RequestId |  A value created by Amazon Glacier that uniquely identifies your request\. In the event that you have a problem with Amazon Glacier, AWS can use this value to troubleshoot the problem\. It is recommended that you log these values\. Type: String  | 
| x\-amz\-sha256\-tree\-hash​ |  The SHA256 tree\-hash checksum of the archive or inventory body\. For more information about calculating this checksum, see [Computing Checksums](checksum-calculations.md)\. Type: String  | 