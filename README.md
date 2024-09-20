# osx-config

Download the IDE: JetBrains Rider   

Add dependencies: entityCore.Design, entityCore.Tools, entityCore.SqlServer       
version 7.0.20 align with the .Net version

To install MS SQL Server on Docker, refer: [Here](https://builtin.com/software-engineering-perspectives/sql-server-management-studio-mac)

To get your password, 
```
docker ps
```
to get your container's name

Then, 
```
docker inspect -f '{{range .Config.Env}}{{println .}}{{end}}' container_name
```

Download .Net 7 from [Download here](https://download.visualstudio.microsoft.com/download/pr/ff89348c-045e-4fdc-bd6c-31b6d3940420/7f6cb1235b86ee021a6186fbd8542a1e/dotnet-sdk-7.0.410-osx-arm64.pkg)
```
vim ~/.zshrc
```

add environment variables: 
```
export DOTNET_ROOT=$HOME/.dotnet
export PATH=$PATH:$HOME/.dotnet:$HOME/.dotnet/tools
```
to the end of the file.

reload the file
```
source ~/.zshrc
```

check your dotnet version
```
dotnet --version
```

install dotnet ef
```
dotnet tool install --global dotnet-ef --version 7.0.18
```


```
vim ~/.zshrc
```

```
export PATH="$PATH:$HOME/.dotnet/tools"
```

```
source ~/.zshrc
```

```
dotnet ef --version
```


Then do the migration under Tools -> Entity Framework Core - > Add Migration


---

To Update Database, first open appsettings.json
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

before run, check the Program.cs, check 
```c#
builder.Services.AddDbContext<StudentProjectContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("StudentProjectContext") ?? throw new InvalidOperationException("Connection string 'StudentProjectContext' not found.")));
```
make sure options.UseSqlServer


