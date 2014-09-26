---
layout: post
title: One OData Endpoint for multiple databases with the same schema
tags: OData WebApi EntityFramework Unity DependencyInjection
---

##Introduction
---
As stated on[OData's Website](http://www.odata.org),
 
In the .NET world, you can easily expose your database data using OData, Web Api and Entity Framework. There are many tutorials about this on [Microsoft's site](http://www.asp.net). Unfortunately, all the tutorials I found were exposing data from only one database. Usually, you end up having an OData endpoint with a Url like this:
http://servername/OData/EntityName

What I wanted to achieve was to have one endpoint for more databases with the same schema. So the goal was to finally have a Url like this:

http://servername/OData/**DatabaseName**/EntityName


##Implementation
---

I will start by saying that you can find the complete sample code on [**Github**](https://github.com/dimitrispaxinos/OData.MultipleDatabaseEndpoint).  Our requirement is to create an endpoint in order to expose the Products of a business. This business has two stores, one in Hamburg and one in Berlin with two different identical databases and we would like to be able to query the Products of both databases using the same endpoint:

*http://servername/OData/hamburg/Products*

*http://servername/OData/berlin/Products*

The endpoint was created using Web API and Entity Framework as an ORM. You can definately modify the code accordingly in case you would like to use the ORM of your choice. I also used Unity as an IOC container since dependency injection is quite crutial in this scenario. 

I will focus on and go through the two most critical points of the implementation that have to do with:

- Providing the right connection string to Entity Framwork
- Handling the provided Url, extracting the store location and routing it accordingly.
- Unity and Object Lifetime 



###Connection String
Our Entity Framework Context class looks like this

```csharp
public class ProductsContext : DbContext
{
	public ProductsContext()
		: base("name=HamburgDB")
	{

	}

	public ProductsContext(string connectionString)
		: base(connectionString)	
	{

	}

	public DbSet<Product> Products { get; set; }
}
```

and is directly used by the controller in order to do all the queries. So, the information about the  connection string has to be passed to the controller and subsequently to the EF context. In order to do that, we create the following interface which is responsible for retrieving the right connection string:  

```csharp
public interface IConnectionStringProvider
{
	string GetConnectionString();
}
```
An instance of an implementation of the above interface will be injected into the constructor of the controller every time it is instantiated using Unity. The provided connection string will be subsequently passed to the constructor of the EF context:


```csharp
public class ProductsController : ApiController
{
	private readonly ProductsContext _db;

    public ProductsController(IConnectionStringProvider connectionStringProvider)
    {
    	_db = new ProductsContext(connectionStringProvider.GetConnectionString());
    }
}
```
We just saw how the connection string gets into the constructor of the EF context. Following the interface segregation principle and in order to set the connection string, we will use one more interface, the IConnectionStringSetter which inherits from the IConnectionStringProvider:

```csharp
public interface IConnectionStringSetter: IDatabasePicker
{
	void SetConnectionString(string storeName);
}
```

A simple implementation of IConnectionStringSetter can look like this:

```csharp
public class ConnectionStringSetter : IConnectionStringSetter 
{
	public string StoreName { get; private set; }

	public void SetConnectionString(string storeName)
	{
		StoreName = storeName;
	}

	public string GetConnectionString()
	{
		return StoreName;
	}
}
```
You can of course adjust the methods according to the way you set and retrieve the connection string, add validations etc.



###Routing
We saw earlier that our goal is to have a Url that looks like this:
http://servername/OData/**DatabaseName**/EntityName

which means that we have to somehow access to the Url before OData does, extract our information we need in order to get the right database and restore the original path structure:

http://servername/OData/EntityName

This can be achieved by creating our own path handler class. This class inherits from the **DefaultODataPathHandler** class, gets an IConnectionStringSetter  object injected into his constructor:

```csharp
public class CustomDataPathHandler : DefaultODataPathHandler
{
	private readonly IConnectionStringSetter _connectionStringSetter;

    public CustomDataPathHandler(IConnectionStringSetter connectionStringSetter)
    {
	    _connectionStringSetter = connectionStringSetter;
    }

    public override ODataPath Parse(IEdmModel model, string odataPath)
    {
	    if (!odataPath.StartsWith("$") && odataPath.IndexOf("/") > 0)
        {
	        storeName = odataPath.Substring(0, odataPath.IndexOf("/"));
            var entityPath = odataPath.Substring(odataPath.IndexOf("/") + 1);
            _connectionStringSetter.SetConnectionString(storeName + "DB");
            odataPath = entityPath;
        }

        return base.Parse(model, odataPath);
    }
}
```

Now that we created our custom path handler, we have to register it when declaring our OData route inside the "Register" method of the static WebApiConfig class:

```csharp
 config.Routes.MapODataRoute(
        routeName: "odata",
        routePrefix: "odata",
        model: builder.GetEdmModel(),
        pathHandler: UnityConfig.UnityContainer.Resolve<CustomDataPathHandler>(),
        routingConventions: ODataRoutingConventions.CreateDefault());
```

As you can see, we use Unity to resolve our instance of CustomDataPathHandler because we need an IConnectionStringSetter object to be injected into it.

###Unity Registration

The last point to note is that we need to have the same object of IConnectionStringSetter and IConnectionStringProvider used by our handler and then passed to our controller. To achieve this, we register the same instance for these both interfaces in the RegisterComponents method of the the static UnityConfig class:

```csharp
var databaseSetter = new DatabaseSetter.ConnectionStringSetter();
UnityContainer.RegisterInstance<IConnectionStringSetter>(databaseSetter);            UnityContainer.RegisterInstance<IConnectionStringProvider>(databaseSetter);
UnityContainer.RegisterType<CustomDataPathHandler>();
```
