---
description: Architecture of executable file for the Insomnia virtual machine
---

# Architecture InsomniaELF

## How to read ELF of Insomnia

Use default ELF reader.

{% hint style="warning" %}
 All Insomnia IL code is contained in **.code** elf section.
{% endhint %}

After reading elf **.code** section, following instructions to decode the IL Code

```csharp
// read module name index (size 4)
var name_index = read4();
```

Next, reading const-string dictionary of key: int, value: string.

```csharp
// read constants srting dictionary size
var strings_storage_size = read4();

// for(i = 0; i != strings_storage_size; i++)
var key = read4();
var size = read4(); // size of string (bytes)
var magic = read2(); // 0x45, validate this
var body = readBytes(size); // body string
var str = utf8.toString(body);
storage.add(key, str);
```

Next, reading classes body.

```csharp
// read list size
var size_of_classes = read4();

// for(i = 0; i != size_of_classes; i++)
var size_body = read4();
var name_index = read4();
var namespace_index = read4();
var flags = readByte(); // See ClassFlags
var parentIdx = read8(); // reading index of parent class, if present
```

Next, read methods

```csharp
// read list size
var size_of_methods = read4();

// for(i = 0; i != size_of_methods; i++)
var bytes_size = read4();
var name_index = read4();
var flags = readByte(); // see MethodFlags
var body_size = read4();
var stack_size = readByte();
var locals_size = readByte();
var return_type_inx = read8();

// read arguments 
var size_of_method_argument = read4();
// for(i = 0; i != size_of_method_argument; i++)
var name_idx = read4();
var type_idx = read8();

// read IL body 
var body = readBytes(body_size);
```

Next, read class fields

```csharp
var size_of_fields = read4();

// for(i = 0; i != size_of_fields; i++)
var fieldNameIdx = read8();
var type_idx = read8();
var flags = readByte(); // See FieldFlags

// read literal value 
// (if type code from FieldType has primitive and flags.Has(Literal))
var size = read4();
var bytes = readBytes(size);
// marshal 'bytes' as primitive type if present
```

