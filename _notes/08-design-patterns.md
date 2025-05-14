# Design Patterns

- A collection of general reusable solutions to common problems in software design.
- These patterns are already tested and proven to work.
- They make the code more readable and maintainable.
- Patterns are micro-architectural solutions.
- They allow the collaborators to be more familiar with the code.

## Factory Pattern

- A creational pattern that provides a way to create objects without specifying the exact class of object that will be created.

```C#
public enum Continent
{
    Europe,
    Asia,
    America,
    Africa,
    Oceania,
    Antarctica
}

public interface IWeatherProvider
{
    string GetWeather();
}

public class EuropeWeather : IWeatherProvider
{
    public string GetWeather()
    {
        return "Weather in Europe";
    }
}

public class AsiaWeather : IWeatherProvider
{
    public string GetWeather()
    {
        return "Weather in Asia";
    }
}

public class AmericaWeather : IWeatherProvider
{
    public string GetWeather()
    {
        return "Weather in America";
    }
}

public class AfricaWeather : IWeatherProvider
{
    public string GetWeather()
    {
        return "Weather in Africa";
    }
}

public class OceaniaWeather : IWeatherProvider
{
    public string GetWeather()
    {
        return "Weather in Oceania";
    }
}

public class AntarcticaWeather : IWeatherProvider
{
    public string GetWeather()
    {
        return "Weather in Antarctica";
    }
}

public IWeatherProvider GetWeatherProvider(Continent continent)
{
    switch (continent)
    {
        case Continent.Europe:
            return new EuropeWeather();
        case Continent.Asia:
            return new AsiaWeather();
        case Continent.America:
            return new AmericaWeather();
        case Continent.Africa:
            return new AfricaWeather();
        case Continent.Oceania:
            return new OceaniaWeather();
        case Continent.Antarctica:
            return new AntarcticaWeather();
        default:
            throw new ArgumentException("Invalid continent");
    }
}
```

- There's a popular saying about the new keyword and it's that `new` is glue, because it mixes class instantiation and code logic leading to strong coupling, something prone to errors, because if you need to change the class name, you have to change it in multiple places and that can lead to bugs.
- The factory pattern is a way to avoid this problem, by creating a factory class that will handle the instantiation of the objects.
- This is a very important pattern because is the base for others like the repository pattern.

## Repository Pattern

- A pattern that provides a way to access data from a data source without exposing the details of the data source.
- Its similar to the DAL (Data Access Layer)

```C#
public interface IRepository<T>
{
    void Add(T entity);
    void Update(T entity);
    void Delete(T entity);
    T GetById(int id);
    IEnumerable<T> GetAll();
}

public class Repository<T> : IRepository<T>
{
    private readonly DbContext _context;
    private readonly DbSet<T> _dbSet;

    public Repository(DbContext context)
    {
        _context = context;
        _dbSet = context.Set<T>();
    }

    public void Add(T entity)
    {
        _dbSet.Add(entity);
        _context.SaveChanges();
    }

    public void Update(T entity)
    {
        _dbSet.Update(entity);
        _context.SaveChanges();
    }

    public void Delete(int id)
    {
        _dbSet.Remove(id);
        _context.SaveChanges();
    }

    public T GetById(int id)
    {
        return _dbSet.Find(id);
    }

    public IEnumerable<T> GetAll()
    {
        return _dbSet.ToList();
    }
}

public class UserRepository : Repository<User>
{
    public UserRepository(DbContext context) : base(context)
    {
    }

    public IEnumerable<User> GetUsersByAge(int age)
    {
        return _dbSet.Where(u => u.Age == age).ToList();
    }
}
```

- It's one of the most used patterns in .NET Core applications since it allows us to separate the data access logic from the business logic.

## Façade Pattern

- A structural pattern that provides a simplified interface to a complex system.

```C#
public class MoneyTransfer
{
    public bool CheckAccountExist(int accountNum) { . . . }
    public bool HasEnoughMoney(int accountNum, double amount) { . . . }
    public bool WithdrawMoney(int accountNum, double amount) { . . . }
    public bool DepositMoney(int accountNum, double amount) { . . . }
    public bool WriteLog(int accountNum, string message) { . . . }
}

// Here the Façade implementation just exposes the methods that are needed to transfer money preventing
public bool TransferMoney(int accountFrom, int accountTo, double sum)
{
    if (!CheckAccountExist(accountFrom) || !CheckAccountExist(accountTo)) || !HasEnoughMoney(accountFrom, sum)
    {
        return false;
    }

    WithdrawMoney(accountFrom, sum);

    DepositMoney(accountTo, sum);

    WriteLog(accountFrom, $"Withdraw {sum} from account {accountFrom}");
    WriteLog(accountTo, $"Deposit {sum} to account {accountTo}");

    return true;
}
```

## Command Pattern

- A behavioral pattern that encapsulates a request as an object, it separates the sender of a request from the receiver of the request.

```C#
interface ICommand
{
    void Execute();
}

class DeleteWordCommand : ICommand
{
    private readonly Document _document; // This is the receiver
    private readonly string _word;

    public DeleteWordCommand(Document document, string word)
    {
        _document = document;
        _word = word;
    }

    public void Execute()
    {
        _document.DeleteWord(_word);
    }
}

class ChangeWordCommand : ICommand
{
    private readonly Document _document;
    private readonly string _oldWord;
    private readonly string _newWord;

    public ChangeWordCommand(Document document, string oldWord, string newWord)
    {
        _document = document;
        _oldWord = oldWord;
        _newWord = newWord;
    }

    public void Execute()
    {
        _document.ChangeWord(_oldWord, _newWord);
    }
}

class Undo // Invoker
{
    Queue<ICommand> undos;

    void AddUndo(ICommand undo)
    {
        undos.Enqueue(undo);
    }

    void PerformUndo()
    {
        undos.Dequeue().Execute();
    }
}
```

## Conclusion

- It's often a mistake to create a heavily design pattern oriented architecture, which can lead to over-engineering and complexity.
- Use only the patterns that you need and that make sense for your application.
