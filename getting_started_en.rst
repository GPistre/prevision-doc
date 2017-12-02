# Building a machine learning model with Prevision.io

## The data
In this tutorial, we're going to create a predictive model from data
using the Prevision.io platform.
We're going to use a public training set from the UCI machine learning
repository, the "Bank Marketing Data Set" where the objective is to
predict whether or not a customer will buy a product.


You can download the dataset here:

https://archive.ics.uci.edu/ml/machine-learning-databases/00222/

And here is a quick peek at the data. The column we want to predict
is called "**y**" and can take the values "yes" and "no" (it is therefore
a binary classification problem). The model we build will output
 the probability that a particular customer will buy the product.



Here's what you need to do with the data before connecting to the platform:
 - Make sure we're dealing with an actual supervised machine learning problem, that is that we have a specific column we want to predict based on the rest of the data.

And here's what you don't need to worry about :
- Missing values. They will be handled directly by the platform.
- Categorical variable encoding. The best encoding will be determined by the platform.
- Text variables. The appropriate embedding or statistical analysis will be done automatically.
- Normalization. Based on the models used, the variables will be pre-processed accordingly.


## Creating a project

You can now go on the Prevision.io website, and either log in to your account,
or register one if you didn't yet.

The first screen you'll see is the dashboard, with all your projects.
Most plans for now only support a single model training at the same time, so if you already have a project running,
you can either wait for it to be over or stop it (not that you will not be able to start it again, stopping is definitive)

![alt text](https://prevision.io/cdn/img/dashboard.png "The dashboard")

You can click on "New Project", which will take you to a new page to define your project.

Here you'll be able to select how you want to import your dataset. (for now, only .CSV files are available,
Hadoop Hive and standard SQL connectors are coming very soon).

### Importing a .CSV file

