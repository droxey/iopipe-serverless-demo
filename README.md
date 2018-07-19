# iopipe-serverless-demo

1. Log in to the [IOpipe](https://www.iopipe.com) website.

1. **Export** your project's `IOPIPE_TOKEN` and `AWS_PROFILE` **environment variables** to the **current environment**:

    ```bash
    $ export IOPIPE_TOKEN=384_CHAR_STRING_GET_FROM_IOPIPE_WEBSITE_AFTER_CREATING_A_PROJECT
    $ export AWS_PROFILE=notesapp
    ```
1. Continue the rest of the deployment in the
**same terminal window**. Next, **clone and navigate** to this example project in your **local filesystem**:

    ```bash
    $ git clone git@github.com:outputs-io/iopipe-serverless-demo.git && cd iopipe-serverless-demo
    ```

1. **Install the `iopipe` package**: `npm install @iopipe/iopipe`

1. **Edit `package.json`**: `code package.json`

1. **Add** the following **configuration entries** to `package.json`:

   ```json
   {
     "dependencies": {
       "@iopipe/trace": "^0.2.0",
       "@iopipe/profiler": "^0.1.0"
     },
     "iopipe": {
       "plugins": [
         "@iopipe/trace",
         ["@iopipe/profiler", {"enabled": true}]
       ]
     }
   }
   ```

1. **Package** up the code: `npm run pkg`

1. **Deploy application**:

   ```bash
   $ sls deploy
   Serverless: Packaging service...
   Serverless: Excluding development dependencies...
   Serverless: Creating Stack...
   Serverless: Checking Stack create progress...
   .....
   Serverless: Stack create finished...
   Serverless: Uploading CloudFormation file to S3...
   Serverless: Uploading artifacts...
   Serverless: Uploading service .zip file to S3 (18.68 MB)...
   Serverless: Validating template...
   Serverless: Updating Stack...
   Serverless: Checking Stack update progress...
   ...............
   Serverless: Stack update finished...
   Service Information
   service: examples
   stage: dev
   region: us-west-2
   stack: examples-dev
   api keys:
     None
   endpoints:
     None
   functions:
     express: examples-dev-express
   ```

1. Finally, **call the function** to **test**:

   ```bash
   $ sls invoke -f express
   {
       "statusCode": 200,
       "body": "{\"success\":true}",
       "headers": {
           "x-powered-by": "Express",
           "content-type": "application/json; charset=utf-8",
           "content-length": "16",
           "etag": "W/\"10-oV4hJxRVSENxc/wX8+mA4/Pe4tA\"",
           "date": "Thu, 19 Jul 2018 09:28:53 GMT",
           "connection": "close"
       },
       "isBase64Encoded": false
   }
   ```

1. **Congrats!** _You've just deployed your first serverless application!_
