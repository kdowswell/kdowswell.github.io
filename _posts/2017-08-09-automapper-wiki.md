---
title:  "AutoMapper Wiki"
excerpt: "Reference page for tips, tricks, and best practices I've found."
header:
  teaser: "/assets/posts/2017-08-09-automapper-wiki/header.jpg"
categories: 
  - Software-Development
tags:
  - AutoMapper
  - CSharp
comments: true
---

![header](/assets/posts/2017-08-09-automapper-wiki/header.jpg)

## Introduction

I am creating this post as a reference for myself and others that find it useful for things I found while using the [AutoMapper](https://github.com/AutoMapper/AutoMapper) library. I will continue to grow this list as reference page for tips, tricks, and best practices I've found.

## IgnoreAllNonExisting

This statement is one that I put on all of my mapping profiles to ensure that you don't set values for properties that do not match your "From" object.

```
Mapper.CreateMap<FromObjectName, ToObjectName>()
    .IgnoreAllNonExisting();
```

## Conditional

I've seen some mapper profiles get very confused with the conditionals. This format helps keep it readable.

```
Mapper.CreateMap<FromObjectName, ToObjectName>()
    .ForMember(m => m.MyPropertyName, o =>
    {
        o.Condition(s => s.MyPropertyToCheck == 1); 
        o.MapFrom(s => DoSomethingToProperty(s.MyPropertyName));
    });
```

