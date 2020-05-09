---
title: Protocol Buffers Using gRPC-Web with ASP.NET Core 3.1 and Angular 9
excerpt: Get started with the basics of Protocol Buffers!
header:
  teaser: ''
categories:
- Web Development
tags:
- Protocol Buffers
- gRPC
- Angular
- ASP.NET Core
comments: true

---
I'm going to be creating an Angular 9 app on Windows 10 using gPRC-Web to communicate to gRPC endpoints hosted in a ASP.NET Core 3.1 API.

gRPC-Web allows you to have a contract between your client web app and a gRPC backend service. For more see [https://grpc.io/blog/grpc-web-ga/](https://grpc.io/blog/grpc-web-ga/ "https://grpc.io/blog/grpc-web-ga/")

## Steps

1. Go here [`https://github.com/protocolbuffers/protobuf/releases/latest`](https://github.com/protocolbuffers/protobuf/releases/latest "https://github.com/protocolbuffers/protobuf/releases/latest")
   * download the appropriate file for your system, for me it was [protoc-3.11.4-win64.zip](https://github.com/protocolbuffers/protobuf/releases/download/v3.11.4/protoc-3.11.4-win64.zip)
   * Extract it
   * Place the exe from the bin folder in a folder you want
     * I put mine in C:/tools/protoc
2. Add that exe location to your SYSTEM PATH
   * System Properties -> Advanced -> Environment Variables ->System Variables
   * Find PATH under System Variables and select it
   * Click Edit
   * Add path of exe to this list
3. Create an Angular App
   * [https://cli.angular.io/](https://cli.angular.io/ "https://cli.angular.io/")
4. Install NPM Packages for Angular App
   * `npm i --save ts-protoc-gen`
   * `npm i --save google-protobuf`
   * `npm i --save-dev @types/google-protobuf`
   * `npm i --save @improbable-eng/grpc-web`
5. Create a proto file in your app directory
   1. app/protos/person.proto

   syntax = "proto3";
   message Person {
   required string name = 1;
   required int32 id = 2;
   optional string email = 3;
   }
6. Create a empty app/generated folder
7. Run protoc in PowerShell to generate client files

    protoc --plugin=protoc-gen-ts=".\node_modules\.bin\protoc-gen-ts.cmd" --js_out="import_style=commonjs,binary:./"  --ts_out="service=grpc-web:./" src/app/protos/person.proto

### References:

[https://anthonygiretti.com/2020/03/29/grpc-asp-net-core-3-1-how-to-create-a-grpc-web-client-examples-with-angular-8-and-httpclient/](https://anthonygiretti.com/2020/03/29/grpc-asp-net-core-3-1-how-to-create-a-grpc-web-client-examples-with-angular-8-and-httpclient/ "https://anthonygiretti.com/2020/03/29/grpc-asp-net-core-3-1-how-to-create-a-grpc-web-client-examples-with-angular-8-and-httpclient/")