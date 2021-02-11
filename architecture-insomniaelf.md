---
description: Architecture of executable file for the Insomnia virtual machine
---

# Architecture InsomniaELF

## How to read ELF of Insomnia

Use default ELF reader.

{% hint style="info" %}
 All Insomnia IL code contains in .code elf section.
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
```

