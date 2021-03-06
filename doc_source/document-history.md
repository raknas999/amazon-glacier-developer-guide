# Document History<a name="document-history"></a>

The following table describes the important changes since the last release of the *Amazon Glacier Developer Guide*\.

**Relevant Dates to this History:**

+ **Current product version:** 2012\-06\-01

+ **Last documentation update:** November 29, 2017


| Change | Description | Release Date | 
| --- | --- | --- | 
|  Querying archives with SQL  |  Amazon Glacier now supports querying data archives with SQL\. For more information, see [Querying Archives with Amazon Glacier Select](glacier-select.md)\. The following APIs are updated accordingly:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/amazonglacier/latest/dev/document-history.html)  |  In this release   | 
|  Expedited and Bulk Data Retrievals  |  Amazon Glacier now supports Expedited and Bulk data retrievals in addition to Standard retrievals\. For more information, see [Archive Retrieval Options](downloading-an-archive-two-steps.md#api-downloading-an-archive-two-steps-retrieval-options)\.   |  November 21, 2016  | 
|  Vault Lock  |  Amazon Glacier now supports Vault Lock, which allows you to easily deploy and enforce compliance controls on individual Amazon Glacier vaults with a Vault Lock policy\. For more information, see [Amazon Glacier Vault Lock](vault-lock.md) and [Amazon Glacier Access Control with Vault Lock Policies](vault-lock-policy.md)\.   |  July 8, 2015  | 
|  Vault tagging  |  Amazon Glacier now allows you to tag your Amazon Glacier vaults for easier resource and cost management\. Tags are labels that you can define and associate with your vaults, and using tags adds filtering capabilities to operations such as AWS cost reports\. For more information, see [Tagging Amazon Glacier Resources](tagging.md) and [Tagging Your Amazon Glacier Vaults](tagging-vaults.md)\.  |  June 22, 2015  | 
|  Vault access policies  |  Amazon Glacier now supports managing access to your individual Amazon Glacier vaults by using vault access policies\. You can now define an access policy directly on a vault, making it easier to grant vault access to users and business groups internal to your organization, as well as to your external business partners\. For more information, see [Amazon Glacier Access Control with Vault Access Policies](vault-access-policy.md)\.  |  April 27, 2015  | 
|  Data retrieval policies and audit logging  |  Amazon Glacier now supports data retrieval policies and audit logging\. Data retrieval policies allow you to easily set data retrieval limits and simplify data retrieval cost management\. You can define your own data retrieval limits with a few clicks in the AWS console or by using the Amazon Glacier API\. For more information, see [Amazon Glacier Data Retrieval Policies](data-retrieval-policy.md)\. In addition, Amazon Glacier now supports audit logging with AWS CloudTrail, which records Amazon Glacier API calls for your account and delivers the log files to an Amazon S3 bucket that you specify\. For more information, see [Logging Amazon Glacier API Calls by Using AWS CloudTrail](audit-logging.md)\.  |  December 11, 2014  | 
|  Updates to Java samples  |  Updated the Java code samples in this guide that use the AWS SDK for Java\.  |  June 27, 2014  | 
|  Limiting vault inventory retrieval  |  You can now limit the number of vault inventory items retrieved by filtering on the archive creation date or by setting a limit\. For more information about limiting inventory retrieval, see [Range Inventory Retrieval](api-initiate-job-post.md#api-initiate-job-post-vault-inventory-list-filtering) in the [Initiate Job \(POST jobs\)](api-initiate-job-post.md) topic\.  |  December 31, 2013  | 
|  Removed outdated URLs  |  Removed the URLs that pointed to the old security credentials page from code examples\.  |  July 26, 2013  | 
|  Support for range retrievals  |  Amazon Glacier now supports retrieval of specific ranges of your archives\. You can initiate a job requesting Amazon Glacier to prepare an entire archive or a portion of the archive for subsequent download\. When an archive is very large, you may find it cost effective to initiate several sequential jobs to prepare your archive\.  For more information, see [Downloading an Archive in Amazon Glacier](downloading-an-archive.md)\. For pricing information, go to the [Amazon Glacier detail page](http://aws.amazon.com/glacier)\.   |  November 13, 2012  | 
|  New Guide  |  This is the first release of the *Amazon Glacier Developer Guide*\.   |  August 20, 2012  | 