![alt text](https://prevision.io/cdn/img/newmodel1.png "New project")

Click on "Choose file" and browse to your dataset file. The platform will import a sample and parse it.

![alt text](https://prevision.io/cdn/img/newmodel2.png "Task selection")

You will see all the variables of your dataset, and you'll be able to
define which one is the target (which one is the one you want to predict).
If your dataset has an "ID", a column indexing every row of the table,
you can select it for the platform to recognize it.
You can also choose to exclude some columns that won't be used for training.
In our case, the dataset has no id, so we leave the field blank, we'll use all columns, and select "**y**" as the target.
Note that if your target column is called "target", the platform will automatically select it. Same for the ID.


Since the "**y**" column only contains two values, the platform detected this is likely a binary classification task
and selected the appropriate choice in the menu. You can choose which metric will be used to optimize the models.
You will still be able to see other metrics once the models are trained (see further below) but the one you choose now
will be used by the platform to train and select the models. If you're not sure what to choose, the default option is usually the best.

All you have to do now is to click on "train models" and the platform will start the real work. You can monitor the
training and performance of your models in the "Performance tab of your project" where you'll see the different
models get built and improve their performance, and you can get info about the nature of the models used by hovering
on the different steps of the curve.

![alt text](https://prevision.io/cdn/img/training.png "Monitoring model progress")

For training, your work is now done, and Prevision.io will do all the rest, but we'll see how to better understand your models and
use them in applications.
Training powerful machine learning models is computationally expensive,
and on large datasets, it can easily take several hours to several days.
As we'll see in the "using you models" section, however, it doesn't prevent your from putting your model in application
from the start.

## Analysing your data and your models

### Data analysis

The model provides an automatic data analysis dashboard in the "Data analysis" tab of your project.

![alt text](https://prevision.io/cdn/img/analysis1.png "Data analysis")
![alt text](https://prevision.io/cdn/img/analysis2.png "Data analysis")

If you haven't done so yet, you can visualize and understand better your dataset, and also make sure
that the platform correctly parsed and detected the data types of the different columns.


### Model analysis & Feature importance

Once some models have been trained (usually after a few seconds -- minutes if it is a large dataset)
you can visualize information and statistics about your model.

![alt text](https://prevision.io/cdn/img/modelanalysis.png "Model analysis")

In the "Model analysis" tab, the platform has calculated different metrics relevant to your task (Accuracy, Precision, Recall, F1, etc...).
As well as a confusion matrix and an ROC curve. This screen is dependent on the task, and will have different types of analyses for
regression and multi-classification tasks.

![alt text](https://prevision.io/cdn/img/varimp.png "Feature importance page")

In the "Feature Importance" tab, you'll be able to see which variables
the platform has selected as the most important ones, giving you insight
into the problem and making the model more understandable.

## Using your models

Even though the *complete* training might take a long time, as soon as a single model
is ready, you can use it to make predictions and deploy it for production. You'll always have
a single endpoint to get predictions from your model and you'll always have access to the best one.

### Bulk predictions

![alt text](https://prevision.io/cdn/img/makeprevisions.png "Making predictions")

You can directly and easily use your models using only the web application. Supposing you have a dataset
containing the same columns as your training, but for which you don't know the value of the "**y**" column (the "test" set).
You can click on the "Make previsions" tab, and you simply need to upload a file and click on the "Make previsions"
button on the right. Once the file is ready (a few minutes at most) you can then download the result.

The file will look like this :

| ID | y_yes             |
|----|-------------------|
| 0  | 0.00139664279675  |
| 1 | 0.57057877341     |
| 2 | 0.101572731172    |
| 3 | 0.000796612865576 |
| 4 | 0.267888413178    |
| 5 | 0.000837767091249 |
| 6 | 0.000855275270632 |
| 7 | 0.0229007849533   |
| 8 | 0.266593064406    |

With the row ID on the right (if not present in the test set, the platform will create one corresponding to the row number).
And on the left, teh probability that the outcome is equal to "1", so in our case, that the customer corresponding to the ID will
purchase the offer proposed by the bank.


### Predict API

If you want to directly integrate the model with your application, you can use the Prevision.io predict API to
make predictions one by one.

Go in the "API Key" section in the menu on the right to arrive on this screen :

![alt text](https://prevision.io/cdn/img/api1.png "Managing API keys")

You select the model you want to deploy and click on "generate" to obtain the model token. You'll also get
an example json for the POST request. ("token" being to token you just generated and "owner" you owner name, indicated in the example.)

You'll need to replace :
- \<YOUR TOKEN> with the token you just generated
- \<YOUR OWNER NAME> with your owner name (usually your last name, specified in the post request example)
- \<PROJECT NAME> with the name of your project


```javascript
{
    "token": "<YOUR TOKEN>",
    "owner": "<YOUR OWNER NAME>",
    "features": {
        "age": 40.02406040594348,
        "job": "admin.",
        "marital": "married",
        "education": "university.degree",
        "default": "no",
        "housing": "yes",
        "loan": "no",
        "contact": "cellular",
        "month": "may",
        "day_of_week": "thu",
        "duration": 258.2850101971448,
        "campaign": 2.567592502670681,
        "pdays": 962.4754540157328,
        "previous": 0.17296299893172767,
        "poutcome": "nonexistent",
        "emp.var.rate": 0.08188550063125165,
        "cons.price.idx": 93.5756643682626,
        "cons.conf.idx": -40.50260027192386,
        "euribor3m": 3.621290812858114,
        "nr.employed": 5167.035910944936
    }
}
```

<br><br>

#### Calling the API from a web app with jQuery

```javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": "http://prevision.io/api/predictUnit/<PROJECT NAME>",
  "method": "POST",
  "headers": {
    "content-type": "application/json",
    "cache-control": "no-cache"
  },
  "processData": false,
  "data": "{"token":"<YOUR TOKEN>","owner":"<YOUR OWNER NAME>","features":{"age":40,"job":"admin.","marital":"married","...": "..."}}"
}

$.ajax(settings).done(function (response) {
  console.log(response);
});
```







#### Calling the API from Node.js

```javascript
var http = require("http");

var options = {
  "method": "POST",
  "hostname": "prevision.io",
  "path": "/api/predictUnit/<PROJECT NAME>",
  "headers": {
    "content-type": "application/json",
    "cache-control": "no-cache"
  }
};

var req = http.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function () {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });
});

req.write(JSON.stringify({ token: '<YOUR TOKEN>',
                            owner: 'prevision',
                           features: {age: 40,
                                      job: "admin.",
                                      marital: "married",
                                      ...: "..."
                                      }
                          })
          );
req.end();
```

<br><br>

#### Calling the API from Python (with the requests module)

```python
import requests

url = "http://prevision.io/api/predictUnit/<PROJECT NAME>"

payload = '{"token":"<YOUR TOKEN>","owner":"<YOUR OWNER NAME>","features":{"age":40,"job":"admin.","marital":"married","...": "..."}}'
headers = {
    'content-type': "application/json",
    'cache-control': "no-cache"
    }

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

<br><br>

If everything works fine, you'll get your prediction on HTTP return response with a 200 status code.

That's all you need to know to get started for now. Many more great features are coming very soon, and we'll document them as
soon as they're ready.

In the meantime, don't hesitate to reach out to us if you need help or more info at support@prevision.io.
