# PART I - C# rules

The rules in this part are C# programming language rules which define how the C# programming language is to be used, independent of used frameworks, libraries, architecture, design, and functionality.

[TOC]

## Language

Always use English language for all identifiers, names, and comments.

## Casing

Always use lowerCamelCase (e.g. `orderTotal`) for:

* Local variables
* Iteration variables
* Method parameters
* Lambda parameters

Always use UpperCamelCase (e.g. `GetOrders`) for:

* All type names
* All type members

Always use lowerCamelCase  with leading underscore (e.g. `_orders`) for:

* Private fields

Always use UpperCamelCase with punctuation (e.g. `Company.Product.Something`) for:

* Assembly names
* Namespaces

Never...

* ...use all uppercase (e.g. `GETORDERS`).
* ...use all lowercase (e.g. `ordertotal`), except for properly lowerCamelCased identifiers of one word.

## Naming

### Characters

Never...

- ...use underscores (e.g. `_my_precious_value`), except as prefix for private fields.
- ...use any other character than uppercase letters (`A-Z`), lowercase letters (`a-z`), and numbers (`0-9`).
- ...use numbers (`0-9`) at the beginning of names.

### Prefixes

Never use prefixes (e.g. `EMyEnum`, `m_someField`, `CMyClass`) except for interfaces and private fields.

### Suffixes

Never use suffixes (e.g. `someText_str`, `MyClassC`).

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

Exception: Technical composition can be part of a name if it is part of the intention (e.g. the same data available in two different formats).

Example:

```c#
public byte[] ConvertToByteArray (string value) {...}
public int ConvertToInt32 (string value) {...}
```

### Length

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

Never use abbreviations unless they shorten excessive names and are well known.

Correct:

```c#
int numberOfItems = 12;

Encoding Utf8 { get; set; }
```

Incorrect:

```c#
int noItems = 12;

Encoding UnicodeTransformationFormat8 { get; set; }
```

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

Exception: The name `IO` can be used for I/O as this is also used in the .NET base class library.

Example:

```c#
namespace MyCompany.MyProduct.Utilities.IO {...}
```

### Negations

Never use negated names.

Correct:

```c#
public bool IsAllowed { get; private set; }
```

Incorrect:

```c#
public bool IsNotAllowed { get; private set; }
```

### Namespaces

#### Conflicts

Never start a namespace with a conflicting name, such as `System`, `Microsoft`, or other well-known names.

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

### Types

#### Conflicts

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

#### Unambiguousness

Never use a name for a type which is already used or which is too general.

Correct:

```c#
public sealed class IceCreamDeviceManager {...}
```

 Incorrect:

```c#
public sealed class DeviceManager {...}
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

#### Interfaces

Always prefix the name of an interface with `I`.

Correct:

```c#
public interface IMyInterface {...}
```

Incorrect:

```c#
public interface MyInterface {...}
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

Exception: A methods intention can be described with a verb only if it is meaningful when the corresponding type or the usage context acts as the object.

Example:

```c#
//class: LaserBeam
public void Fire () {...}
```

#### Return values

Always use a name which indicates that a method has a return value and which describes it properly.

Always use one of the following prefixes if a methods main intention is to deliver an *existing* value:

* `Get`

Always use one of the following prefixes if a methods main intention is to *retrieve* or *compute* a value:

* `Retrieve`
* `Determine`
* `Compute`
* `Calculate`

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

### Properties

#### Object naming

Always use a object for property names.

Correct:

```c#
public int OrderCount { get; set; }
```

Incorrect:

```c#
public int GetOrderCount { get; set; } //implies method by adding a verb
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

### Miscellaneous

#### Boolean values

Always use one of the following prefixes, using proper casing, for boolean values:

- `Is`, `is`
- `Has`, `has`
- `Contains`, `contains`
- `Can`, `can`
- `Should`, `should`
- `Must`, `must`
- `Allows`, `allows`
- `Supports`, `supports`

Example:

```c#
public bool IsStarted { get; private set;}

public bool CanLogin (string username) {...}

bool hasOrders = true;
```

#### Computational values

Always use one of the following suffixes for computational values:

- `Count`
- `Sum`
- `Min`
- `Max`
- `Average`
- `Median`

Example:

```c#
int itemCount = someList.Count;

public double CustomersPerHourAverage { get; set; }
```

#### Values with units

Always use the corresponding unit suffix for values with units.

Correct:

```c#
public Image DownloadImage (string url, int timeoutMilliseconds) {...}

public void FireLaser (double powerKilowatts) {...}
```

Incorrect:

```c#
public Image DownloadImage (string url, int timeout) {...}

