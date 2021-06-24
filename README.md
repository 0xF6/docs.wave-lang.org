<!-- warning -->
<p align="center">
  <a href="#">
    <img src="https://user-images.githubusercontent.com/13326808/118900923-c3c9c280-b91a-11eb-94f3-691feb53e0f4.png">
  </a>
</p>

<!-- Logo -->
<p align="center">
  <a href="#">
    <img src="https://user-images.githubusercontent.com/13326808/118315186-dba9dc80-b4fd-11eb-8d2f-32e8313ba6a7.png">
  </a>
</p>

<p align="center">
  <a href="#">
    <img height="128" wight="128" src="https://user-images.githubusercontent.com/13326808/119747309-2252eb80-be9b-11eb-8bcc-2613658162a7.png">
  </a>
</p>

<!-- Name -->
<h1 align="center">
 ⚡️🔮 Mana Lang 🔮⚡️
</h1>

<!-- classic badges -->
<p align="center">
  <a href="https://www.codacy.com/gh/0xF6/mana_lang/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=0xF6/mana_lang&amp;utm_campaign=Badge_Grade">
    <img src="https://app.codacy.com/project/badge/Grade/9dc3cb6f384747c39d0b83241e725de2">
  </a>
  <a href="https://www.codacy.com/gh/0xF6/mana_lang/dashboard?utm_source=github.com&utm_medium=referral&utm_content=0xF6/mana_lang&utm_campaign=Badge_Coverage">
    <img src="https://app.codacy.com/project/badge/Coverage/9dc3cb6f384747c39d0b83241e725de2">
  </a>
  <a href="#">
    <img src="http://img.shields.io/:license-MIT-blue.svg">
  </a>
<a href="https://app.fossa.com/projects/git%2Bgithub.com%2F0xF6%2Fwave_lang?ref=badge_shield" alt="FOSSA Status"><img src="https://app.fossa.com/api/projects/git%2Bgithub.com%2F0xF6%2Fwave_lang.svg?type=shield"/></a>
  <a href="https://github.com/0xF6/wave_lang/releases">
    <img src="https://img.shields.io/github/release/0xF6/mana_lang.svg?logo=github&style=flat">
  </a>
</p>
<!-- popup badges -->
<p align="center">
  <a href="https://t.me/ivysola">
    <img src="https://img.shields.io/badge/Ask%20Me-Anything-1f425f.svg?style=popout-square&logo=telegram">
  </a>
</p>

<!-- big badges -->
<p align="center">
  <a href="#">
    <img src="https://forthebadge.com/images/badges/0-percent-optimized.svg">
    <img src="https://forthebadge.com/images/badges/ctrl-c-ctrl-v.svg">
    <img src="https://forthebadge.com/images/badges/kinda-sfw.svg">
    <img src="https://forthebadge.com/images/badges/powered-by-black-magic.svg">
  </a>
</p>
<p align="center">
  <a href="#">
    <img src="https://forthebadge.com/images/badges/works-on-my-machine.svg">
  </a>
</p>


---

> Mana is an open source high-level strictly-typed programming language with a standalone OS, arm and quantum computing support.

---

## OS Support

OS                            | Version                       | Architectures
------------------------------|-------------------------------|----------------
Windows 10                    | 1607+                         | x64, ARM64
OSX                           | 10.14+                        | x64
Linux                         |                               | x64, ARM64


## Compiling from source

### Building on Windows

For building, you need the following tools:
- dotnet 6.0
- Win10 SDK
- vsbuild-tools-2019 with MSVC 2019, MSVC142 for ARM64


Checkout mana sources
```bash
git clone git://github.com/0xf6/mana_lang.git --recurse-submodules
cd mana lang
git fetch --prune --unshallow --tags

dotnet restore
```

#### Compile IshtarVM
Go to ishtar folder
```base
cd .\backend\mana.backend.ishtar.light
```
Compile for Windows 10 x64
```bash
dotnet publish -r win10-x64 -c Release
```
Compile for Windows 10 ARM64
```
dotnet publish -r win-arm64 -c Release
```

Copy output files
```bash
mkdir output
cp -R ./backend/mana.backend.ishtar.light/bin/net6.0/win10-x64/native/ ./output
```

The `output` folder should contain:
- ishtar.exe - main ishtar file
- ishtar.exp - export metadata for main module
- ishtar.lib - dynamic library for main module
- ishtar.pdb - debug symbols


