<p align="center">
  <a href="https://dev.to/vumdao">
    <img alt="Create Cron Jobs on AWS Lambda with cloudwatch event" src="https://dev-to-uploads.s3.amazonaws.com/i/g7i755v13fkb9nxqqkr0.jpg" width="500" />
  </a>
</p>


## Quick start aws-chalice
## A very simple example of creating lambda function with cloudwatch event using aws-chalice. It provides an optional of how to create lambda function beyond aws-cdk (eg. [python lamdbda cron](https://github.com/aws-samples/aws-cdk-examples/blob/master/python/lambda-cron))


## What’s In This Document 
- [Create new chalice project](#-Create-new-chalice-project)
- [Create the functions in app.py](#-Create-the-functions-in-app.py)
- [Config lambda fuction attributes](#-Config-lambda-fuction-attributes)
- [Deploy chalice to create cloudwatch event which trigger lambda cron](#-Deploy-chalice-to-create-cloudwatch-event-which-trigger-lambda-cron)
- [Check result](#-Check-result)
- [Clean up](#-Clean-up)


### 🚀 **[Create new chalice project](#-Create-new-chalice-project)**
```
⚡ $ chalice new-project lambda-cron
⚡ $ cd lambda-cron/
```

### 🚀 **[Create the functions in app.py](#-Create-the-functions-in-app.py)**
[app,py](https://github.com/vumdao/lambda-cron/blob/master/app.py)
```
from datetime import datetime
from chalice import Chalice


app = Chalice(app_name='lambda-cron')
app.debug = True


#@app.schedule('cron(0 18 ? * MON-FRI *)')
@app.schedule('cron(* * ? * * *)')
def cron_tab(event):
    print(f"{datetime.now()}: I'm running!")
```

### 🚀 **[Config lambda fuction attributes](#-Config-lambda-fuction-attributes)**
- Here is just config lambda timeout 
```
⚡ $ cat .chalice/config.json 
{ 
  "version": "2.0",
  "app_name": "lambda-cron",
  "stages": {
    "dev": {
      "lambda_timeout": 300
    }
  } 
}
```

### 🚀 **[Deploy chalice to create cloudwatch event which trigger lambda cron](#-Deploy-chalice-to-create-cloudwatch-event-which-trigger-lambda-cron)**
```
⚡ $ chalice deploy
Creating deployment package.
Creating IAM role: lambda-cron-dev
Creating lambda function: lambda-cron-dev-cron_tab
Resources deployed:
  - Lambda ARN: arn:aws:lambda:ap-northeast-2:111111111111:function:lambda-cron-dev-cron_tab
```

- Note: Chalice auto create IAM role `lambda-cron-dev` base on the need of the function, we can disable by adding `"manage_iam_role": false` but you must provide the IAM ARN in `config.json` eg. ` "iam_role_arn": "arn:aws:iam::111111111111:role/lambda-cron-dev"`

### 🚀 **[Check result](#-Check-result)**
- Lambda function with Event Bridge trigger

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/qjy3fx8zs8f8g01r4nx7.png)

- Cloudwatch event rule

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/caxa5lhe32hxyv07tya2.png)

- Cloudwatch log group

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/f16e1604xhxkcpfro3t1.png)


### 🚀 **[Clean up](#-Clean-up)**
```
⚡ $ chalice delete
Deleting function: arn:aws:lambda:ap-northeast-2:111111111111:function:lambda-cron-dev-cron_tab
Deleting IAM role: lambda-cron-dev
```

### **Visit wwww.cloudopz.co to get more**

<h3 align="center">
  <a href="https://dev.to/vumdao">:stars: Blog</a>
  <span> · </span>
  <a href="https://vumdao.hashnode.dev/">Web</a>
  <span> · </span>
  <a href="https://www.linkedin.com/in/vu-dao-9280ab43/">Linkedin</a>
  <span> · </span>
  <a href="https://www.linkedin.com/groups/12488649/">Group</a>
  <span> · </span>
  <a href="https://www.facebook.com/CloudOpz-104917804863956">Page</a>
  <span> · </span>
  <a href="https://twitter.com/VuDao81124667">Twitter :stars:</a>
</h3>