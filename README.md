# Example
```cs
// This class must be sealed.
sealed class PlayerData {
    public string CustomData = "Hello World";
}

sealed class Program {
    private readonly WeakTable<Player, PlayerData> players
               = new WeakTable<Player, PlayerData>(_ => new PlayerData());

    public void Test(Player p) {
        var pData = players[p];

        Assert.AreEqual("Hello World", pData.CustomData);

        pData.CustomData = "Another Medium";

        Assert.AreEqual("Another Medium", pData.CustomData);
        Assert.AreEqual(players[p].CustomData, pData.CustomData);
    }
}
```

# Avoiding memory leaks
Before using WeakTables, it's important to know how to avoid memory leaks. It's pretty simple.

A type is memory-safe if all of its fields are [integrals](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/integral-numeric-types), [floats](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types), `string`s, `char`s, `bool`s, enums, pointers, or structs/sealed classes that are also memory-safe.

If a type isn't memory-safe, wrap it in `WeakRef<T>`. For example, instead of `object`, use `WeakRef<object>`:

```cs
sealed class Data {
    public WeakRef<object> SomeObject 
     = new WeakRef<object>(new object());
}
```

With that in mind, you're ready to use WeakTables.

# How to integrate into your project
Simply add the source to your project. There are a few ways.
- Git submodule: Run `git submodule add https://github.com/Dual-Iron/weak-tables lib/weak-tables` in your working tree
- Git clone: Clone or fork this repository into a new folder in your project.
- Manual: Drop the [source code](https://github.com/Dual-Iron/weak-tables/archive/refs/heads/master.zip) into a new folder in your project.

If you can't compile the code because your language version is C# 7.3 and not 8.0, you can upgrade easily using [this tool](https://github.com/Dual-Iron/ProjectUpgrader/releases/latest).

After that, you're good to go. Enjoy!
