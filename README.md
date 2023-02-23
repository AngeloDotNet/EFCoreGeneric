# EFCore Generic Library V3

If you like this repository, please drop a :star: on <a href="https://bit.ly/3m1cgEe">Github</a>!


## Installation

The library is available on <a href="https://bit.ly/3xKgkvc">NuGet</a> or run the following command in the .NET CLI:

```bash
dotnet add package EFCoreGeneric
```


## Example class implements methods

```csharp
namespace MyNet6Project;

public class MyService : IMyService
{
    private readonly IUnitOfWork<MyEntity, int> unitOfWork;

    public MyService(IUnitOfWork<MyEntity, int> unitOfWork)
    {
        this.unitOfWork = unitOfWork;
    }

    public async Task<List<MyEntity>> GetListItemAsync()
    {
        var listItem = await unitOfWork.ReadOnly.GetAllAsync();
        return listItem;
    }

    public async Task<MyEntity> GetItemAsync(int id)
    {
        var item = await unitOfWork.ReadOnly.GetByIdAsync(id);
        return item;
    }

    public async Task CreateItemAsync(MyEntity item)
    {
        await unitOfWork.Command.CreateAsync(item);
    }

    public async Task UpdateItemAsync(MyEntity item)
    {
        await unitOfWork.Command.UpdateAsync(item);
    }

    public async Task DeleteItemAsync(MyEntity item)
    {
        await unitOfWork.Command.DeleteAsync(item);
    }
}
```


## Registering services at Startup

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddScoped<DbContext, DataDbContext>();
    services.AddScoped(typeof(IUnitOfWork<,>), typeof(UnitOfWork<,>));
    services.AddScoped(typeof(IDatabaseRepository<,>), typeof(DatabaseRepository<,>));
    services.AddScoped(typeof(ICommandRepository<,>), typeof(CommandRepository<,>));
}
```


## Contributing

Contributions and/or suggestions are always welcome.
