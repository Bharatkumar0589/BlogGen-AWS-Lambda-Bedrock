S3-Bucket:

	Create bucket -> Bucket name(awsbedrockbloggen1) -> Create

Lambda Function:

Go-to==> AWS Lambda -> Create function -> function name -> runtime(Python 3.12) -> Architecture(x86_64) -> Create Function

	Once the Lambda Function created goto -->

		Configuration --> Edit(General configuration) --> Timeout = 3min --> Save

		Code and define the Lambda Function==>(BlogGenApp.py)

	To add Boto3 runtime layer with Python==3.12:
		
	     create local python folder in local machine with following command in terminal after that compress the folder and create a zip file:
		>>> pip install boto3 -t python/
		
	     To create a Layer goto:
		Open the layers -> Create layer ->  Name: boto3updatedlayer -> upload .zip file -> Compatible runtimes(Python== 3.10,3.11,3.12) -> Create

	     then goto Lambda function paste the code(BlogGenApp.py)-> Deploy:
		Lambda-> Layers-> Add layer-> Custom layers -> boto3updatedlayer -> Version = 1 -> Add

To Trigger the Lambda Function:

	goto --> AWS API Gateway -> Create API -> Build(HTTP API) -> API Name(bedrockbloggenapi) -> review and Create -> create --> Routes for xxxx Create -> POST(/bolg-generation) -> Create -> Attach integrations -> Create an integration -> Integration type(Lambda Function) -> Choose Lambda function -> Create -> Stages(Dev) -> Deploy

(https://xxxxxxxx.execute-api.us-east-1.amazonaws.com/dev/bolg-generation) use this in postman to trigger the api to generate blog:

		body(raw)==>{
			     "blog_topic":"your blog topic"
			     }