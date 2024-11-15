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

### Go to the "Permissions" tab.
Under "Bucket policy," enter the policy provided, adjusting the "Resource" field to match your bucket's ARN with "/*" at the end.
Uploading Your Website Files
Upload your website files, including an "index.html" file to serve as the main page.

## Finalizing Configuration
Return to the "Properties" tab and copy the endpoint URL for your bucket.
This URL will serve your "index.html" file as the homepage. If the index file is missing, the "error.html" page (if configured) will display instead.

### Sample Website Pages
The following are example pages for your website:
index.html: A basic static webpage with content tailored to AWS S3.
error.html: A custom error page (e.g., 404) for handling missing files.

## CI/CD Deployment to AWS S3 Bucket with GitHub Actions
To automate deployment to AWS S3 using GitHub Actions, follow these steps:

### Step 1: Add AWS Secrets to GitHub
In your GitHub repository, go to Settings.
In the left sidebar, select Secrets and Variables and then choose Actions.
Click New repository secret and add the following secrets:
### AWS_S3_BUCKET: Your S3 bucket name.
### AWS_ACCESS_KEY_ID: Your AWS access key ID.
### AWS_SECRET_ACCESS_KEY: Your AWS secret access key.

### Step 2: Create a GitHub Actions Workflow
In your project’s root directory, create a folder named .github/workflows.
Inside this folder, create a new file, e.g., deploy.yml.
Copy the following code into the deploy.yml file. Modify the branch name if needed to match the branch you want to deploy from.

    name: Upload Website
      on:
    push:
        branches: [ "main" ]
    pull_request:
         branches: [ "main" ]
    
    jobs:
      build:
      runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install dependencies
        run: npm install

      - name: Build app
        run: npm run build

      - name: Upload to S3
        uses: jakejarvis/s3-sync-action@master
        with:
          args: --acl public-read
        env:
          SOURCE_DIR: build/
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
Commit and push your changes to GitHub.

### Step 3: Verify the Deployment
Go to the Actions tab in your GitHub repository to monitor the deployment process.
Once the workflow completes successfully, your website files should be uploaded to S3 and accessible via the bucket's endpoint URL.


## Conclusion
By following these steps, you can easily host a static website on AWS S3. 





