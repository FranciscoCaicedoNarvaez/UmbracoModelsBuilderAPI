# Umbraco Models Builder API
## Create strongly typed models in Umbraco.ModelsBuilder.Api

When Models Builder is enabled and users in UAT and Production environments have access to it, they are able to generate the models at any time, there is a high risk of breaking the website if properties in document types are updated. To prevent this from happening I decided to explain how to use and integrate the Umbraco.ModelsBuilder.API 
More about Builder modes can be found [here](https://our.umbraco.com/documentation/Reference/Templating/Modelsbuilder/Builder-Modes).

Using API models will allow to generate the models in a dev environment only, and then compiled to a dll. It is a good practice to generate models outside the Umbraco project in a separate Class Library.

The following steps show how to use the API models in a vanilla Umbraco 8 installation.

## Install Umbraco.ModelsBuilder.Api from NuGet

![image](https://user-images.githubusercontent.com/8690373/54001428-06b67a00-4197-11e9-9ced-9bb4addf5f41.png)

Alternatively, run the following command in the Package manager console:

```C#
PM> Install-Package Umbraco.ModelsBuilder.Api
```

## Make sure the web.config file contains the following keys and values
```xml
<add key="Umbraco.ModelsBuilder.EnableApi" value="true" />
<add key="Umbraco.ModelsBuilder.Enable" value="true" />
<add key="Umbraco.ModelsBuilder.ModelsMode" value="Nothing" />
```

## Download Umbraco Models Builder Custom Tool

In *Visual Studio -> Tools -> Extensions and features -> Online* and install **ModelsBuilder Custom Tool**

![image](https://user-images.githubusercontent.com/8690373/54001444-16ce5980-4197-11e9-991f-75b5bd7b136e.png)

## Configure Custom Tool

In *Visual Studio -> Tools -> Options -> Umbraco* type the back office login details

![image](https://user-images.githubusercontent.com/8690373/54001476-2e0d4700-4197-11e9-9f0d-960f5e348a25.png)

## Create a Class library for the models

Create a new class library project where the Umbraco models are going to be generated. For this example the Class library name is called **Umbraco.Web.PublishedModels.ContentModels**

In the new class library create an empty class called *builder.cs*, then in its properties, reference the Custom Tool as *UmbracoModelsBuilder*.

![image](https://user-images.githubusercontent.com/8690373/54001489-38c7dc00-4197-11e9-9b6f-3df70d74831c.png)

## Run Custom Tool

Right click on the *builder.cs* class and choose Run Custom Tool. This will generate the models of the Umbraco application.

![image](https://user-images.githubusercontent.com/8690373/54001509-454c3480-4197-11e9-9ee7-c3162eddfeca.png)

Models will show as children on the builder class

![image](https://user-images.githubusercontent.com/8690373/54001519-4e3d0600-4197-11e9-8cdd-9873361b8c24.png)

## Add project dependency

Last step is to add the class library to the project dependencies. In this way the compiled models can be accessible in the Umbraco application. This will copy the dll to the Umbraco’s bin directory **Umbraco.Web.PublishedModels.ContentModels.dll**

![image](https://user-images.githubusercontent.com/8690373/54001550-5a28c800-4197-11e9-9d16-c6fb5b15bc85.png)

## Umbraco Backoffice settings

When we login to the Backoffice in dev environment. Go to *Settings -> Models Builder*. We notice models cannot be generated in this page but the API is enabled. Therefore we are able to generate the models in the class library.

![image](https://user-images.githubusercontent.com/8690373/54001565-644ac680-4197-11e9-92fc-801838f34bc0.png)

On the contrary, in UAT and production environments the API is disabled and models cannot be generated.

![image](https://user-images.githubusercontent.com/8690373/54001574-6e6cc500-4197-11e9-9f98-54c08672b3df.png)

Now, we have reduced the risk of breaking the website when users update document type properties.


# Source code

Class library source code can be downloaded re-used in other Umbraco 8 projects. Make sure the Custom Tool is installed and configured in Visual studio. 

Generated models have been left in source code for reference only. Delete the models and generate the ones for your project.



