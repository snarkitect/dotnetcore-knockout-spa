** Project based on http://www.dotnetcurry.com/aspnet/1394/aspnet-core-knockout
1. `dotnet new knockout`
2. `npm install`
3. `dotnet run`

** This portion is from  [Web API Tutorial](https://docs.microsoft.com/en-us/aspnet/core/tutorials/web-api-vsc#add-support-for-entity-framework-core)
4. add Models folder, include EF Context
    * May need extra DbSet for different models?

** This portion is from [Use SQLite instead of InMemory](https://docs.microsoft.com/en-us/ef/core/get-started/netcore/new-db-sqlite)    
5. Add entity framework packages in terminal
    ```
    dotnet add package Microsoft.EntityFrameworkCore.Sqlite
    dotnet add package Microsoft.EntityFrameworkCore.Design
    ``` 
6. Add the ef tool to the .csproj file 
    ```
    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.0" />
    </ItemGroup>
    ```
7. * Startup.cs
    ```
    public void ConfigureServices(IServiceCollection services)
    {   
        //Goes into environment specific folder eg: /Debug/app/TodoList.pdb
        services.AddDbContext<TodoContext>(options => options.UseSqlite("Data Source=TodoList.db"));
        services.AddMvc();
    }
    ```
    * Run `dotnet ef migrations add InitialCreate` to scaffold a migration and create the initial set of tables for the model.
    * Run `dotnet ef database update` to apply the new migration to the database. This command creates the database before applying migrations.
        * If you don't do this, you'll get errors like "SQLite Error 1: 'no such table"

8. NEXT STEPS set up typescript models and crud operations in some sane fashion.
https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Supplying_request_options