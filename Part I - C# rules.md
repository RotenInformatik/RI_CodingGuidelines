# PART I - C# rules

The rules in this part specify how to use the C# programming language.

Note: For compactness, most code examples only adhere to its associated rule, not to all rules.

Note: The styling and formatting in the [Templates](#Templates) section overrules all other code examples.

[TOC]

## Naming

### Language

Always use proper English language for all names.

### Characters

Never...

- ...use any other character than uppercase letters (`A-Z`), lowercase letters (`a-z`), and numbers (`0-9`).
- ...use numbers (`0-9`) at the beginning of names.
- ...use underscores (`_`), except as prefix for private fields.

### Casings

Always use UpperCamelCase with punctuation (e.g. `Company.Product.Something`) for:

- Assembly names
- Namespaces

Always use UpperCamelCase without punctuation (e.g. `GetOrders`) for:

- All type names
- All type members, except private fields
- Type parameters

Always use lowerCamelCase (e.g. `orderTotal`) for:

- Private fields
- Local variables
- Local constants
- Local methods
- Iteration variables
- Constructor parameters
- Method parameters
- Lambda parameters
- Indexer parameters
- Operator parameters

Never...

- ...use all uppercase (e.g. `GETORDERS`).
- ...use all lowercase (e.g. `ordertotal`), except for properly lowerCamelCased identifiers of one word.

### Notations

Never use Hungarian or any other special notation.

Correct:

```c#
string comment = "Test";
```

Incorrect:

```c#
string strComment = "Test";
string str_Comment = "Test";
```

### Meaning

Always choose meaningful names which describe the intention and not type, size, or technical composition.

Correct:

```c#
public Bitmap ConvertToBitmap (byte[] rawData) {...}
```

Incorrect:

```c#
public Bitmap ProcessBytes (byte[] byteArray) {...}
```

Exception: Technical composition can be part of a name if it is part of the intention.

Example:

```c#
public byte[] ConvertToByteArray (string value) {...}

public int ConvertToInt32 (string value) {...}
```

### Negation

Never use negated names.

Correct:

```c#
public bool IsAllowed { get; private set; }
```

Incorrect:

```c#
public bool IsNotAllowed { get; private set; }
```

### Lengths

Always choose names which are expressive enough and never unnecessarily shorten names.

Correct:

```c#
public int GetItemCount (string temporaryFile) {...}
```

Incorrect:

```c#
public int GetItmCnt (string tmpFile) {...}
```

### Abbreviations

#### Well known

Never use abbreviations unless they shorten excessive names *and* are well known.

Correct:

```c#
int itemCount = 12;

Encoding Utf8 { get; set; }
```

Incorrect:

```c#
int itmCnt = 12;

Encoding UnicodeTransformationFormat8 { get; set; }
```

#### Proper casing

Always use proper casing for abbreviations, even for two letter abbreviations.

Correct:

```c#
namespace MyCompany.MyProduct.Utilities.HwAbstraction {...}

Encoding Utf8 { get; set; }
```

Incorrect:

```c#
namespace MyCompany.MyProduct.Utilities.HWAbstraction {...}

Encoding UTF8 { get; set; }
```

Exceptions: The following two letter abbreviations can be use with all uppercases:

* `IO` (I/O, Input/Output)
* `UI` (User Interface)

### Prefixes

#### General

Never use prefixes (e.g. `EMyEnum`, `m_someField`, `CMyClass`), except for cases described below.

#### Interface types

Always prefix the name of an interface with `I`.

Correct:

```c#
public interface IBeamWeapon {...}
```

Incorrect:

```c#
public interface BeamWeapon {...}
```

#### Private fields

Always prefix the name of a private field with `_`.

Correct:

```c#
private int _lockVersion;
```

Incorrect:

```c#
private int lockVersion;
```

#### Type parameters

Always prefix type parameters with `T`.

Always use the name to express what the type parameter is used for.

Correct:

```c#
public class RandomDictionary <TKey, TValue> {...}
```

Incorrect:

```c#
public class RandomDictionary <Key, Value> {...} //not recognizable as a type parameter

public class RandomDictionary <T, U> {...} //what are they used for?
```

Exception: Use just `T` if only one type parameter is used.

Example:

```c#
public class RandomCollection <T> {...}
```

#### Method actions

Always use one of the following prefixes if a methods main action is to deliver an *existing* value:

- `Get`

Always use one of the following prefixes if a methods main action is to *retrieve* or *compute* a value:

- `Retrieve`
- `Determine`
- `Compute`
- `Calculate`

Correct:

```c#
public CompositionState GetCompositionState () {...}

public decimal CalculateCustomerTurnover () {...}
```

Incorrect:

```c#
public CompositionState Composition () {...}

public decimal GetCustomerTurnover () {...}
```

#### Boolean values

Always use one of the following prefixes, using proper casing, for boolean values (members, variables):

- `Is`, `is`
- `Has`, `has`
- `Contains`, `contains`
- `Can`, `can`
- `Should`, `should`
- `Must`, `must`
- `Allows`, `allows`
- `Supports`, `supports`

Correct:

```c#
public bool IsStarted { get; private set;}

public bool CanLogin (string username) {...}

bool hasOrders = true;
```

Incorrect:

```c#
public bool Started { get; private set;}

public bool Loginable (string username) {...}

bool ordered = true;
```

#### Event indications

*See [Events](#Pre/Post indication)*

### Suffixes

#### General

Never use suffixes (e.g. `someText_str`, `MyClassC`), except for cases described below.

#### Base types

Always suffix the name of an abstract type *which provides default interface implementation* with `Base`.

Correct:

```c#
public abstract class DeviceBase : IDevice {...}
```

Incorrect:

```c#
public abstract class Device : IDevice {...}
```

#### Extension types

Always suffix the name of a type which provides extension methods with `Extensions`.

Always use the full name of the extended type, even for interface type extensions.

Never use type aliases, also for well known extended types.

Correct:

```c#
public static class StringExtensions {...}

public static class IServiceProviderExtensions {...}

public static class Int32Extensions {...}
```

Incorrect:

```c#
public static class StringUtilities {...}

public static class ServiceProviderExtensions {...}

public static class IntExtensions {...}
```

#### Attribute types

Always suffix the name of an attribute type with `Attribute`.

Correct:

```c#
public sealed class ExportAttribute : Attribute {...}
```

Incorrect:

```c#
public sealed class Export : Attribute {...}
```

#### Exception types

Always suffix the name of an exception type with `Exception`.

Correct:

```c#
public class TransmissionFailedException : Exception {...}
```

Incorrect:

```c#
public class TransmissionFailed : Exception {...}
```

#### Async methods

Always suffix the name of an async method with `Async`.

Correct:

```c#
public async Task<Response> TransceiveAsync (Request request) {...}
```

Incorrect:

```c#
public async Task<Response> Transceive (Request request) {...}
```

#### Unsafe contexts

Always suffix the name of an unsafe type or member with `Unsafe`.

Never repeat the `Unsafe` suffix in a member if the containing type already uses the `Unsafe` suffix.

Correct:

```c#
public unsafe sealed class MemoryPointerUnsafe {...}

public unsafe byte[] ReadMemoryUnsafe (IntPtr address) {...}
```

Incorrect:

```c#
public unsafe sealed class MemoryPointer {...}

public unsafe byte[] ReadMemory (IntPtr address) {...}
```

#### Computed values

Always use one of the following suffixes, using proper casing, for computed values (members, variables):

- `Count`
- `Sum`
- `Min`
- `Max`
- `Average`
- `Median`

Correct:

```c#
int itemCount = someList.Count;

public double CustomersPerHourAverage { get; set; }
```

Incorrect:

```c#
int items = someList.Count;

public double CustomersPerHour { get; set; }
```

#### Unit values

Always use the corresponding unit suffix, using proper casing, for values with units (members, variables).

Correct:

```c#
public Image DownloadImage (string url, int timeoutMilliseconds) {...}

public int LaserPowerKilowatts { get; set; }
```

Incorrect:

```c#
public Image DownloadImage (string url, int timeout) {...}

public int LaserPower { get; set; }
```

Exception: The unit is provided dynamically, e.g. through an additional property.

Example:

```c#
public double RadiationValue { get; }

public RadiationUnit RadiationUnit { get; }
```

#### UI controls

Always use suffixes for UI controls, using proper casing, which matches the type of the UI control.

Never use prefixes for UI values.

Correct:

```c#
public Label FirstNameLabel { get; set; }

public TextBox FirstNameEdit { get; set; }
```

Incorrect:

```c#
public Label lblFirstName { get; set; }

public TextBox FirstName { get; set; }
```

#### Event indications

*See [Events](#Pre/Post indication)*

### Assemblies

#### Conflicts

Never start an assembly with a conflicting name, e.g. `System`, `Microsoft`, or other well-known names.

Correct:

```c#
MyCompany.MyProduct.Utilities.dll
```

Incorrect:

```c#
System.Utilities.dll
```

#### Schema

Always start an assembly with the company name and the component name before other parts.

Ensure that the entire organization uses the same schema.

Correct:

```c#
MyCompany.MyProduct.Utilities.dll

MyCompany.MyLibrary.Utilities.dll
```

Incorrect:

```c#
Utilities.dll

MyLibrary.Utilities.dll
```

#### Depth

Never use increasing depth of names for assemblies which belong together.

Correct:

```c#
MyCompany.MyProduct.UserInterface.Common.dll
MyCompany.MyProduct.UserInterface.Controls.dll
MyCompany.MyProduct.UserInterface.Views.Common.dll
MyCompany.MyProduct.UserInterface.Views.Customers.dll
MyCompany.MyProduct.UserInterface.Views.Products.dll
```

Incorrect:

```c#
MyCompany.MyProduct.UserInterface.dll
MyCompany.MyProduct.UserInterface.Controls.dll
MyCompany.MyProduct.UserInterface.Views.dll
MyCompany.MyProduct.UserInterface.Views.Customers.dll
MyCompany.MyProduct.UserInterface.Views.Products.dll
```

### Namespaces

#### Conflicts

Never start a namespace with a conflicting name, e.g. `System`, `Microsoft`, or other well-known names.

Correct:

```c#
namespace MyCompany.MyProduct.Utilities {...}
```

Incorrect:

```c#
namespace System.Utilities {...}
```

#### Schema

Always start a namespace with the company name and the component name before other parts.

Ensure that the entire organization uses the same schema.

Correct:

```c#
namespace MyCompany.MyProduct.Utilities {...}

namespace MyCompany.MyLibrary.Utilities {...}
```

Incorrect:

```c#
namespace Utilities {...}

namespace MyLibrary.Utilities {...}
```

### Regions

#### Unambiguousness

Never use the same region name twice on the same level.

Correct:

```c#
#region Instance Properties
...
#endregion

#region Instance Methods
...
#endregion
```

Incorrect:

```c#
#region Instance Members
...
#endregion

#region Instance Members
...
#endregion
```

#### Clarity

Always use simple region names which describe the content of the region but not its behavior or intention.

Correct:

```c#
#region Instance Properties
...
#endregion

#region ICloneable implementation
...
#endregion
```

Incorrect:

```c#
#region Device management stuff, throws InvalidOperationException on error
...
#endregion
```

### Types

#### Unambiguousness

Never use the same name for a type and a namespace.

Correct:

```c#
namespace MyCompany.MyLibrary.Bootstrapping
{
	public sealed class Bootstrapper {...}
}
```

 Incorrect:

```c#
namespace MyCompany.MyLibrary.Bootstrapper
{
	public sealed class Bootstrapper {...}
}
```

#### Clarity

Never use a type name which is already used elsewhere, in well-known libraries, or which is too general.

Correct:

```c#
public sealed class IceCreamDeviceManager {...}

public static class DeveloperConsole {...}
```

 Incorrect:

```c#
public sealed class DeviceManager {...}

public static class Console {...}
```

#### Redundancy

Never repeat the name of a type in its members.

Correct:

```c#
public enum IceCreamMachineState
{
	Off = 0,
	Idle = 1,
	...
}

public sealed class Customer
{
    public int TotalOrderCount { get; }
}
```

Incorrect:

```c#
public enum IceCreamMachineState
{
	IceCreamMachineOff = 0,
	IceCreamMachineIdle = 1,
	...
}

public sealed class Customer
{
    public int CustomerTotalOrderCount { get; }
}
```

### Methods

#### Verb-Object naming

Always use a verb-object pair for method names.

Correct:

```c#
public void ShowWarning (string message) {...}
```

Incorrect:

```c#
public void Warning (string message) {...} //object only

public void Warn (string message) {...} //verb only
```

Exception: A methods intention can be described with only a verb, without an object, in cases where the corresponding type or the usage context acts as the object.

Example:

```c#
//class: LaserBeam
public void Fire () {...}
```

#### Returned value

Always use a name which indicates whether a method has a return value and if it has one, which allows reasonable inference of the returned type.

Correct:

```c#
//class: Application
public static Task BeginTermination () {...}
```

Incorrect:

```c#
//class: Application
public static Task Terminate () {...} //implies immediate termination
```

### Properties, Fields, Constants

#### Object naming

Always use a object for property, field, and constant names.

Correct:

```c#
public int OrderCount { get; }

public int MaxPlayers { get; set; }
```

Incorrect:

```c#
public int GetOrderCount { get; } //implies method by adding a verb

public int GetMaxPlayers { get; set; } //implies getter-only
```

#### Returned type

Always use a name which allows reasonable inference of the returned type.

Correct:

```c#
public int OrderCount { get; set; }
```

Incorrect:

```c#
public int Orders { get; set; } //could imply list of order objects
```

### Events

#### Event naming

Always use an event, something which can happen in the used context, for event names.

Correct:

```c#
public event EventHandler TransmissionError;

public event EventHandler MessageReceived;
```

Incorrect:

```c#
public event EventHandler Error; //not specific enough for the used context

public event EventHandler Message; //a message itself cannot happen, it is just a thing
```

#### Pre/Post indication

Always indicate whether an event is chronologically raised before or after the event it is tied to.

Always use at least one of the following:

* Prefixes (`Before`, `While`, `After`)
* Suffixes as word endings (`...ing`, `...ed`)

Correct:

```c#
public event EventHandler BeforeSending;

public event EventHandler WhileSending;

public event EventHandler AfterSending;

public event EventHandler StateChanging;

public event EventHandler StateChanged;
```

Incorrect:

```c#
public event EventHandler Send; //is this before or after?

public event EventHandler StateChange; //is this before, during, or after?
```

Exception: The context unambiguously defines when an event can be raised.

Example:

```c#
public event EventHandler TransmissionError; //an error is only known after it happened
```

### Variables

#### `foreach` iteration variables

Always use a proper regular variable name for a `foreach` iteration variable.

Correct:

```c#
foreach (var order in customer.Orders)
{
    ...
}
```

Incorrect:

```c#
foreach (var o in customer.Orders)
{
    ...
}
```

#### `for` iteration variables

Always use a proper regular variable name for a `for` iteration variable.

Correct:

```c#
for (int index = 0; index < orders.Count; index++)
{
    ...
}
```

Incorrect:

```c#
for (int i = 0; i < orders.Count; i++)
{
    ...
}
```

## Styling

### Source code files

#### File structure

Always use the following structure in a source code file, in this order:

* File header (optional)
* `extern alias` directives
* `using` directives
* `using static` directives
* `namespace` declaration
* Actual content or type definition respectively (inside `namespace`)

Correct:

```c#
// FILE HEADER

extern alias FooBarV1;
extern alias FooBarV2;

using System;
using System.Collections.Generic;

using static System.Math;

namespace MyCompany.MyProduct.Utilities
{
	public static class StringExtensions {...}
}
```

Incorrect:

```c#
namespace MyCompany.MyProduct.Utilities
{
	using static System.Math;
    
	using System;
	using System.Collections.Generic;
    
    extern alias FooBarV1;
	extern alias FooBarV2;
    
	// FILE HEADER
	// File:    D:\Data\MyProduct\MyCompany.MyProduct.Utilities\StringUtilities.cs
	// Version: 1.1
	// Author:  Joe

	public static class StringUtilities {...}
}
```

#### File header

Always keep file headers consistent accross all source code files.

Never include the following in a file header:

- The file name
- The file location
- The project name
- The solution name
- Any namespace names
- Any type names
- Any version information
- Any history or change log information
- Any author information

It is recommended that a file header, if used at all, only contains copyright information as the actual documentation of namespaces, types, and members should be done through XML comments.

#### One namespace per file

Never declare more than one namespace per file.

#### One type per file

Always put each type in its own source code file which is named exactly as the type (even delegate types).

Never put more than one type in a source code file.

Exceptions:

- Nested types (more than one type).
- Generic types (more than one type; same type name but different generic type arguments).
- Partial types (one type spread over more than one source code file).

### `extern alias` directives

#### Grouping

Always group `extern alias` directives according to the assemblies they belong to.

Always group `extern alias` directives according to the following structure:

1. Framework assemblies
2. Third-party library assemblies
3. Own library assemblies
4. Assemblies within the same product as the type in the current source code file

Correct:

```c#
extern alias CoolLibraryV1;
extern alias CoolLibraryV2;

extern alias MyLibraryV1;
extern alias MyLibraryV2;

namespace MyCompany.MyProduct.Something {...}
```

Incorrect:

```c#
extern alias MyLibraryV1;
extern alias CoolLibraryV1;

extern alias MyLibraryV2;
extern alias CoolLibraryV2;

namespace MyCompany.MyProduct.Something {...}
```

#### Freestanding

Never put `extern alias` directives inside a namespace.

Correct:

```c#
extern alias FooBarV1;
extern alias FooBarV2;

namespace MyCompany.MyProduct.Utilities
{
	public static class StringUtilities {...}
}
```

Incorrect:

```c#
namespace MyCompany.MyProduct.Utilities
{
	extern alias FooBarV1;
	extern alias FooBarV2;
    
	public static class StringUtilities {...}
}
```

### `using` directives

#### Grouping

Always group `using` directives according to the namespaces in ascending depth and sorted alphabetically.

Always group `using` directives according to the following structure:

1. Framework namespaces
2. Third-party library namespaces
3. Own library namespaces
4. Namespaces with the same root as the type in the current source code file

Correct:

```c#
using System;
using System.Collections;
using System.Collections.Generic;

using SomeOtherLibrary;

using MyCompany.MyLibrary.Collections;
using MyCompany.MyLibrary.Utilities;

using MyCompany.MyProduct.Utilities;

namespace MyCompany.MyProduct.Something {...}
```

Incorrect:

```c#
using MyCompany.MyProduct.Utilities;

using MyCompany.MyLibrary.Utilities;
using MyCompany.MyLibrary.Collections;

using SomeOtherLibrary;

using System;
using System.Collections.Generic;
using System.Collections;

namespace MyCompany.MyProduct.Something {...}
```

#### Freestanding

Never put `using` directives inside a namespace.

Correct:

```c#
using System;
using System.Collections.Generic;

namespace MyCompany.MyProduct.Utilities
{
	public static class StringUtilities {...}
}
```

Incorrect:

```c#
namespace MyCompany.MyProduct.Utilities
{
	using System;
	using System.Collections.Generic;
    
	public static class StringUtilities {...}
}
```

#### `using alias`

Never use `using` alias directives.

Correct:

```c#
using OtherCompany.TheirProduct.CoolFeature;

namespace MyCompany.MyProduct.Utilities {...}
```

Incorrect:

```c#
using CoolFeature = OtherCompany.TheirProduct.CoolFeature;

namespace MyCompany.MyProduct.Utilities {...}
```

Exception: To resolve conflicts between two namespaces or a namespace and a type name.

Example:

```c#
using Bootstrapping = OtherCompany.TheirLibrary.Bootstrapper;

namespace MyCompany.MyProduct.Utilities
{
	public static class MyApplication
    {
        public static void Main ()
        {
            //class Bootstrapper has same name as its containing namespace
            Bootstrapper bs = new Bootstrapper();
            bs.Run();
        }
    }
}
```

#### `using static`

Never use `using static` directives.

Correct:

```c#
using System;

namespace MyCompany.MyProduct.Utilities
{
	public static class Logger
    {
        public static void Print (string message)
        {
            Console.WriteLine(message);
        }
    }
}
```

Incorrect:

```c#
using System;

using static System.Console;

namespace MyCompany.MyProduct.Utilities
{
	public static class Logger
    {
        public static void Print (string message)
        {
            WriteLine(message);
        }
    }
}
```

Exception: For use with mathematical operations (from any framework or library).

Example:

```c#
using System;

using static System.Math;

namespace MyCompany.MyProduct.Utilities
{
	public static class Circle
    {
        public static double CalculateArea (double radius)
        {
            return PI * Pow(radius, 2);
        }
    }
}
```

### `#region` blocks

#### Usage of regions

Always use regions to group members of a type, where each kind of member has its region, in this order:

- Constants
- Static constructor
- Static fields
- Static indexer
- Static properties
- Static events
- Static methods
- Operators
- Instance constructors
- Instance destructor
- Instance fields
- Instance indexer
- Instance properties
- Instance events
- Instance methods
- Overridden and overwritten members
- Interface implementations (one region per implemented interface)
- Nested types (one region per nested type)

Within these regions, always sort the members first by accessibility (in the following order), then by name:

* `public`
* `internal`
* `protected`
* `protected internal`
* `private protected`
* `private`

#### Region scope/level

Always use regions on the level of type members or nested types.

Never use regions in any other scope than type members or nested types.

Correct:

```c#
namespace MyCompany.MyLibrary.Utilities
{
	public static class FileUtilities
    {
    	#region Instance Properties
    	...
    	#endregion
    	
    	#region Instance Methods
    	...
    	#endregion
    }
}
```

Incorrect:

```c#
namespace MyCompany.MyLibrary.Utilities
{
	#region File utilities
	public static class FileUtilities
    {
		...
    }
    #endregion
}
```

#### Nested regions

Never nest regions.

Correct:

```c#
namespace MyCompany.MyLibrary.Utilities
{
	public static class FileUtilities
    {
    	#region Instance Properties
    	...
    	#endregion
    	
    	#region Instance Methods
    	...
    	#endregion
    }
}
```

Incorrect:

```c#
namespace MyCompany.MyLibrary.Utilities
{
	public static class FileUtilities
    {
    	#region Public members
    	
    	#region Properties
    	...
    	#endregion
    	
    	#region Methods
    	...
    	#endregion
    	
    	#endregion
    	
    	#region Private members
    	
    	#region Properties
    	...
    	#endregion
    	
    	#region Methods
    	...
    	#endregion
    	
    	#endregion
    }
}
```

Exception: Nested types which exist in their own region can have nested regions to group its members.

Example:

```c#
namespace MyCompany.MyLibrary.Utilities
{
	public static class FileUtilities
    {
    	#region Instance Properties
    	...
    	#endregion
    	
    	#region Instance Methods
    	...
    	#endregion
    	
    	#region SomeNestedClass
    	private sealed class SomeNestedClass
    	{
    		#region Instance Properties
    		...
    		#endregion
    	
    		#region Instance Methods
    		...
    		#endregion
    	}
    	#endregion
    }
}
```

### Type usage

#### Type aliases

Always use the built-in C# type aliases.

Never use the actual type name for built-in C# type aliases.

Correct:

```c#
int orderTotal = 0;
string customerId = null;

public object SyncRoot { get; }
```

Incorrect:

```c#
Int32 orderTotal = 0;
String customerId = null;

public Object SyncRoot { get; }
```

Exception: Always use the actual type name when used as a part of an identifier or name.

Example:

```c#
public int ConvertToInt32 (string value) {...}
```

#### Fully qualified names

Never use fully qualified names.

Always include types of a namespace with `using`.

Correct:

```c#
using System.Collections;

public sealed class AppleOrangeComparer : IComparer {...}
```

Incorrect:

```c#
public sealed class AppleOrangeComparer : System.Collections.IComparer {...}
```

Exception: Resolution of ambiguous namespaces or type names.

Example:

```c#
using System.Collections;

public sealed class AppleOrangeComparer : IComparer, SomeLibrary.IComparer {...}
```

#### Static type names

Always use the type name to access static members (even from inside the type).

Correct:

```c#
public static StringUtility
{
	...
	string[] pieces = StringUtility.SplitNewLines(value);
	...
}
```

Incorrect:

```c#
public static StringUtility
{
	...
	string[] pieces = SplitNewLines(value);
	...
}
```

#### Nullable types

Never use `Nullable<T>`, use `T?` instead.

Correct:

```c#
int? orderTotal = null;
```

Incorrect:

```c#
Nullable<int> orderTotal = null;
```

Exception: `Nullable<T>` can be used when dealing with type information.

Example:

```c#
Type openTypeInfo = typeof(Nullable<>);
```

#### Attribute types

Always use the shortened type names when applying attributes, omitting the `Attribute` suffix.

Correct:

```c#
[Export]
public class BackupService {...}
```

Incorrect:

```c#
[ExportAttribute]
public class BackupService {...}
```

### Generic constraints

#### Order

Always use the following generic type constraint order (multiplicity stated in parentheses):

1. `class`, `struct`, `unmanaged`, base class type (0...1)
2. other type parameters (0...*)
3. interface types (0...*)
4. `new()` (0...1)

Correct:

```c#
public sealed class ValueProxy <TValue, TProxy>
	where TValue : class, TProxy, IDisposable
	where TProxy : ProxyBase, new()
{...}
```

Incorrect:

```c#
public sealed class ValueProxy <TValue, TProxy>
	where TValue : IDisposable, TProxy, class
	where TProxy : new(), ProxyBase
{...}
```

#### Separation

Always separate generic type constraints into one dedicated line per type parameter.

Correct:

```c#
public sealed class MyDictionary <TKey, TValue>
	where TKey : class
	where TValue : new()
{...}
```

Incorrect:

```c#
public sealed class MyDictionary <TKey, TValue>	where TKey : class where TValue : new()
{...}
```

### Modifiers

#### Order

Always use the following modifier order:

1. `public`, `private`, `protected`, `internal`
2. `new`
3. `abstract`
4. `virtual`
5. `sealed`
6. `override`
7. `static`
8. `readonly`, `ref`
9. `extern`
10. `unsafe`
11. `volatile`
12. `async`
13. `partial`

#### `partial`

Never use `partial` types or methods.

Exception: If the code for a type is not fully but partially auto-generated.

### Variables

#### `var` usage

Never use `var`.

Correct:

```c#
Customer customer = order.GetCustomer();

decimal totalTurnover = customer.CalculateTurnover();


```

Incorrect:

```c#
var customer = order.GetCustomer();

var totalTurnover = customer.CalculateTurnover();
```

Exception: Use as `foreach` iterator variables.

Example:

```c#
foreach (var beam in this.LaserBeams) { ... }
```

#### `out` declaration

Always use `out` parameter variable declaration.

```c#
int value;
if (!int.TryParse(input, out value)) {...}
```

Incorrect:

```c#
if (!int.TryParse(input, out int value)) {...}
```

#### `for` iteration variables

Always declare the `for` iteration variable inside `for`.

Correct:

```c#
for (int index = 0; index < orders.Count; index++)
{
    ...
}
```

Incorrect:

```c#
int index;
for (index = 0; index < orders.Count; index++)
{
    ...
}
```

Exception: After the loop finished iteration, the last index (plus one) needs to be known.

Example:

```c#
int index;
for (index = 0; index < orders.Count; index++)
{
    ...
}
orders.InsertAt(index, newOrder);
```

#### Scope reduction

Always declare a variable as close to its use as possible and in the narrowest/innermost scope possible.

Correct:

```c#
foreach (var beam in this.LaserBeams)
{
    ...
    float requiredPowerKilowatts = beam.RequiredPowerKilowatts;
    ...
}
```

Incorrect:

```c#
float requiredPowerKilowatts = 0.0f;
...
foreach (var beam in this.LaserBeams)
{
    ...
    requiredPowerKilowatts = beam.RequiredPowerKilowatts;
    ...
}
```

#### Multiple declarations

Never declare multiple variables in the same statement or on the same line.

Correct:

```c#
double powerKilowatts = 0.0;
int numberOfRounds = 0;
int missCount = 0;
```

Incorrect:

```c#
double powerKilowatts = 0.0; int numberOfRounds, missCount;
numberOfRounds = missCount = 0;
```

### Expressions

#### `nameof`

Always use `nameof` instead of hard-coded names.

Correct:

```c#
this.OnPropertyChanged(nameof(this.UserName));
```

Incorrect:

```c#
this.OnPropertyChanged("UserName");
```

#### `this`, `base`

Always use `this` or `base` to access instance members (including constructors) from inside the type.

Correct:

```c#
public sealed class IceCreamMachine : FoodMachine
{
	public IceCreamMachine (string name)
	 : this (name, null) {...}
    
    public IceCreamMachine (string name, Recipe[] recipes)
     : base (name) {...}
    
    public override void Start ()
    {
    	base.Start();
    	this.DeconstructRecipe();
    }
    
    public new Serving DispenseOneServing ()
    {
    	Serving serving = base.DispenseOneServing();
    	this.AddToppings(serving);
    	return serving;
    }
}
```

Incorrect:

```c#
public sealed class IceCreamMachine : FoodMachine
{
	public IceCreamMachine (string name)
	 : base(name) {...}
    
    public IceCreamMachine (string name, Recipe[] recipes)
     : base(name) {...}
    
    public override void Start ()
    {
    	base.Start();
    	DeconstructRecipe();
    }
    
    public new Serving DispenseOneServing ()
    {
    	Serving serving = ((FoodMachine)this).DispenseOneServing();
    	AddToppings(serving);
    	return serving;
    }
}
```

#### Numeric literals

Always use `_` as thousand separators for numeric literals.

Correct:

```c#
const int FifthPerfectNumber = 33_550_336;
```

Incorrect:

```c#
const int FifthPerfectNumber = 33550336;
```

#### Prefer expressions

Always use the lambda expression statement form if possible for:

* Constructors
* Finalizers
* Methods
* Properties (getter and setter)

Correct:

```c#
public override string ToString() => this.Name;

public string Address => this._address ?? string.Empty;

public string Name
{
	get => this._name;
	set => this._name = value ?? "[Unknown]";
}
```

Incorrect:

```c#
public override string ToString()
{
    return this.Name;
}

public string Address
{
	get
    {
    	return this._address ?? string.Empty;
    }
}

public string Name
{
	get
    {
    	return this._name;
    }
    set
    {
    	this._name = value ?? "[Unknown]";
    }
}
```

### Statements

#### `goto`

Never use `goto`.

Exceptions:

* To go out of deeply nested loops.
* To jump to another `case` of the same `switch` using `goto case`.

### TODO Enumerations



## Formatting

### Braces

#### Used braces

*See [Templates](#Templates) section for examples*

Always use curly braces with the following, even for one line code blocks:

* `do`
* `while`
* `if`, `else`
* `for`
* `foreach`
* `switch`
* `fixed`
* `lock`
* `try`, `catch`, `finally`
* `using` (the statement, not the directive)
* `unsafe` (the statement, not the modifier)
* `checked` (the statement, not the expression)
* `unchecked` (the statement, not the expression)

#### Omitted braces

*See [Templates](#Templates) section for examples*

Never use curly braces with the following, even for multi line code blocks:

* `case`

* `default` (the `switch` label, not the expression)

#### Separate lines

Always put curly braces on their own line.

Correct:

```c#
if (orders.Count == 0)
{
    this.ShowWarning("Customer never ordered anything.");
}
```

Incorrect:

```c#
if (orders.Count == 0) {
    this.ShowWarning("Customer never ordered anything.");
}
```

Exception: Auto properties.

Example:

```c#
public bool IsRunning { get; private set; }
```

### Parenthesis

#### Used parenthesis

*See [Templates](#Templates) section for examples*

Always use parenthesis with the following:

* `nameof`
* `sizeof`
* `typeof`
* `catch`, `when`
* `checked` (the expression, not the statement)
* `unchecked` (the expression, not the statement)
* `default` (the expression, not the `switch` label)

#### Omitted parenthesis

*See [Templates](#Templates) section for examples*

Never use parenthesis with the following, except to express precedence where applicable:

* `await`

* `stackalloc`

* `case`, `when`

* `goto`

* `return`

* `yield return`

* `throw`

#### Explicit operator precedence

Always use parenthesis to explicitly express the precedence of operators.

Correct:

```c#
if (((width * height) + offset) >= threshold)
{
    ...
}
```

Incorrect:

```c#
if (width * height + offset >= threshold)
{
    ...
}
```

### Whitespaces

#### Tabs vs. Spaces

Always use spaces with a tab and indent size of 4.

Always replace tabs used for code formatting with spaces.

#### Spaces

Always put *one* space...

* ...around `=>`.

  ```c#
  Action<string> log = x => Console.WriteLine(x);
  ```

* ...around `:` in type declarations.

  ```c#
  public sealed class IceCreamMachine : IFoodDispenser { ...}
  ```

* ...around `:` in generic type constraints.

  ```c#
  public sealed class RandomList<T>
   where T : new()
  {...}
  ```

* ...around `:` in constructor declarations.

  ```c#
  public IceCreamMachine (MachineController controller)
   : base(controller)
  {...}
  
  public IceCreamMachine ()
   : this(null)
  {...}
  ```

* ...around non-unary operators.

  ```c#
  int x = a + b;
  int y = x >= 0 ? x * 10 : x * 20;
  ```

* ...around assignment operators.

  ```c#
  int x = a + b;
  x += 42;
  ```

* ...around curly braces of auto properties.

  ```c#
  public string Name { get; private set; }
  ```

* ...between the member name and the `(` argument parameter list (declaration).

  ```c#
  public Response DownloadFile (Request request) {...}
  ```

* ...between the member name and the `<` type parameter list (declaration).

  ```c#
  public T GetExport <T> () {...}
  ```

* ...between the member name and the `[` indexer parameter list (declaration).

  ```c#
  public string this [int index] {...}
  ```

* ...before `where ` generic type constraints.

  ```c#
  public sealed class RandomList<T> : IList<T>, IList
   where T : new()
  {...}
  ```

* ...before `base` and `this` in constructor declarations.

  ```c#
  public IceCreamMachine (MachineController controller)
   : base(controller)
  {...}
  
  public IceCreamMachine ()
   : this(null)
  {...}
  ```

* ...after argument parameter separator `,`.

  ```c#
  public Response DownloadFile (Request request, TimeSpan timeout) {...}
  ```

* ...after type parameter separator `,`.

  ```c#
  Dictionary<string, string> dictionary = new Dictionary<string, string>();
  ```

* ...after inheritance separator `,`.

  ```c#
  public sealed class RandomList<T> : IList<T>, IList
   where T : new()
  {...}
  ```

* ...after constraint separator `,`.

  ```c#
  public sealed class ClonePool<T>
   where T : ICloneable, new()
  {...}
  ```

Never put *any* space...

* ...around `:` in case labels.

  ```c#
  switch (...)
  {
      default:
      	break;
      
      case 123:
      	break;
  }
  ```

* ...around `[` and`]` for attributes.

  ```c#
  [Export]
  public class BackupService {...}
  ```

* ...between unary operator and operand.

  ```c#
  int x = a++;
  ```

* ...between the member name and the `(` argument parameter list (usage).

  ```c#
  connection.Send(message);
  ```

* ...between the member name and the `<` type parameter list (usage).

  ```c#
  BackupService backupService = container.GetExport<BackupService>();
  ```

* ...between the member name and the `[` indexer parameter list (usage).

  ```c#
  Customer firstCustomer = customers[0];
  ```

* ...between `new` and `()` in `new()` generic constraint.

  ```c#
  public sealed class ClonePool<T>
   where T : ICloneable, new()
  {...}
  ```

* ...before the first parameter.

  ```c#
  Response response = connection.DownloadFile(request, 1000);
  ```

* ...before argument parameter separator `,`.

  ```c#
  public Response DownloadFile (Request request, TimeSpan timeout) {...}
  ```

* ...before type parameter separator `,`.

  ```c#
  Dictionary<string, string> dictionary = new Dictionary<string, string>();
  ```

* ...before inheritance separator `,`.

  ```c#
  public sealed class RandomList<T> : IList<T>, IList
   where T : new()
  {...}
  ```

* ...before constraint separator `,`.

  ```c#
  public sealed class ClonePool<T>
   where T : ICloneable, new()
  {...}
  ```

* ...before enumeration member separator `,`.

  ```c#
  public enum DeviceState
  {
      Idle = 0,
      Running = 1,
      Error = 2,
  }
  ```

* ...before `;`.

  ```c#
  int x = a + b;
  ```

* ...before `[]` or `[...]` for arrays.

  ```c#
  byte[] buffer = new byte[1024];
  ```

* ...inside `[]` or `[...]` for arrays.

  ```c#
  byte[] buffer = new byte[1024];
  ```

* ...after the last parameter.

  ```c#
  Response response = connection.DownloadFile(request, 1000);
  ```

* ...after `base` and `this` in constructor declarations.

  ```c#
  public IceCreamMachine (MachineController controller)
   : base(controller)
  {...}
  
  public IceCreamMachine ()
   : this(null)
  {...}
  ```

#### Indentations

Always increment the indentation level...

- ...after opening curly braces `{`.
- ...after `case` or `default` label.
- ...after first line of multiline statement.

Always decrement the indentation level...

- ...before closing curly braces `}`.
- ...after `case` block.
- ...after last line of multiline statement.

Never change indentation level...

* ...after `#region`.

#### Empty lines

Always put *one* empty line between...

* ...any of the following at a file level:
  * `extern alias` groups.
  * `using` groups with different namespace roots.
  * `using static` groups with different namespace roots.
  * `namespace`.
* ...any of the following inside a type:
  * Regions.
  * Members.
  * Nested types.
* ...`#region` and the region content.
* ...the region content and `#region`.
* ...`enum` members.

Never put *any* empty line between...

* ...a comment and the type or member its describing.
  Note: A comment is considered part of the type or member.
* ...a curly brace (`{`, `}`) and its outer or inner scope.
* ...a type or member declaration and its generic type constraints.
* ...a constructor declaration and its `base` or `this` calls.

#### Trailing whitespace

Never have any trailing whitespace on a line before the carriage return or line feed.

#### Trailing empty line

Always have exactly one empty line at the end of the file (so the file ends with a line feed).

## Commenting

### Language

Always use proper English language for all comments.

### TODO Usage

[TBD]

### TODO XML comments

Namespaces



Classes and Structs



Enumerations



Delegates



Constants



Constructors



Destructors



Fields



Indexer



Properties



Events



Methods



Operators



## TODO Preprocessor



## TODO Templates

Always use parenthesis with the following:

- `checked`

  ```c#
  checked(someValue + 10)
  ```

- `unchecked`

- ```c#
  checked(someValue + 10)
  ```

  `default`

  ```c#
  default(T)
  ```

- `nameof`

  ```c#
  nameof(this.SomeProperty)
  ```

- `sizeof`

  ```c#
  sizeof(int)
  ```

- `typeof`

  ```c#
  typeof(int)
  ```

- `catch`, `when`

  ```c#
  catch (HttpRequestException e) when (e.Message.Contains("404"))
  ```

#### Omitted parenthesis

Never use parenthesis with the following, except to express precedence:

- `await`

  ```c#
  await someTask
  ```

- `stackalloc`

  ```c#
  stackalloc int[100]
  ```

- `case`, `when`

  ```c#
  case Rectangle r when r.Area > 0:
  ```

- `goto`

  ```c#
  goto someLabel;
  ```

- `return`

  ```c#
  return someValue;
  ```

- `yield return`

  ```c#
  yield return someValue;
  ```

- `throw`

  ```c#
  throw new InvalidOperationException();
  ```

### 



Always use curly braces with the following, even for one line code blocks:

- `do`

  ```c#
  do
  {
      ...
  } while (device.IsBusy)
  ```

- `while`

  ```c#
  while (device.IsBusy)
  {
      ...
  }
  ```

- `if`, `else`

  ```c#
  if (orders.Count == 0)
  {
      ...
  }
  else
  {
      ...
  }
  ```

- `for`

  ```c#
  for (int index = 0; index < this.Customers.Count; index++)
  {
      ...
  }
  ```

- `foreach`

  ```c#
  foreach (var customer in this.Customers)
  {
      ...
  }
  ```

- `switch`

  ```c#
  switch (args[0])
  {
  	...
  }
  ```

- `fixed`

  ```c#
  fixed (int* p = &pt.x)
  {
      ...
  }
  ```

- `lock`

  ```c#
  lock (this.SyncRoot)
  {
      ...
  }
  ```

- `unsafe`

  ```c#
  unsafe
  {
      ...
  }
  ```

- `using`

  ```c#
  using (MemoryStream ms = new MemoryStream())
  {
      ...
  }
  ```

- `try`, `catch`, `finally`

  ```c#
  try
  {
      ...
  }
  catch
  {
      ...
  }
  finally
  {
      ...
  }
  ```

- `checked`

  ```c#
  checked
  {
      ...
  }
  ```

- `unchecked`

  ```c#
  unchecked
  {
      ...
  }
  ```

#### Omitted braces

Never use curly braces with the following, even for multi line code blocks:

- `case`

  ```c#
  switch (args[0])
  {
      case abc:
          ...
          break;
  }
  ```

- `default`

  ```c#
  switch (args[0])
  {
      default:
          ...
          break;
  }
  ```

### 





Move block structures to here (braces, parenthesis)



Classes



Structs



Enumerations



Delegates



Constants



Constructors



Destructors



Fields



Indexer



Properties



Events



Methods



Operators



#### TODO Object initializers

[TBD]

#### TODO Anonymous methods

[TBD]

#### TODO Lambda expressions

[TBD]