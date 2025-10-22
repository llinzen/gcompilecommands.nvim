# Compile Commands Generator for Neovim

This is a simple plugin to generate the `compile_commands.json` file.

## Overview

The main purpose of this plugin is to facilitate the generation of the `compile_commands.json` file in Neovim projects, when you don't have access to other tools like [bear](https://github.com/rizsotto/Bear). The `compile_commands.json` file is used by various development tools for static code analysis, auto-completion, and more.

## How to Use

To use this plugin, follow these simple steps:

1. Install this plugin in your Neovim environment using your preferred method (e.g., using a plugin manager like [lazy](https://github.com/folke/lazy.nvim)).
```
{
  "leosmaia21/gcompilecommands.nvim",
  opts = {
    tmp_file_path = "$HOME/tmp/compilecommandsNEOVIM.json"
  },
  ft = { "c", "cpp", "make" }, -- lazy load plugin only on C, C++ and make filetypes
}
```
3. In your project file, open Neovim and run the `:Gcompilecommands` command. This will execute the `make` command in dry-run mode to generate the `compile_commands.json` file. Note that it will also run `make fclean` before generating the file.

4. After successful execution, the `compile_commands.json` file will be available for use by external tools.

### Cmake

Cmake projects store the header, source and make files in dedicated subdirectories. To generate and use the compilation database the :GCompilecommands call can be made from the cmake generated Makefile in the build directory. 
To use this generated database one can tell your lsp where to find it. For clangd this can be achived with a .clangd config file located at the project root with the following contents:
```
CompileFlags:
  CompilationDatabase: build/
```
Another helpful for cmake projects is the following line, which can be placed in a .nvim.lua file at the project base:
```
vim.cmd(":let &makeprg='cd build && cmake .. && make -Wall -w $* && cd ..'")
```
This configures the vim builtin :make command to first envoke cmake and then invoke make in the build directory. This command can of course be taylored to your needs.

## Contributions

Contributions are welcome! If you encounter issues, have improvements, or have ideas to make this plugin even more useful, feel free to open an [issue](https://github.com/leosmaia21/gcompilecommands.nvim/issues) or submit a [pull request](https://github.com/leosmaia21/gcompilecommands.nvim/pulls).

We hope this plugin makes generating the `compile_commands.json` file a straightforward and efficient task in your Neovim projects. Enjoy!
