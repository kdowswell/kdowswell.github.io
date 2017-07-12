---
title:  "ASP.NET Core MVC Feature Folders"
header:
categories: 
  - Software-Development
tags:
  - ASP.NET
---

![header](/assets/posts/2017-07-11-asp-net-core-mvc-feature-folders/header.jpg)

The default ASP.NET Core MVC project templates generate a project template with Models, Views, and Controllers all separated into their respective folders. This default MVC structure can be difficult to maintain when project sizes get large and you've been maintaining your website for an extended period of time.

To help with this issue, the concept of Feature Folders allows you to group your Models, Views, and Controllers all together. This aligns with the concepts of how modern Agile software development teams deliver software in short Sprints targeting specific features for development tasks.

Let's jump into an example converting the default template to use feature folders!

## Example

### Prerequisites

* Visual Studio 2017 (15.2)

### Step 1 - Create a New Project

1. File -> New Project.
2. Choose ASP.NET Core Web Application using the full .NET framework.
3. Provide project name and location.
![create project 1](/assets/posts/2017-07-11-asp-net-core-mvc-feature-folders/CreateProj1.jpg)
4. Continue to next step.
5. Choose Web Application with no authentication.
![create project 2](/assets/posts/2017-07-11-asp-net-core-mvc-feature-folders/CreateProj2.jpg)

Your project should look like this:

![project 1](/assets/posts/2017-07-11-asp-net-core-mvc-feature-folders/Project1.jpg)

### Step 2 - Add feature Infrastructure Files!

In your web app, add the following files. I put mine in a Infrastructure/FeatureFolders/ folder

```
public class FeatureViewLocationExpander : IViewLocationExpander
{
    public void PopulateValues(ViewLocationExpanderContext context)
    {

    }

    public IEnumerable<string> ExpandViewLocations(
        ViewLocationExpanderContext context,
        IEnumerable<string> viewLocations)
    {
        if (context == null)
        {
            throw new ArgumentNullException(nameof(context));
        }
        if (viewLocations == null)
        {
            throw new ArgumentNullException(nameof(viewLocations));
        }

        // {0} - Action Name
        // {1} - Controller Name
        // {2} - Area name

        //Features
        yield return "/Features/{1}/{0}.cshtml";
        yield return "/Features/{1}/Views/{0}.cshtml";

        //Feature Features
        yield return "/Features/{2}/{1}/{0}.cshtml";
        yield return "/Features/{2}/{1}/Views/{0}.cshtml";
        yield return "/Features/{2}/Shared/{0}.cshtml";

        //Shared
        yield return "/Features/Shared/{0}.cshtml";
    }
}
```

```
public static class ServiceCollectionExtensions
{
    public static IMvcBuilder AddFeatureFolders(this IMvcBuilder services)
    {
        if (services == null)
        {
            throw new ArgumentNullException(nameof(services));
        }

        services.AddRazorOptions(o =>
        {
            o.ViewLocationExpanders.Add(new FeatureViewLocationExpander());
        });

        return services;
    }
}
```

### Step 3 - Alter Startup.cs to Use Feature Folders

In Startup.cs, simply chain the call like below to indicate to MVC to expand it's view search to the folders indicated in the FeatureViewLocationExpander class.

```
services.AddMvc().AddFeatureFolders();
```

### Step 4 - Refactor Site Files Into Feature Folders

Now Simply add a "Features" folder at the root of your web app. Then move files from the generated site template into appropriate folders.

![project 2](/assets/posts/2017-07-11-asp-net-core-mvc-feature-folders/Project2.jpg)

In this example I've used the controller name as the view name. doing this you must specify the view returned from the Index action

```
public IActionResult Index()
{
    ViewData["Message"] = "Your application description page.";

    return View("About");
}
```

There might be a better way of doing this but for now this is how I like doing it.

Note: if you use Resharper, it doesn't recognize these views in the Features folders. So you have to do one additional step to get Resharper intillisense for the views. Add AssemblyAttributes.cs to the root of your project with the following:

```
using JetBrains.Annotations;

//Note: These are the possible assembly annotations for finding views
//AspMvcAreaMasterLocationFormatAttribute
//AspMvcAreaPartialViewLocationFormatAttribute
//AspMvcAreaViewLocationFormatAttribute
//AspMvcMasterLocationFormatAttribute
//AspMvcPartialViewLocationFormatAttribute
//AspMvcViewLocationFormatAttribute

[assembly: AspMvcViewLocationFormat(@"~\Features\{1}\{0}.cshtml")]
[assembly: AspMvcViewLocationFormat(@"~\Features\{1}/Views/{0}.cshtml")]

[assembly: AspMvcAreaViewLocationFormat(@"~\Features\{2}\{1}\{0}.cshtml")]
[assembly: AspMvcAreaViewLocationFormat(@"~\Features\{2}\{1}\Views\{0}.cshtml")]
[assembly: AspMvcAreaViewLocationFormat(@"~\Features\{2}\Shared\{0}.cshtml")]

[assembly: AspMvcViewLocationFormat(@"~\Features\Shared\{0}.cshtml")]

[assembly: AspMvcAreaMasterLocationFormat(@"~\Features\{2}")]
```

### GitHub Repo
To view the full source code from this post please visit <https://github.com/kdowswell/asp-net-core-mvc-feature-folders>.

## Summary
So now you are all set up to begin using feature folders in your own web app. This is a very basic example. But it allows for a much better coding experience and organization structure as your project sizes grow.

If this post helped you please share via the social media links below. Thanks!

## Tools
Since this post is on folders and files. A **must have** extension you should get is [Add New File](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.AddNewFile). This extension saves me tons of time. And overall it's just a better experience than using the built in Visual Studio "New Item" process. I use it to create folders and files all day while using VS.

## Additional Resources



