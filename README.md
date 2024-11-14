# Hosting a Static Website on AWS S3

## Accessing the AWS Console
Log in to your AWS Management Console and type "S3" into the search bar. Select "S3" from the results.

### Creating a New Bucket
Click "Create bucket."
Enter a unique "Bucket name", in this case, I used "Add-To-Card" for your website.

### Configuring Bucket Settings
Deselect "Block all public access" to allow users to access your website.
Click "Create bucket" to finalize.
Selecting Your Bucket
After the bucket is created, select it from the list of available buckets.

## Setting Up Static Website Hosting
In the "Properties" tab, scroll down to "Static web hosting" and click "Edit."
Select "Enable" and choose "Host a static website."
Specify the home page (index document) for your site.
Optional: Configuring Error Handling
If desired, set an error document name for handling errors and click "Save changes."


Endpoint Creation
Once static website hosting is enabled, an endpoint URL for your bucket is generated.

### Adding a Bucket Policy for Public Access
To make your files accessible, add a bucket policy:

Go to the "Permissions" tab.
Under "Bucket policy," enter the policy provided, adjusting the "Resource" field to match your bucket's ARN with "/*" at the end.
Uploading Your Website Files
Upload your website files, including an "index.html" file to serve as the main page.

## Finalizing Configuration
Return to the "Properties" tab and copy the endpoint URL for your bucket.
This URL will serve your "index.html" file as the homepage. If the index file is missing, the "error.html" page (if configured) will display instead.
Sample Website Pages
The following are example pages for your website:

index.html: A basic static webpage with content tailored to AWS S3.
error.html: A custom error page (e.g., 404) for handling missing files.

## Conclusion
By following these steps, you can easily host a static website on AWS S3. 





