---
title:  "Razor Pages Url tt File"
excerpt: "I've loved the speed I'm able to code out page redirects and any kind of partial or layout references."
header:
  teaser: /assets/posts/razor-pages-url-tt-file/header.jpg
categories: 
  - Software-Development
tags:
  - ASP.NET Core
  - Razor Pages
comments: true
---

![header](/assets/posts/razor-pages-url-tt-file/header.jpg)

## Introduction

I've been working on a new site and have gone from using feature folders and the MVC pattern to using ASP.NET Core 2.0 Razor Pages with the MVVM pattern it is based on. Going from MVC to Razor pages has been a fun experience. But one of the learning experiences I've faced was what was the best way to reference pages in my code for redirects or anything else.

I created a SitePages.tt file in my ASP.NET Core 2 site using Razor Pages to scan the /Pages folder and output a class with string properties to get IntelliSense. I've loved the speed I'm able to code out page redirects and any kind of partial or layout references. I have Resharper, but there is no good solution right now for Razor Pages. So I feel like my solution works great for me!

## Prerequisites

* ASP.NET Core 2.0 or later
* Visual Studio 15.3 or later

See [Introduction to Razor Pages in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/mvc/razor-pages/?tabs=visual-studio) for much more great information on getting started with Razor Pages if you haven't already.

## Steps

1. Create an ASP.NET Core 2.0 Web Application

    I'm targeting .NET 4.6.1 but you can use whatever .NET flavor you'd like! Just make sure you're targeting ASP.NET Core **2.0** or higher.

    ![new project dialog]({% asset_path newproject.jpg %})

2. Add a SitePages.tt file to the root of your website project.

    I had a little trouble finding a template file from the add new item menu but I just use the [Add New File](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.AddNewFile) extension by Mads Kristensen. Either way. Once you have your tt file added to your project, just paste the content shown below and you should be in business.

## SitePages tt file

```csharp
<#@ template language="C#" hostSpecific="true" debug="True" #>
<#@ output extension="cs" #>
<#@ assembly name="System.Core" #>
<#@ assembly name="EnvDte" #>
<#@ import namespace="System.Linq" #>
<#@ import namespace="System.IO" #>
<#@ import namespace="System.Collections.Generic" #>
<#@ import namespace="System.Text.RegularExpressions" #>
<#@ import namespace="System" #>
<#
  var visualStudio = (this.Host as IServiceProvider).GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE;
  var project = visualStudio.Solution.FindProjectItem(this.Host.TemplateFile).ContainingProject as EnvDTE.Project;

  string root = Host.ResolvePath("");
  var projectItems = GetProjectItemsRecursively(project.ProjectItems);
#>
namespace <#=System.Runtime.Remoting.Messaging.CallContext.LogicalGetData("NamespaceHint")#>
{
	public static class SitePages
	{
<#ListPages("/Pages", "cshtml", projectItems);#>

	}
}

<#+
	public void ListPages(string path, string fileType, List<string> projectItems)
	{
		var root = Host.ResolvePath("");
		
		var fileNames = Directory.EnumerateFiles(root + path, "*." + fileType, SearchOption.AllDirectories)
			.Select(x => x.Replace("\\", "/"))
			.Where(x => projectItems.Any(p => p.Equals(x, StringComparison.OrdinalIgnoreCase)))
			.Select(x => x.Substring(root.Length))
			.Select(x => x.Replace("/Pages/", ""))
			.Select(x => x.Replace(".cshtml", ""))
			.OrderBy(x => x)
			.ToList();

		foreach(string fileName in fileNames)
		{
			if (fileName.Contains("_"))
				WriteLine("\t\tpublic static string " + fileName.Replace("/", "") + " => @\"" + fileName + "\";");
			else
				WriteLine("\t\tpublic static string " + fileName.Replace("/", "") + " => @\"/" + fileName + "\";");
		}
	}

	public List<string> GetProjectItemsRecursively(EnvDTE.ProjectItems items)
	{
		var ret = new List<string>();
		if (items == null) return ret;

		foreach(EnvDTE.ProjectItem item in items)
		{
			string result = item.FileNames[1].Replace("\\", "/");
			
			// If not folder.
			if (result[result.Length - 1] != '\\')
			{
				ret.Add(result);
			}
						
			ret.AddRange(GetProjectItemsRecursively(item.ProjectItems));
		}

		return ret;
	}
#>
```

My tt file is based on a gist <https://gist.github.com/niaher/bfa87f0aeda1204091fe>.

## Using Your Shiny New Toy

Alright. Now you should be able to see the generated .cs file with all of your .cshtml files represented as class properties of the SitePages.cs class.

Here are some examples of how I'm using it.

In a view
```html
<cancel-button asp-page="@SitePages.DashboardIndex"></cancel-button>
```

In my Page Model http handlers
```csharp
public async Task<IActionResult> OnPostAsync()
{
    await _mediator.Send(command);
    return RedirectToPage(SitePages.DashboardIndex);
}
```

If you add a new page, just right click your SitePages.tt file and click "Run Custom Tool". This will generate out your new site page property.

## Final Notes

I hope you enjoy this little tt file helper for your Razor Pages projects. I threw the tt file together pretty quickly and so if you've got any suggestions etc.. best way to give feedback or chat would be via Twitter @KurtDowswell.

## References

* <https://gist.github.com/niaher/bfa87f0aeda1204091fe>
* <https://docs.microsoft.com/en-us/aspnet/core/mvc/razor-pages/?tabs=visual-studio>
