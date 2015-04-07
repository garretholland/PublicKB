{{{
  "title": "Persisting Wordpress Files",
  "date": "04-02-2015",
  "author": "Bill Burge",
  "attachments": [],
  "contentIsHTML": false
}}}

<h3>Persisting Wordpress Files</h3>

CenturyLink Cloud WordPress sites utilize Object Storage for persistent WordPress content files such as images and file attachments.  In order to utilize persistent storage you must first manually configure Centurylink Cloud Object Storage using the following link:

[Using object storage from the control portal](../Object Storage/using-object-storage-from-the-control-portal.md)

Once object storage has been configured, you must edit your base  WordPress *wp-config.php* file on http://www.github.com to integrate your Wordpress site with your object storage account.  

---

**Note: There are many methods to edit and commit this file. This guide covers editing it in place on http://www.github.com.**

---

**1. Login to http://www.github.com using the GitHub username and password provided to CenturyLink during your WordPress installation.**

**2. Browse to the GitHub repository associated with your WordPress blog and open wp-config.php**

![](../images/persisting-wordpress-files_1.png "persisting-wordpress-files_1.png")

**3. In the upper right-hand corner, click the pencil icon to _Edit the file_**

![](../images/persisting-wordpress-files_2.png "persisting-wordpress-files_2.png")

**4. Find the section of the file labeled _CenturyLink Object Storage Customer Variables_**

In this section you will see three replaceable variables:

1. customer_access_key
2. customer_secret_access_key
3. customer_bucket

**NOTE: These are variables you will have obtained when configuring your [CenturyLink Cloud Object Storage.](../Object Storage/using-object-storage-from-the-control-portal.md)**

![](../images/persisting-wordpress-files_3.png "persisting-wordpress-files_3.png")

_The following example shows the variables replaced:_

![](../images/persisting-wordpress-files_4.png "persisting-wordpress-files_4.png")

**5. Once you have updated the file, browse to the bottom of the screen, input a reason for the changes, and click _Commit changes_**

![](../images/persisting-wordpress-files_5.png "persisting-wordpress-files_5.png")

**6. Login to your CenturyLink Cloud WordPress Blog Dashboard utilizing the password supplied during setup.**

**7. Expand Plugins in the left column.**

![](../images/persisting-wordpress-files_6.png "persisting-wordpress-files_6.png")

**8. Click Activate next to the Amazon Web Services plugin.**

![](../images/persisting-wordpress-files_7.png "persisting-wordpress-files_7.png")

**9. Click Activate next to the Amazon S3 and CloudFront plugin.

![alt text](../images/persisting-wordpress-files_8.png "persisting-wordpress-files_8.png")

**10. Expand AWS in the left column.**

![](../images/persisting-wordpress-files_9.png "persisting-wordpress-files_9.png")

**11. Select S3 and Cloudfront**

![](../images/persisting-wordpress-files_10.png "persisting-wordpress-files_10.png")

**12. Ensure the following settings are configured:**

**S3 Settings**
* Ensure the bucket you created is selected in the drop down
* Bucket is setup for virtual hosting - **UNCHECKED**
* Set a far future HTTP expiration header for uploaded files - **CHECKED**
* Object Path: /uploads/

**CloudFront Settings**
* Domain Name - **BLANK**
* Implement object versioning by appending a timestamp to the S3 file path - **UNCHECKED**

**Plugin Settings**
* Copy files to S3 as they are uploaded to the Media Library - **CHECKED**
* Point file URLs to S3/CloudFront for files that have been copied to S3 - **CHECKED**
* Remove uploaded file from local filesystem once it has been copied to S3 - **CHECKED**
* Always serve files over https (SSL) - **CHECKED**
* Copy any HiDPI (@2x) images to S3 (works with WP Retina 2x plugin) - **UNCHECKED**

*The following example is correctly configured:*

![](../images/persisting-wordpress-files_11.png "persisting-wordpress-files_11.png")

**13. Once settings are verified, click *Save Changes* to commit configuration changes.**

![](../images/persisting-wordpress-files_12.png "persisting-wordpress-files_12.png")