#### Compile manac
Go to mana compiler folder
```base
cd .\compiler
```
Compile
```
dotnet publish -r win-x64 -c Release
```
Copy the output files
```bash
mkdir output
cp -R ./bin/Release/net6.0/win-x64/publish ./output
```

The `output` folder should contain:
- manac.exe - main executable compiler file


### Building on Linux (on ubuntu)

For building, you need the following tools:
- dotnet 6.0
- clang
- zlib1g-dev
- libkrb5-dev
- libssl-dev

Checkout mana sources
```bash
git clone git://github.com/0xf6/mana_lang.git --recurse-submodules
cd mana lang
git fetch --prune --unshallow --tags

dotnet restore
```


#### Compile IshtarVM
Go to ishtar folder
```base
cd .\backend\mana.backend.ishtar.light
```
Compile for Linux x64
```bash
dotnet publish -r linux-x64 -c Release
```
Compile for Linux ARM64
```
dotnet publish -r linux-arm64 -c Release
```

Copy output files
```bash
mkdir output
cp -R ./backend/mana.backend.ishtar.light/bin/Release/net6.0/linux-x64/native ./output
```

#### Compile manac
Go to mana compiler folder
```base
cd .\compiler
```
Compile
```
dotnet publish -r linux-x64 -c Release
```
Copy output files
```bash
mkdir output
cp -R ./bin/Release/net6.0/linux-x64/publish ./output
```

The `output` folder should contain:
- manac - main executable compiler file

## Contributing

We welcome everyone to contribute to mana language.
To do so, you need to know a couple of things about the folder structure::

```yaml
/backend: folder contains all backend vm\generator for mana
  /clr: variant generator for CLR VM
  /hashlink: variant generator for Hashlink VM
  /LLVM: variabnt generator for LLVM toolstack
  /ishtar.generator: variant generator for IshtarVM
  /ishtar.light: implementation of ishtar vm in C#
/compiler: folder contains source for mana compiler
/ide_ext: visual code extension sources
/lib: folder with common libraries
  /ast: mana AST library, for parsing
  /projectsystem: project system models, for compiler
/lsp: language server for mana lang
/mana.std: standard library sources
/samples: Wow! its samples!
/test: folder with various tests
```

You can run all tests from the root directory with `dotnet test`.

To recompile the vm and the compiler: `dotnet build`.

To recompile the standard library: `manac ./mana.std/corlib.wproj`.

After your changes are done, please remember to run `dotnet format` to guarantee all files are properly formatted and
then run the full suite with `dotnet test`.

## Q\A

```yaml
Q:
  Why is it called mana?
A:
  I liked it very much 🗿🗿🗿
  So, I tried to choose a memorable name that would be easy
  simple for the tools (like the 'rune' package manager).
  The original name was Wave Lang, but I didn't like it, 
  and it was chosen at random 🙂.

Q:
  Why it based on C#?
A:
  Initially, i started developing a virtual machine in C++,
  but there were a lot of difficulties with basic things (such as collections, text formatting, etc.)
  And at some point i saw that microsoft began to develop a fully AOT compiler for dotnet.
  That means we could write in pure C# without using runtime and std, 
  which allows everyone to write such hard things like an OS!
  So I decided - that's it! I'm Definitely writing a virtual machine in C#!

  So, now I'm developing using the C# runtime and the std, but 
  in version 2.0 I'm planning to completely move away from runtime dependencies.

Q:
  This language really support quantum computing?
A:
  Not now, but in future I'm planning to add support for Microsoft Quantum Simulator, 
  next - support for Azure Qunatum or IBM quantum cloud.
  And after the release of stationary quantum extension card (like PCEx128 😃), 
  I'll add support for them too.


```
## Special Thanks

<p align="center">
  <a href="https://www.jetbrains.com/?from=mana_lang">
    <img height="128" wight="128" src="https://raw.githubusercontent.com/0xF6/mana_lang/master/.github/images/jetbrains-variant-3.png">
  </a>
</p>


## License

Mana is primarily distributed under the terms of both the MIT license and the Apache License (Version 2.0),
with portions covered by various BSD-like licenses.

Check LICENSE files for more information.

## Support
<p align="center">
   <a href="https://ko-fi.com/P5P7YFY5">
    <img src="https://www.ko-fi.com/img/githubbutton_sm.svg">
  </a>
</p>


