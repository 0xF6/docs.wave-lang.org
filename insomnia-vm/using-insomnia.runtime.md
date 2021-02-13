---
description: using insomnia.runtime package for building application code.
---

# Insomnia.Runtime

## Install package

{% hint style="info" %}
Current runtime support only C\# library
{% endhint %}

```text
dotnet add package insomnia.vm.runtime
```

## Sample code

{% hint style="warning" %}
All Insomnia IL code is contained in **.code** elf section
{% endhint %}

{% hint style="warning" %}
All namespace must start with **global::**

_'global::name/space/ClassName'_
{% endhint %}

```csharp
using wave.emit;
using static wave.emit.MethodFlags;
using static wave.emit.WaveTypeCode;
// ..

// create instance of InsomniaAssembly
var asm = new InsomniaAssembly
{
    Name = "wave_test"
};
// create instance of ModuleBuilder
var foo_module = new ModuleBuilder("foo");

// create instance of ClassBuilder
var clazz = module.DefineClass("global::baz/theClass");

// See MethodFlags

var name = "FooFunction";
// See MethodFlags
var flags =  Static | Public;
// See WaveTypeCode
var returnType = TYPE_VOID.AsType();
var argument = ("value", TYPE_STRING);

var method = clazz.DefineMethod(name, flags, returnType, argument);

// require IL Generator
var body = method.GetGenerator();

// transform the conditional pseudocode into IL
// debug.print((1448+228)^2);
body.Emit(OpCodes.LDC_I4_S, 1448);
body.Emit(OpCodes.LDC_I4_S, 228);
body.Emit(OpCodes.ADD);
body.Emit(OpCodes.LDC_I4_S, 2);
body.Emit(OpCodes.XOR);
body.Emit(OpCodes.DUMP_0);
body.Emit(OpCodes.RET);


// baking bytes from foo_module
asm.AddSegment((".code", foo_module.BakeByteArray()));
InsomniaAssembly.WriteToFile(asm, 
    new DirectoryInfo("./"));

```

