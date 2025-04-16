
# 📘 Lua Annotation Cheat Sheet

> For use with `lua-language-server` (Sumneko / Lua LS) — great for Neovim plugins, config files, and general Lua projects.

---

## 🔹 1. Primitive Types

```lua
---@type string
local title = "My Project"

---@type number
local version = 1.0

---@type boolean
local enabled = true

---@type nil
local nothing = nil

---@type any
local dynamic_value
```

---

## 🔹 2. Tables

### ➤ Array-style Table

```lua
---@type string[]
local names = { "Alice", "Bob" }
```

### ➤ Dictionary-style Table (Maps)

```lua
---@type table<string, number>
local scores = {
  alice = 95,
  bob = 82
}
```

### ➤ Nested Table Type (Generic-style)

```lua
---@type table<string, string[]>
local categorized = {
  fruits = { "apple", "banana" },
  colors = { "red", "blue" }
}
```

---

## 🔹 3. Classes and Structures

### ➤ Defining a Class

```lua
---@class User
---@field name string
---@field age number
---@field is_active boolean
```

### ➤ Using a Class

```lua
---@type User
local admin = {
  name = "Andrew",
  age = 21,
  is_active = true
}
```

---

## 🔹 4. Function Annotations

### ➤ Simple Parameters and Returns

```lua
---@param a number
---@param b number
---@return number
local function add(a, b)
  return a + b
end
```

### ➤ Optional Parameters

```lua
---@param name string
---@param age? number
---@return string
local function greet(name, age)
  return age and (name .. ", age " .. age) or name
end
```

### ➤ Multiple Returns

```lua
---@return number, number
local function get_size()
  return 1920, 1080
end
```

---

## 🔹 5. Generics

### ➤ Generic List Access

```lua
---@generic T
---@param list T[]
---@return T
local function get_first(list)
  return list[1]
end
```

### ➤ Generic Key-Value Map

```lua
---@generic K, V
---@param map table<K, V>
---@return K, V
local function get_any(map)
  for k, v in pairs(map) do return k, v end
end
```

---

## 🔹 6. Overloads

```lua
---@overload fun(x: number): number
---@overload fun(x: string): string
local function double(x)
  if type(x) == "number" then
    return x * 2
  elseif type(x) == "string" then
    return x .. x
  end
end
```

---

## 🔹 7. Fields and Modules

### ➤ Annotating Fields in a Class

```lua
---@class Config
---@field path string
---@field debug? boolean
```

### ➤ Annotating Module Table

```lua
---@type table<string, string>
M.keybinds = {}
```

### ➤ Annotating a Module Import

```lua
---@module 'myplugin.utils'
local utils = require("myplugin.utils")
```

---

## 🔹 8. UI/Plugin Config Types (Example)

```lua
---@class TerminalOptions
---@field right_padding integer
---@field left_padding integer
---@field bottom_padding integer
---@field top_padding integer
---@field border boolean
---@field number boolean
---@field relativenumber boolean
---@field scroll boolean

---@param opts TerminalOptions
function setup_terminal(opts)
  -- configuration logic
end
```

---

## 🔹 9. Special Tags

| Tag             | Description                                  |
|----------------|----------------------------------------------|
| `@type`        | Defines the type of a variable                |
| `@param`       | Annotates function parameters                 |
| `@return`      | Annotates function return types               |
| `@class`       | Defines a custom structured type              |
| `@field`       | Describes a property inside a class           |
| `@alias`       | Defines a type alias                          |
| `@generic`     | Supports generics for reusable functions      |
| `@overload`    | Declares multiple valid signatures            |
| `@module`      | Declares an external module name              |
| `@nodiscard`   | Warn if a function return is ignored (LSP)    |
| `@deprecated`  | Marks a symbol as deprecated                  |

---

## 📝 Tips for Real Usage

- ✅ Always annotate modules with `---@type` or `---@class` to make LSP happy.
- 🎯 Use `@param` / `@return` on all exported or complex functions.
- 🔄 Use `@generic` for utility functions like `map`, `filter`, `clone`.
- 📦 Store all type annotations in a `types.lua` file if things get big.
- 💡 Combine with `vim.validate()` or assert functions for runtime safety.

---
