## What is Lua?

[Lua](https://www.lua.org/about.html) is a scripting/programming language developed with the aim of being portable, super fast, and lightweight, while maintaining great flexibility.

This is *not* a tutorial on how to use Lua, and it is assumed that you have some knowledge of Lua and programming in general. If you are new to Lua or programming, there are excellent resources online and can be found through your favourite search engine.

## Lua and PAYDAY 2

A great deal of PAYDAY's codebase is written in Lua. Thanks to it being a high-level language, tools like [SuperBLT](docs/tools/superblt.md) can be created, which allow modders to change the functions and variables written in Lua at runtime of the game.

(The version of LuaJIT PAYDAY 2 uses is `LuaJIT-2.1.0-beta3`. While it is completely not required and useless to most modders, you can be download this file from [the LuaJIT website](https://luajit.org/download.html).)

## Development Environment

The environment you write code in is almost entirely your preference. This guide will not tell you what is best, because what works for you is what is best. However, you will need the following:

* A text editor of your choice

If you're not sure, try [VSCodium](https://vscodium.com/), its free, open source, and super easy.

* [The PAYDAY 2 Decompiled LuaJIT](https://github.com/steam-test1/Payday-2-LuaJIT-Complete)

These are the decompiled Lua files much of the game runs on. You will need these to understand how much of the game works, and to figure out what you are trying to change.


