# osx-config C# Web App Enviroment

---

## Install MS SQL Server on Docker
To install MS SQL Server on Docker, follow: [Instruction](https://builtin.com/software-engineering-perspectives/sql-server-management-studio-mac)

### To get your password, 2 steps:
First, run      
```
docker ps
```
to get your container's name.

Then,     
```
docker inspect -f '{{range .Config.Env}}{{println .}}{{end}}' container_name
```
You can find your password after SA_PASSWORD.

---
## Download the IDE: JetBrains Rider 
[Download Here](https://www.jetbrains.com/rider/download/#section=mac)

### Create a New solution
use Web App(MVC) template

### Add dependencies:   
entityCore.Design, entityCore.Tools, entityCore.SqlServer     (Right click the solution -> Manage NuGet Package)  
select version 7.0.20 to align with the .Net version

---

## Configue .Net environment
Download .Net 7 from [Download here](https://download.visualstudio.microsoft.com/download/pr/ff89348c-045e-4fdc-bd6c-31b6d3940420/7f6cb1235b86ee021a6186fbd8542a1e/dotnet-sdk-7.0.410-osx-arm64.pkg)

### Add environment variables: 
```
vim ~/.zshrc
```
Add:

```
export DOTNET_ROOT=$HOME/.dotnet
export PATH=$PATH:$HOME/.dotnet:$HOME/.dotnet/tools
```
to the end of the file.

### Reload the resource file
```
source ~/.zshrc
```

### Check your dotnet version
```
dotnet --version
```

### Install dotnet ef
```
dotnet tool install --global dotnet-ef --version 7.0.20
```

### Add environment variables:  
```
vim ~/.zshrc
```
Add:
```
export PATH="$PATH:$HOME/.dotnet/tools"
```
to the end of the file.   
### Reload the resource file
```
source ~/.zshrc
```
### Check your dotnet ef version
```
dotnet ef --version
```

---

## Migration
### After have a model class
Run the migration under Tools -> Entity Framework Core - > Add Migration

---

## Update Database
To Update Database, first open appsettings.json
Here, StudentProject is the solution name.
```
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*",
  "ConnectionStrings": {
    "StudentProjectContext": "Data Source=localhost,1433;Initial Catalog=YOUR DATABASE NAME;User ID=sa;Password=YOUR PWD;TrustServerCertificate=True;MultipleActiveResultSets=true;"
  }
}
```

Before run, check the Program.cs, check 
```c#
builder.Services.AddDbContext<StudentProjectContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("StudentProjectContext") ?? throw new InvalidOperationException("Connection string 'StudentProjectContext' not found.")));
```
Make sure options.UseSqlServer instead of UseSqlite

Run the migration under Tools -> Entity Framework Core - > Update Database   

And check your database to see whether the table is created successfully.