public void FireLaser (double power) {...}
```

#### UI controls

Always use suffixes for UI values which match the type of the UI control.

Never use prefixes for UI values.

Correct:

```c#
public Label FirstNameLabel { get; set; }
public Label LastNameLabel { get; set; }
```

Incorrect:

```c#
public Label lblFirstName { get; set; }
public Label LastName { get; set; }
```

#### Regions

Always use simple region names which describe the content of the region but not its behavior or intention.

Correct:

```c#
#region Properties
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

## Style & Formatting

### Source code files

#### File structure

Always use the following structure in a source code file:

* File header (optional)
* `using` directives
* `namespace` declaration
* Actual content or type definition respectively

Never include the following in the file header:

* The file name
* The file location
* The project name
* The solution name
* Any namespace names
* Any type names
* Any version information
* Any history or change log information
* Any author information

Correct:

```c#
// FILE HEADER

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
    
    // FILE HEADER
	// File:    D:\Workfolder\MyProduct\MyCompany.MyProduct.Utilities\StringUtilities.cs
	// Version: 1.1
	// Author:  Joe

	public static class StringUtilities {...}
}
```

#### One type per file

Always put each type in its own source code file which is named exactly as the type (even `delegate` types).

Never put more than one type in a source code file.

Exceptions:

- Nested types (more than one type per source code file).
- Partial classes (one type in more than one source code file).

#### One namespace per file

Never declare more than one namespace per file.

### `using` directives

#### Grouping

Always group `using` directives according to the namespaces in ascending depth and sorted alphabetically.

Always group `using` directives according to the following structure:

1. Framework namespaces
2. Third-party library namespaces
3. Own library namespaces
4. Namespaces with the same root as the type in the source code file

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

Never put using directives inside a namespace.

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

### `#region` blocks

#### Usage of regions

Always use regions to group members of a type.

Always use a single separate region per nested type.

[TBD: Which member to group and how to name them]

#### Region scope/level

Always use regions on the level of type members or nested types.

Never use regions in any other scope than type members or nested types.

Correct:

```c#
namespace MyCompany.MyLibrary.Utilities
{
	public static class FileUtilities
    {
    	#region Properties
    	...
    	#endregion
    	
    	#region Methods
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
    	#region Properties
    	...
    	#endregion
    	
    	#region Methods
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
    	#region Properties
    	...
    	#endregion
    	
    	#region Methods
    	...
    	#endregion
    	
    	#region SomeNestedClass
    	private sealed class SomeNestedClass
    	{
    		#region Properties
    		...
    		#endregion
    	
    		#region Methods
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
```

Incorrect:

```c#
Int32 orderTotal = 0;

String customerId = null;
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

public sealed class AppleOrangeComparer : IComparer, SomeBadlyDesignedLibrary.IComparer {...}
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

### Variables

#### `var` usage

Never use `var` except for `foreach` iterator variables.

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

Always declare a variable as close to its first use as possible and in the narrowest scope possible.

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

### Statements

#### Object initializers

[TBD]

#### Anonymous methods

[TBD]

#### Lambda expressions

[TBD]

### Braces & Parenthesis

#### Mandatory braces

Always use curly braces with control statements (e.g. `if`, `for`) or for object initializers, even for one line statement blocks.

Correct:

```c#
if (orders.Count == 0)
{
    this.ShowWarning("Customer never ordered anything.");
}
```

Incorrect:

```c#
if (orders.Count == 0)
    this.ShowWarning("Customer never ordered anything.");
```

#### Separate lines

Always put curly braces on their own line and properly indented.

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

if (orders.Count == 0)
	{
    this.ShowWarning("Customer never ordered anything.");
	}
```

Exception: Automatic properties.

Example:

```c#
public bool IsRunning { get; private set; }
```

#### Explicit operator precedence

Always use parenthesis to explicitly express the precedence of operators:

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

Always use tabs. Or spaces. It doesn't matter. Choose one and then *stick* to it. So use tabs. Or spaces.

#### Spaces

Always put *one* space before:

* Opening parentheses (`(`) of control statements (e.g. `if`, `for`).
* Binary operators (e.g. `==`, `+`).

Never put spaces before:

* Closing parentheses (`)`) of control statements (e.g. `if`, `for`).
* Unary operators (e.g. `++`, `--`).

Always put *one* space after:

* Binary operators (e.g. `==`, `+`).

Never put spaces after:

* Opening parentheses (`(`) of control statements (e.g. `if`, `for`).

#### Empty lines

Always put empty lines between (number of empty lines stated in parentheses):

* File header and `using` groups (4).
* `using` groups with different namespace roots (1).
* `using` groups and the `namespace` declaration (4).
* Each member (including nested types) of a type; comments are considered part of the member (1).
* Two regions (1).

Never put empty lines between:

* A comment and the type or member its commenting/describing.

#### Indentations

[TBD]

Always increment the indentation level after:

* `namespace`

Never increment the indentation level after:

* `#region`

## Comments

[TBD]