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
2. Add exe from download to SYSTEM PATH

   I placed mine in c:/tools/protoc
   * 
3. Create an Angular App
   * [https://cli.angular.io/](https://cli.angular.io/ "https://cli.angular.io/")
4. Install NPM Packages for Angular App
   * `npm i --save ts-protoc-gen`
   * `npm i --save google-protobuf`
   * `npm i --save-dev @types/google-protobuf`
   * `npm i --save @improbable-eng/grpc-web`