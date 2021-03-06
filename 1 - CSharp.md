# PART I - C#

*[C#/.NET Coding Guidelines](https://github.com/RotenInformatik/RI_CodingGuidelines) | Version 1.0 | Author: Andreas Roten | License: Apache License 2.0*

The rules in this part specify how to use the C# programming language.

Typically, they do not affect software functionality or behavior but merely names and code prettiness.

For compactness, most code examples only adhere to its associated rule, not to all rules.

[TOC]

## Naming

### Language

Always use proper English language for all names.

### Characters

Never...

- ...use any other character than uppercase letters (`A-Z`), lowercase letters (`a-z`), and numbers (`0-9`).
- ...use numbers (`0-9`) at the beginning of names.
- ...use underscores (`_`), except as prefix for private fields, as separator for test assembly suffixes, or as separator for test method names.

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

#### Test assemblies

*See [Test code](#Test code)*

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

### Test code

#### Assemblies

Always put test code into their own test assembly.

Never put unit tests, integration tests, and system tests into the same test assembly.

Always name a test assembly after the assembly which contains the concrete types (for unit tests), the subsystem (for integration tests), or the system (for system tests) it is testing, otherwise adhering to the same naming rules as described in here.

Always use the following suffixes for the test assembly names:

* Unit tests: `_UnitTests`
* Integration tests: `_IntegTests`
* System tests: `_SysTests`

#### Types

Always name a test type after the concrete type (for unit tests), the subsystem (for integration tests), or the system (for system tests) it is testing, otherwise adhering to the same naming rules as described in here.

Example (unit test):

```c#
public sealed class LaserBeam { ... }
```

Example (integration test):

```c#
public sealed class SpaceshipAi { ... }
```

Example (system test):

```c#
public sealed class SpaceshipGameOnLinux { ... }
```

#### Methods

Always use the following pattern to name test methods: `Situation_TestAction_ExpectedOutcome`, otherwise adhering to the same naming rules as described in here.

Example:

```c#
public void LaserBeamIdle_FireLaserBeam_LaserBeamFiring () { ... }
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
- Instance finalizers
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
public static class StringUtility
{
	...
	string[] pieces = StringUtility.SplitNewLines(value);
	...
}
```

Incorrect:

```c#
public static class StringUtility
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

#### `do...while`

Always put the `while` statement of a `do...while` loop on the same line as the closing curly brace `}`.

Correct:

```c#
do (...)
{
    ...
} while (...)
```

Incorrect:

```c#
do (...)
{
    ...
}
while (...)
```

#### `switch`, `default`

Always put the default block at the beginning of a switch block.

Correct:

```c#
switch (args[0])
{
    default:
        ...
        break;

    case abc:
        ...
        break;
}
```

Incorrect:

```c#
switch (args[0])
{
    case abc:
        ...
        break;

    default:
        ...
        break;
}
```

### Enumerations

#### One member per line

Never put more than one `enum` member on the same line.

Correct:

```c#
public enum DeviceState
{
    Unknown = 0,
    Off = 1,
    Idle = 2,
    Working = 3,
}
```

Incorrect:

```c#
public enum DeviceState
{
    Unknown, Off, Idle, Working
}
```

#### Member ending consistency

Always end each `enum` member with the `enum` member separator `,`.

Correct:

```c#
public enum DeviceState
{
    Unknown = 0,
    Off = 1,
    Idle = 2,
    Working = 3,
}
```

Incorrect:

```c#
public enum DeviceState
{
    Unknown = 0,
    Off = 1,
    Idle = 2,
    Working = 3
}
```

## Formatting

### Braces

#### Used braces

*See [Templates](#Templates) section for examples*

Always use curly braces with the following, even for one line code blocks:

* `do...while`
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

Always use spaces. A tab is converted to 4 spaces.

Always use spaces for both code and comments.

Always replace tabs used for code formatting with spaces.

#### Spaces

Always put *one* space...

* ...around `=>`.

  ```c#
  Action<string> log = message => Console.WriteLine(message);
  ```

* ...around `:` in type declarations.

  ```c#
  public sealed class IceCreamMachine : IFoodDispenser { ...}
  ```

* ...around `:` in generic type constraints.

  ```c#
  public sealed class RandomList <T>
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

* ...between the type name and the `<` type parameter list (declaration).

  ```c#
  public sealed class RandomList <T> : IList<T>, IList
  {...}
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
  public sealed class RandomList <T> : IList<T>, IList
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
  public sealed class RandomList <T> : IList<T>, IList
   where T : new()
  {...}
  ```

* ...after constraint separator `,`.

  ```c#
  public sealed class ClonePool <T>
   where T : ICloneable, new()
  {...}
  ```

* ...after a control or block statement and its opening parenthesis `(`.

  ```c#
  if (...) {...}
  foreach (...) {...}
  lock (...) {...}
  using (...) {...}
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

* ...between the type name and the `<` type parameter list (usage).

  ```c#
  public sealed class RandomList <T> : IList<T>, IList
  {...}
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
  public sealed class ClonePool <T>
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
  public sealed class RandomList <T> : IList<T>, IList
   where T : new()
  {...}
  ```

* ...before constraint separator `,`.

  ```c#
  public sealed class ClonePool <T>
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

* ...after a single line statement or expression and its opening parenthesis `(`.

  ```c#
  sizeof(...)
  typeof(...)
  checked(...)
  ```

#### Indentations

Always increment the indentation level...

- ...after opening curly braces `{`.
- ...after `case` or `default` label.
- ...after the first line of multiline statements.

Always decrement the indentation level...

- ...before closing curly braces `}`.
- ...after `case` block.
- ...after last line of multiline statement.

Never change indentation level...

* ...after `#region`.
* ...before `#endregion`.

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

### Usage

Always use comments for the following, never for anything else:

* To describe public namespaces, types, and members as part of the API documentation.
* To describe non-obvious or unexpected behaviour.
* To describe non-obvious or complex code structures.
* To provide additional explanation about *why* and *how*.
* To provide references and links to additional documentation.

Never state or describe the obvious.

Always comment...

* ...all public namespaces.
* ...all public types.
* ...all public and protected members.

Never comment...

* ...`#region` blocks.
* ...`extern alias` directives.
* ...`using` directives.

### Whitespaces

#### Spaces

Always put *one* space...

- ...after starting a regular comment.

  ```c#
  // Some explanation here.
  ```

- ...after starting an XML comment.

  ```c#
  /// <summary>
  ///     Implements something.
  /// </summary>
  /// <threadsafety static="false" instance="false" />
  ```

#### Indentations

Always increment the indentation level...

- ...after an opening XML comment tag.

Always decrement the indentation level...

- ...before before a closing XML comment tag.

Never change indentation level...

- ...within the same XML comment level.

Always fall back to indentation level zero...

* ...for CDATA blocks of `code` XML comment elements.

#### Empty lines

Never use empty lines in or between comments.

### Regular comments

#### General

Always use regular comments (`//`, `/**/`) inside code blocks (e.g. method bodies) but never outside.

#### Decorations

Never use decorations in XML comments (e.g. using `_` or `-` for underlining or `*` for framing).

Exception: For structuring large blocks of necessary comments.

Example:

```c#
/************************/
/* Top secret algorithm */
/************************/

// PURPOSE
// -------
// ...some lengthy explanation...

// HOW IT WORKS
// ------------
// ...some lengthy explanation...
```

### XML comments

#### General

Always use XML comments (`///`) outside code blocks (e.g. method declarations) but never inside.

Always follow the additional rules as described below and the formatting as shown in [Templates](#Templates).

#### Decorations

Never use decorations in XML comments (e.g. using `_` or `-` for underlining or `*` for framing).

#### Documentation file

Always use the `doc` compiler parameter to generate an XML documentation file for each assembly.

Always name the XML documentation file the same as the corresponding assembly, except the extension.

#### Documentation tool

Always define the XML comments in a way which supports the selected documentation tool.

Ensure that the entire organization uses the same documentation tool.

Sandcastle Help File Builder (SHFB) is the recommended documentation tool and therefore the following rules for XML comments adhere to the style and possibilities of SHFB.

#### Namespaces

Always use a source code file named *_NamespaceDoc.cs* once per namespace to document it.

If a namespace is defined in more than one assembly, put *_NamespaceDoc.cs* in the assembly which is at the top of the dependency tree. If a namespace is defined in multiple assemblies not depending on each other, put a separate *_NamespaceDoc.cs* in each assembly.

The content of a *_NamespaceDoc.cs* source code file must look like the following:

```c#
using System.Runtime.CompilerServices;

namespace MyCompany.MyProduct.MyComponent.SomeNamespace
{
	/// <summary>
	///    Contains some utilities for blah and foobar.
	/// </summary>
	[CompilerGenerated]
	public sealed class NamespaceDoc
	{
	}
}
```

Always adhere to the following rules for *_NamespaceDoc.cs* source code files:

* The source code file must be named *_NamespaceDoc.cs*.
* The source code file must not contain any other namespaces or types than described here.
* The source code file must contain a class named *NamespaceDoc* inside the described namespace.
* The class *NamespaceDoc* must be `public` and `sealed`.
* The class *NamespaceDoc* must not derive from a class (except `object`) or implement any interface.
* The class *NamespaceDoc* must not implement any members.
* The class *NamespaceDoc* must have the `CompilerGenerated` attribute.
* The class *NamespaceDoc* must have only and exactly one `summary` XML comment.
* The `summary` XML comment must start with *Contains* and should be only one sentence.

### Special comments

#### Conceptional documentation

Always put a comprehensive explanation about concepts in a single, logical place and reference to that place using `see` references inside a `remarks`/`para` block.

```c#
/// <summary>
///     Implements a local bus which can use optional connections to remote busses.
/// </summary>
/// <remarks>
///     <para>
///         See <see cref="IBus" /> for more details.
///     </para>
/// </remarks>
/// <threadsafety static="true" instance="true" />
public sealed class LocalBus : IBus { ... }

/// <summary>
///     Defines the interface for a message bus.
/// </summary>
/// <remarks>
///     ... hundreds of lines which explains the whole concept of message busses...
/// </remarks>
/// <threadsafety static="true" instance="true" />
public interface IBus : IDisposable, ISynchronizable, ILogSource
```

#### Default values

Always document the default values of constants, fields, and properties with setters using `c` elements in a `remarks`/`para` block.

```c#
/// <summary>
///     The sigma or standard deviation of all values in the history.
/// </summary>
/// <remarks>
///     <para>
///         The default value is <c> 0.0 </c>.
///     </para>
/// </remarks>
public double Sigma;
```

#### Default implementations

Always state a virtual members default implementation in a `remarks`/`note`/`implement` block.

```c#
/// <summary>
///     Called when the logging needs to be configured.
/// </summary>
/// <remarks>
///     <note type="implement">
///         The default implementation does nothing.
///     </note>
/// </remarks>
protected virtual void ConfigureLogging () { ... }
```

#### Asynchronous methods

Always describe the continuation of a `Task`-returning or `async` method in the `returns` block.

```c#
/// <summary>
///     Dispatches an operation onto a thread.
/// </summary>
/// <param name="operation"> The operation to dispatch. </param>
/// <returns>
///     The task which continues after the operation finished dispatching.
/// </returns>
public async Task Dispatch (Delegate operation) { ... }
```

#### Dynamic members

Always provide a note in a `remarks`/`note`/`important` block that a member is dynamic and might impact performance and portability.

```c#
/// <summary>
///     Gets the value bag which provides untyped access to the document.
/// </summary>
/// <value>
///     The value bag which provides untyped access to the document.
/// </value>
/// <remarks>
///     <note type="important">
///         This is a dynamic member and might impact performance or portability.
///     </note>
/// </remarks>
public dynamic ValueBag { get; }
```

#### Number of enumerations

Always state how often an enumerable parameter is enumerated in a `remarks`/`para` block.

```c#
/// <summary>
///     Determines how many elements are in a sequence.
/// </summary>
/// <typeparam name="T"> The type of the elements in the sequence. </typeparam>
/// <param name="enumerable"> The sequence which contains the elements. </param>
/// <returns>
///     The amount of elements in the sequence.
/// </returns>
/// <remarks>
///     <para>
///         This is a O(n) operation where n is the number of elements in the sequence.
///     </para>
///     <para>
///         <paramref name="enumerable" /> is enumerated exactly once.
///     </para>
/// </remarks>
public static int Count <T> (this IEnumerable<T> enumerable)
```

#### Algorithmic complexity

Always state the algorithmic complexity of a collection type or member in a `remarks`/`para` block.

```c#
/// <summary>
///     Determines how many elements are in a sequence.
/// </summary>
/// <typeparam name="T"> The type of the elements in the sequence. </typeparam>
/// <param name="enumerable"> The sequence which contains the elements. </param>
/// <returns>
///     The amount of elements in the sequence.
/// </returns>
/// <remarks>
///     <para>
///         This is a O(n) operation where n is the number of elements in the sequence.
///     </para>
///     <para>
///         <paramref name="enumerable" /> is enumerated exactly once .
///     </para>
/// </remarks>
public static int Count <T> (this IEnumerable<T> enumerable)
```

#### Unsafe contexts

Always indicate unsafe types or members with a corresponding note in a `remarks`/`note`/`security` block.

```c#
/// <summary>
///     Performs a fast data buffer copy.
/// </summary>
/// <param name="source"> The source data buffer. </param>
/// <param name="destination"> The destination data buffer. </param>
/// <param name="count"> The number of bytes to copy. </param>
/// <remarks>
///     <note type="security">
///         This method is unsafe.
///     </note>
/// </remarks>
public unsafe static void FastCopy (byte[] source, byte[] destination, int count) {...}
```

#### Locking

Always state when a type or member performs locking which can leave the context of the type itself (e.g. through an event, callback, or member call of an outside-provided instance).

```c#
/// <summary>
///     Implements a state machine.
/// </summary>
/// <remarks>
///     <note type="important">
///         Some virtual methods are called from within locks to
///         <see cref="SyncRoot" />. Be careful in inheriting classes when
///         calling outside code from those methods (e.g. through events, callbacks,
///         or other virtual methods) to not produce deadlocks!
///     </note>
/// </remarks>
/// <threadsafety static="true" instance="true" />
public class StateMachine : LogSource, ISynchronizable { ... }
```

#### Thread safety

Always state the thread-(un)safety of a type using `threadsafety` and make sure that this type is either thread-safe or unsafe in its entirety (with one scope for static members and one for instance members).

Always state the thread-(un)safety on interfaces if the interface implementations are expected to be thread-safe or thread-unsafe. Omit the thread-safety statement if the interface implementor can decide on its own whether to implement it thread-safe or not.

Always state the thread-(un)safety on delegates if the usages are expected to be thread-safe or thread-unsafe. Omit the thread-safety statement if the delegate user can decide on its own whether to use it thread-safe or not.

#### Exceptions

Always document all exceptions which can be thrown by a member (including unhandled exceptions which can be thrown by another member used inside) using `exception` blocks.

#### Extension methods

Always document extension methods like they are part of the type they extend.

### XML comment elements

#### Order

Always use the following XML comment element order:

1. `inheritdoc`
2. `summary`
3. `typeparam`
4. `param`
5. `returns`
6. `value`
7. `event`
8. `remarks`
9. `threadsafety`
10. `exception`
11. `example`

#### `summary`

**Type**: Top-level block element.

**Used on**: Types, Members.

**Mandatory**: For public types and public/protected members.

**Multiplicity**: One per type or member.

**Purpose**: Describes a type or member in one sentence. Use `remarks` for more details.

**Parent tags**: None.

**Child tags**: Any inline elements.

**Attributes**: None.

**Example**:

```c#
/// <summary>
///     Implements a list of random items.
/// </summary>
```

#### `typeparam`

**Type**: Top-level block element.

**Used on**: Types, Members.

**Mandatory**: For generic public types and generic public/protected members.

**Multiplicity**: One per generic type parameter.

**Purpose**: Describes a generic type parameter.

**Parent tags**: None.

**Child tags**: Any inline elements.

**Attributes**:

* `name`; Mandatory; The name of the generic type parameter.

**Example**:

```c#
/// <typeparam name="T"> The type of random items stored in the list. </typeparam>
```

#### `param`

**Type**: Top-level block element.

**Used on**: Members.

**Mandatory**: For members with parameters.

**Multiplicity**: One per member parameter.

**Purpose**: Describes a member parameter.

**Parent tags**: None.

**Child tags**: Any inline elements.

**Attributes**:

- `name`; Mandatory; The name of the member parameter.

**Example**:

```c#
/// <param name="item"> The item which is added to the list. </param>
```

#### `returns`

**Type**: Top-level block element.

**Used on**: Methods, Operators.

**Mandatory**: For all methods and operators with a return value.

**Multiplicity**: One per method or operator.

**Purpose**: Describes a return value.

**Parent tags**: None.

**Child tags**: Any inline elements.

**Attributes**: None.

**Example**:

```c#
/// <returns>
///     The first item in the list or null if the list is empty.
/// </returns>
```

#### `value`

**Type**: Top-level block element.

**Used on**: Properties, Indexer.

**Mandatory**: For all properties, indexer.

**Multiplicity**: One per property, indexer.

**Purpose**: Describes a (returned) value. Use `remarks`  to state default values.

**Parent tags**: None.

**Child tags**: Any inline elements.

**Attributes**: None.

**Example**:

```c#
/// <value>
///     True if the list is empty, false otherwise.
/// </value>
```

#### `event`

**Type**: Top-level block element.

**Used on**: Members.

**Mandatory**: For members which can raise events.

**Multiplicity**: One per event which can be raised.

**Purpose**: Describes an event which could be raised by using the member.

**Parent tags**: None.

**Child tags**: Any inline elements.

**Attributes**:

- `cref`; Mandatory; The event member which can be raised.

**Example**:

```c#
/// <param cref="Started"> Raised after start is complete. </typeparam>
```

#### `remarks`

**Type**: Top-level block element.

**Used on**: Types, Members.

**Mandatory**: For public types and public/protected members which require description of details.

**Multiplicity**: One per type or member.

**Purpose**: Describes details of a type or member.

**Parent tags**: None.

**Child tags**: `para`, `note`.

**Attributes**: None.

**Example**:

```c#
/// <remarks>
///     <para>
///         The random list is automatically filled with randomized items.
///     </para>
///     <note type="note">
///         This is just an example.
///         It is just nonsense so you focus on the actual template.
///     </note>
/// </remarks>
```

#### `para`

**Type**: Block element subordinated to `remarks`.

**Used on**: *same as `remarks`*

**Mandatory**: All descriptions must be in `para` or `note`, not in `remarks` directly.

**Multiplicity**: One for each described general detail.

**Purpose**: Describes general details of a type or member.

**Parent tags**: `remarks`.

**Child tags**: Any inline elements.

**Attributes**: None.

**Example**:

```c#
///     <para>
///         The random list is automatically filled with randomized items.
///     </para>
```

#### `note`

**Type**: Block element subordinated to `remarks`.

**Used on**: *same as `remarks`*

**Mandatory**: All descriptions must be in `para` or `note`, not in `remarks` directly.

**Multiplicity**: One for each described detail of significant importance.

**Purpose**: Describes details of a type or member which are of significant importance.

**Parent tags**: `remarks`.

**Child tags**: Any inline elements.

**Attributes**:

- `type`; Mandatory; The significance of the described detail.

**Significance**:

The following can be used for the `type` attribute:

* `note`: A hint or non-obvious detail.
* `important`: An important detail which must be considered when using the type or member.
* `implement`: A rule which must be followed by inheritors.
* `security`: A security-relevant detail or advise.
* `cs`: A note related to the C# language.

**Example**:

```c#
///     <note type="note">
///         This is just an example.
///         It is just nonsense so you focus on the actual template.
///     </note>
```

#### `threadsafety`

**Type**: Top-level block element.

**Used on**: Types.

**Mandatory**: For all types.

**Multiplicity**: One for each type.

**Purpose**: States whether a types members are thread-safe or not.

**Parent tags**: None.

**Child tags**: None.

**Attributes**:

* `static`; Mandatory; States whether public/protected static members are thread safe.
* `instance`; Mandatory; States whether public/protected instance members are thread safe.

**Example**:

```c#
/// <threadsafety static="false" instance="false" />
```

#### `exception`

**Type**: Top-level block element.

**Used on**: Members.

**Mandatory**: For all members which can throw exceptions.

**Multiplicity**: One for each exception which can be thrown by the member.

**Purpose**: Describes which exceptions can be thrown under which circumstances.

**Parent tags**: None.

**Child tags**: Any inline elements.

**Attributes**:

* `cref`; Mandatory; References the exception type which is described.

Example:

```c#
/// <exception cref="ArgumentNullException">
///     <paramref name="item" /> is null.
/// </exception>
```

#### `example`

**Type**: Top-level block element.

**Used on**: Types, Members.

**Mandatory**: For public types and public/protected members where usage is not obvious.

**Multiplicity**: One per type or member.

**Purpose**: Provides an example how to use a type or member.

**Parent tags**: None.

**Child tags**: `code` and any inline elements.

**Attributes**: None.

**Example**:

```c#
/// <example>
///     Here is some example:
///     <code language="cs">
/// <![CDATA[
/// RandomList<string> rl = new RandomList<string>();
/// ...
/// ]]>
///     </code>
/// </example>
```

#### `code`

**Type**: Block element subordinated to `example`.

**Used on**: *same as `example`*

**Mandatory**: All code examples must be in `code`, not in `example` directly.

**Multiplicity**: One for each code example.

**Purpose**: Provides the actual sample code for an example.

**Parent tags**: `example`.

**Child tags**: `CDATA`

**Attributes**:

* `language`; Mandatory; States the used code language; `cs` = C#

**Example**:

```c#
///     <code language="cs">
/// <![CDATA[
/// RandomList<string> rl = new RandomList<string>();
/// ...
/// ]]>
///     </code>
```

#### `inheritdoc`

**Type**: Top-level block element.

**Used on**: Types, Members.

**Mandatory**: For public types and public/protected members which inherit documentation from another.

**Multiplicity**: One per type or member.

**Purpose**: Applies the documentation already written for another type or member to avoid duplicates.

**Parent tags**: None.

**Child tags**: None.

**Attributes**:

- `cref`; Optional; References the type and/or member from which the documentation is inherited.

**Example** (inheriting the documentation from the base type or interface):

```c#
/// <inheritdoc />
```

**Example** (inheriting the documentation from a particular type and/or member):

```c#
/// <inheritdoc cref="IThreadDispatcher.Post(Delegate,object[])"/>
```

#### `paramref`

**Type**: Inline element.

**Purpose**: References a parameter of the current member.

**Attributes**:

* `name`; Mandatory; The name of the referenced member parameter.

**Example**:

```c#
/// <exception cref="ArgumentNullException">
///     <paramref name="item" /> is null.
/// </exception>
```

#### `typeparamref`

**Type**: Inline element.

**Purpose**: References a generic type parameter of the current type or member.

**Attributes**:

* `name`; Mandatory; The name of the referenced generic type parameter.

**Example**:

```c#
/// <returns>
///     The first resolved value of type <typeparamref name="T" /> or null.
/// </returns>
```

#### `see` (code reference)

**Type**: Inline element.

**Purpose**: References another type or member.

**Attributes**:

* `cref`; Mandatory; The referenced type or member.

**Example** (with member parameters for overloaded members):

```c#
/// <remarks>
///     <para>
///         See <see cref="SomeOtherType.SomeMethod(string,int)" /> for more details.
///     </para>
/// </remarks>
```

**Example** (without member parameters for non-overloaded members):

```c#
/// <remarks>
///     <para>
///         See <see cref="SomeOtherType.SomeMethod /> for more details.
///     </para>
/// </remarks>
```

**Example** (with reference to type only, without a referenced member):

```c#
/// <remarks>
///     <para>
///         See <see cref="SomeOtherType" /> for more details.
///     </para>
/// </remarks>
```

#### `see` (external reference)

**Type**: Inline element.

**Purpose**: Links to an external information.

**Attributes**:

- `href`; Mandatory; The URL to the external information.

**Example** (with the URL itself as the text):

```c#
/// <remarks>
///     <para>
///         See <see href="https://en.wikipedia.org/wiki/Radix_sort" />.
///     </para>
/// </remarks>
```

**Example** (with a separate text):

```c#
/// <remarks>
///     <para>
///         See <see href="https://en.wikipedia.org/wiki/Radix_sort">Radix sort</see>.
///     </para>
/// </remarks>
```

#### `c`

**Type**: Inline element.

**Purpose**: Used for inline monospace/code elements.

**Attributes**: None.

**Example**:

```c#
/// <remarks>
///     <para>
///         Use the GUID <c>e54dcff7-f8f3-4a11-9d17-1cf7decd880e</c>.
///     </para>
/// </remarks>
```

## Preprocessor

### Indentations

Never indent preprocessor directives, regardless what code they are applied to.

Correct:

```c#
public void DoSomething ()
{
#if PLATFORM_WINDOWS
	// ... some code which depends on a Windows-only library
#elif PLATFORM_LINUX
	// ... some code which depends on a Linux-only library
#else
#error "Platform not defined!"
#endif
}
```

Incorrect:

```c#
public void DoSomething ()
{
	#if PLATFORM_WINDOWS
		// ... some code which depends on a Windows-only library
	#elif PLATFORM_LINUX
		// ... some code which depends on a Linux-only library
	#else
		#error "Platform not defined!"
	#endif
}
```

### Empty lines

Never add unnecessary empty lines before or after preprocessor directives.

Correct:

```c#
public void DoSomething ()
{
#if PLATFORM_WINDOWS
	// ... some code which depends on a Windows-only library
#elif PLATFORM_LINUX
	// ... some code which depends on a Linux-only library
#else
#error "Platform not defined!"
#endif
}
```

Incorrect:

```c#
public void DoSomething ()
{
    
#if PLATFORM_WINDOWS
	// ... some code which depends on a Windows-only library
#elif PLATFORM_LINUX
	// ... some code which depends on a Linux-only library
#else
    
#error "Platform not defined!"
    
#endif

}
```

### Conditional compilation

Never use conditional compilation, such as the following preprocessor directives:

`#if`, `#else`, `#elif`,  `#endif`, `#define`, `#undef`

Exception: For compilation differences between debug and release versions.

Example:

```c#
#if DEBUG
[assembly: AssemblyConfiguration("DEBUG")]
#else
[assembly: AssemblyConfiguration("RELEASE")]
#if !RELEASE
#warning "RELEASE not specified but used."
#endif
#endif
```

Exception: For platform-specific code *which cannot be dynamically selected at runtime*.

Example:

```c#
public void DoSomething ()
{
#if PLATFORM_WINDOWS
	// ... some code which depends on a Windows-only library
#elif PLATFORM_LINUX
	// ... some code which depends on a Linux-only library
#else
#error "Platform not defined!"
#endif
}
```

### Warnings and errors

Never use warning and errors, such as the following preprocessor directives:

`#warning`, `#error`

Exception: In combination with conditional compilation to indicate unknown/undefined situations.

### Line override

Never use line number override, such as the following preprocessor directives:

`#line`

Exception: For auto-generated code which is generated by a template or tool.

### Compiler pragmas

Never use compiler pragmas, such as the following preprocessor directives:

`#pragma`, `#pragma checksum`, `#pragma warning`

Exception: `#pragma warning` to disable a compiler warning *with documented rationale*.

Example:

```c#
// Disabled CS0649 because ...
#pragma warning disable 0649
			// ... some code which generates a warnung but should not
#pragma warning restore 0649
```

## Templates

The styling and formatting, both code and comments, in this section overrules all other code examples.

### Expressions

#### `checked`

```c#
checked(someValue + 10)
```

#### `unchecked`

```c#
unchecked(someValue + 10)
```

#### `default`

```c#
default(T)
```

#### `nameof`

```c#
nameof(this.SomeProperty)
```

#### `sizeof`

```c#
sizeof(int)
```

#### `typeof`

```c#
typeof(int)
```

#### `await`

```c#
await someTask
```

#### `stackalloc`

```c#
stackalloc int[100]
```

### Statements

#### `throw`

```c#
throw new InvalidOperationException();
```

#### `catch`, `when`

```c#
catch (HttpRequestException e) when (e.Message.Contains("404"))
```

#### `case`, `when`

```c#
case Rectangle r when r.Area > 0:
```

#### `goto`

```c#
goto someLabel;
```

#### `return`

```c#
return someValue;
```

#### `yield return`

```c#
yield return someValue;
```

### Blocks

#### `do...while`

```c#
do
{
    ...
} while (device.IsBusy)
```

#### `while`

```c#
while (device.IsBusy)
{
    ...
}
```

#### `if`, `else`

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

#### `for`

```c#
for (int index = 0; index < this.Customers.Count; index++)
{
    ...
}
```

#### `foreach`

```c#
foreach (var customer in this.Customers)
{
    ...
}
```

#### `switch`, `default`, `case`

```c#
switch (args[0])
{
    default:
        ...
        break;

    case abc:
        ...
        break;

    case xyz:
        ...
        break;
}
```

#### `fixed`

```c#
fixed (int* p = &pt.x)
{
    ...
}
```

#### `lock`

```c#
lock (this.SyncRoot)
{
    ...
}
```

#### `unsafe`

```c#
unsafe
{
    ...
}
```

#### `using`

```c#
using (MemoryStream ms = new MemoryStream())
{
    ...
}
```

#### `try`, `catch`, `finally`

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

#### `checked`

```c#
checked
{
    ...
}
```

#### `unchecked`

```c#
unchecked
{
    ...
}
```

### Types

#### `class`

```c#
/// <summary>
///     Implements a list of random items.
/// </summary>
/// <typeparam name="T"> The type of random items stored in the list. </typeparam>
/// <remarks>
///     <para>
///         The random list is automatically filled with randomized items.
///     </para>
///     <note type="note">
///         This is just an example.
///         It is just nonsense so you focus on the actual template.
///     </note>
/// </remarks>
/// <threadsafety static="false" instance="false" />
/// <example>
///     <code language="cs">
/// <![CDATA[
/// RandomList<string> rl = new RandomList<string>();
/// ...
/// ]]>
///     </code>
/// </example>
public class RandomList <T> : Collection<T>, IRandomList<T>
 where T : new()
{
	...
}
```

#### `struct`

```c#
/// <summary>
///     Implements a random tuple.
/// </summary>
/// <typeparam name="TKey"> The type of the key element. </typeparam>
/// <typeparam name="TValue"> The type of the value element. </typeparam>
/// <remarks>
///     <para>
///         The random tuple is automatically filled with a randomized key and value.
///     </para>
///     <note type="note">
///         This is just an example.
///         It is just nonsense so you focus on the actual template.
///     </note>
/// </remarks>
/// <threadsafety static="false" instance="false" />
/// <example>
///     <code language="cs">
/// <![CDATA[
/// RandomTuple<int, double> rl = RandomTuple<int, double>();
/// ...
/// ]]>
///     </code>
/// </example>
public struct RandomTuple <TKey, TValue> : IEquatable<RandomTuple<TKey, TValue>>
 where TKey : new()
 where TValue : new()
{
	...
}
```

#### `interface`

```c#
/// <summary>
///     Defines the interface for a list of random items.
/// </summary>
/// <typeparam name="T"> The type of random items stored in the list. </typeparam>
/// <remarks>
///     <note type="implement">
///         The random list should be automatically filled with randomized items.
///     </note>
///     <note type="note">
///         This is just an example.
///         It is just nonsense so you focus on the actual template.
///     </note>
/// </remarks>
/// <threadsafety static="false" instance="false" />
public interface IRandomList <T> : IList<T>, IList
 where T : new()
{
	...
}
```

#### `enum`

```c#
/// <summary>
///     Defines the state of a device.
/// </summary>
/// <remarks>
///     <para>
///         Any device can have any state at any time.
///     </para>
///     <note type="note">
///         This is just an example.
///         It is just nonsense so you focus on the actual template.
///     </note>
/// </remarks>
public enum DeviceState
{
	/// <summary>
	///     The device status is unknown (check connection state).
	/// </summary>
    Unknown = 0,
    
    /// <summary>
	///     The device is powered-off.
	/// </summary>
    Off = 1,
    
    /// <summary>
	///     The device is powered-on but does nothing.
	/// </summary>
    Idle = 2,
    
    /// <summary>
	///     The device working hard!
	/// </summary>
    Working = 3,
}
```

#### `delegate`

```c#
/// <summary>
///     Defines the callback which decides whether an item is worthy or not.
/// </summary>
/// <typeparam name="T"> The type of item whose worthyness is checked. </typeparam>
/// <param name="item"> The item whose worthyness is checked. </param>
/// <returns>
///     true if the item passed by <paramref name="item" /> is worthy,
///     false otherwise or if <paramref name="item" /> is null.
/// </returns>
/// <remarks>
///     <note type="implement">
///         The worthyness is decided randomly.
///     </para>
///     <note type="note">
///         This is just an example.
///         It is just nonsense so you focus on the actual template.
///     </note>
/// </remarks>
public delegate bool RandomPredicate <T> (T item) where T : class;
```

### Members

#### Constants (`const`)

```c#
/// <summary>
///     The default separator between a name and its value.
/// </summary>
/// <remarks>
///     <para>
///         The default value is <c> = </c>.
///     </para>
/// </remarks>
public const char DefaultNameValueSeparator = '=';
```

#### Constructors

```c#
/// <summary>
///     Creates a new instance of <see cref="IniReader" />.
/// </summary>
/// <param name="reader"> The used <see cref="TextReader" />. </param>
/// <remarks>
///     <para>
///         INI reader settings with default values are used.
///     </para>
/// </remarks>
/// <exception cref="ArgumentNullException">
///     <paramref name="reader" /> is null.
/// </exception>
public IniReader (TextReader reader)
	: this(reader, null)
{
}

/// <summary>
///     Creates a new instance of <see cref="IniReader" />.
/// </summary>
/// <param name="reader"> The used <see cref="TextReader" />. </param>
/// <param name="settings"> The used INI reader settings. </param>
/// <exception cref="ArgumentNullException">
///     <paramref name="reader" /> is null.
/// </exception>
public IniReader (TextReader reader, IniReaderSettings settings)
{
    ...
}
```

#### Finalizers (`~`)

```c#
/// <summary>
///     Garbage collects this instance of <see cref="IniReader" />.
/// </summary>
/// <remarks>
///     <para>
///         The finalizer calls <see cref="Dispose(bool)" />.
///     </para>
/// </remarks>
~IniReader ()
{
    this.Dispose(false);
}
```

#### Fields

```c#
/// <summary>
///     The sigma or standard deviation of all values in the history.
/// </summary>
/// <remarks>
///     <para>
///         The default value is <c> 0.0 </c>.
///     </para>
/// </remarks>
public double Sigma;
```

#### Indexer (`this`)

```c#
/// <summary>
///     Gets or sets the item at a specified index.
/// </summary>
/// <param name="index"> The zero-based index. </param>
/// <returns>
///     The item at <paramref name="index" />.
/// </returns>
/// <value>
///     The item at <paramref name="index" />.
/// </value>
/// <exception cref="ArgumentOutOfRangeException">
///     <paramref name="index" /> is outside the range.
/// </exception>
public T this [int index]
{
	get
    {
    	...
    }
    set
    {
    	...
    }
}

/// <summary>
///     Gets or sets the item at a specified index.
/// </summary>
/// <param name="index"> The zero-based index. </param>
/// <returns>
///     The item at <paramref name="index" />.
/// </returns>
/// <value>
///     The item at <paramref name="index" />.
/// </value>
/// <exception cref="ArgumentOutOfRangeException">
///     <paramref name="index" /> is outside the range.
/// </exception>
public T this [int index]
{
	get => ... ;
	set => ... ;
}
```

#### Properties (`get`, `set`)

```c#
/// <summary>
///     Gets or sets the power of the spaceship laser in kilowatts.
/// </summary>
/// <value>
///     The power of the spaceship laser in kilowatts or 0 if the laser is disabled.
/// </value>
/// <remarks>
///     <para>
///         The default value is <c> 0 </c>.
///     </para>
/// </remarks>
/// <exception cref="ArgumentOutOfRangeException">
///     <paramref name="value" /> is below zero.
/// </exception>
public int LaserPowerKilowatts
{
	get
    {
    	...
    }
    set
    {
    	...
    }
}

/// <summary>
///     Gets or sets the power of the spaceship laser in kilowatts.
/// </summary>
/// <value>
///     The power of the spaceship laser in kilowatts or 0 if the laser is disabled.
/// </value>
/// <remarks>
///     <para>
///         The default value is <c> 0 </c>.
///     </para>
/// </remarks>
/// <exception cref="ArgumentOutOfRangeException">
///     <paramref name="value" /> is below zero.
/// </exception>
public int LaserPowerKilowatts
{
	get => ... ;
	set => ... ;
}

/// <summary>
///     Gets the maximum power of the spaceship laser in kilowatts.
/// </summary>
/// <value>
///     The maximum power of the spaceship laser in kilowatts.
/// </value>
public int LaserPowerMaxKilowatts
{
	get
    {
    	...
    }
}

/// <summary>
///     Gets the maximum power of the spaceship laser in kilowatts.
/// </summary>
/// <value>
///     The maximum power of the spaceship laser in kilowatts.
/// </value>
public int LaserPowerMaxKilowatts => ... ;
```

#### Events (`event`, `add`, `remove`)

```c#
/// <summary>
///     Raised after a request message was received.
/// </summary>
public event EventHandler<BusMessageEventArgs> ReceivingRequest;

/// <summary>
///     Raised after a database connection has changed.
/// </summary>
event EventHandler<ConnectionChangedEventArgs> IDatabaseManager.ConnectionChanged
{
	add
	{
		...
	}
	remove
	{
		...
	}
}
```

#### Methods

```c#
/// <summary>
///     Gets the first resolved value for the specified export name.
/// </summary>
/// <typeparam name="T"> The type of the resolved value. </typeparam>
/// <param name="exportName"> The export name which is resolved. </param>
/// <returns>
///     The first resolved value.
/// </returns>
/// <remarks>
///     <para>
///         <paramref name="exportName"/> can also be a type name.
///     </para>
/// </remarks>
/// <exception cref="CompositionException">
///     The resolving failed.
/// </exception>
public T GetExport <T> (string exportName)
{
    ...
}

/// <summary>
///     Gets the first resolved value for the specified export name.
/// </summary>
/// <typeparam name="T"> The type of the resolved value. </typeparam>
/// <param name="exportName"> The export name which is resolved. </param>
/// <returns>
///     The first resolved value.
/// </returns>
/// <remarks>
///     <para>
///         <paramref name="exportName"/> can also be a type name.
///     </para>
/// </remarks>
/// <exception cref="CompositionException">
///     The resolving failed.
/// </exception>
public T GetExport <T> (string exportName) => ... ;
```

#### Unary operators (`operator`)

```c#
/// <summary>
///     Decrements a <see cref="RomanNumber" /> by 1.
/// </summary>
/// <param name="x"> The value. </param>
/// <returns>
///     The result.
/// </returns>
public static RomanNumber operator -- (RomanNumber x)
{
	...
}
```

#### Binary operators (`operator`)

```c#
/// <summary>
///     Adds two <see cref="RomanNumber" />s.
/// </summary>
/// <param name="x"> The first value. </param>
/// <param name="y"> The second value. </param>
/// <returns>
///     The result.
/// </returns>
public static RomanNumber operator + (RomanNumber x, RomanNumber y)
{
	...
}
```

