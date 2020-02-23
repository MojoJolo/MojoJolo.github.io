---
layout: post
title: "MLflow Models gRPC Wrapper"
date: 2020-02-23
description: This post talks about the boilerplate gRPC wrapper that I created for MLflow Models.
---

I've been reading about MLflow for a week now. It seems a solution to one of our problems at work. We have a problem that it takes time to deploy models provided to us by the data science team. This is due to a variety of reasons, but mostly because it takes time for us to deploy the models.

It should not be the case though. That is why I looked for ways to improve our deployment process. Here comes MLflow. MLflow is interesting because it comprises of three parts: Tracking, Projects, and Models. And from my experience, you don't need to setup all of those parts for MLflow to work.

I have my eye on MLflow Models. As I skimmed through the documentation, I learned that packaging a model into a standard format is just a few lines of code and commands. With `mlflow models serve` command, most models can be deployed in a REST API as easy as that.

### Not using REST

But what if we don't want to use REST? Well, MLflow also allows us to load the model inline through `mlflow.pyfunc.load_model(MODEL_PATH)`. It is convenient because we can use it to implement a gRPC wrapper for MLflow Models.

#### mlflow-grpc
[https://github.com/MojoJolo/mlflow-grpc](https://github.com/MojoJolo/mlflow-grpc)

In this repository, I tried to create a gRPC wraper for MLflow Models. Creating a boilerplate gRPC server is easy. There are lots of tutorials about it ([here](https://grpc.io/docs/quickstart/python/) and [here](https://www.semantics3.com/blog/a-simplified-guide-to-grpc-in-python-6c4e25f0c506/)).

In my wrapper, it accepts a string input as defined in the `mlflow.proto` and also returns a string output. This can easily be changed to different data types (refer to this [guide](https://developers.google.com/protocol-buffers/docs/overview) by Google).

```
syntax = "proto3";

message Input {
    string value = 1;
}

message Output {
    string value = 1;
}

service MLflow {
    rpc predict(Input) returns (Output) {}
}
```

The file `server.py` contains most of the code that involves loading the model, serving it, and starting the server.

Most of the code here are boilerplate and just basic functionality. Nevertheless, this can still be used to serve MLflow models in gRPC as an alternative to the REST API that MLflow provides.