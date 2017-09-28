# React Google Cloud Storage

A step by step guide into deploying your react app to Google Cloud Storage.

#### Assumptions:
* You created your react app with create-react-app. If you are looking to create your own React app look into: https://github.com/facebookincubator/create-react-app
* You have already created a project under the Google Cloud Platform

### Step 1:
Within your root folder of your react app type. 
```
npm run build
```
This should create a build folder in your project directory.

### Step 2: 
Now open up your browser and navigate to https://console.cloud.google.com/storage/.
If you haven't created a project yet do so and then come back to this step. Assuming you have click Create Bucket or go here https://console.cloud.google.com/storage/create-bucket.
Now choose a bucket name - mine is test-app, and select Multi-Regional and click create.

### Step 3:
Open up your file explorer and select the entire build folder and drag and drop it into Bucket/test-application folder, it should say drop files here.

### Step 4: 
Create a new file called app.yaml with your favorite text editor and copy the following into it.
```
runtime: python27
api_version: 1
threadsafe: true
handlers:
- url: /
  static_files: build/index.html
  upload: build/index.html
- url: /
  static_dir: build
```
Now go ahead and upload this file the same way you did the build folder.

### Step 5:
Now that all your files have been uploaded look at your navigation pane and you should see something labeled as Activate Google Cloud Shell, click on this.

### Step 6:
Now comes the easy part, copy these steps into your Google Cloud Shell to deploy your app.
```
mkdir test-app
gsutil rsync -r gs://test-application ./test-app
cd test-app
gcloud config set project [HERE IS YOUR PROJECTID]
gcloud app deploy
```
With your last command you should also get a url to navigate to.
