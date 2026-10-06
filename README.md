# as3-to-ts

> A tool that helps porting AS3 codebases to TypeScript

This fork has attempted to unify the whole as3-to-ts fork network.

This project is a fork of [as3web/as3-to-ts](https://github.com/as3web/as3-to-ts) which is a fork of
[simonbuchan/as3-to-typescript](https://github.com/simonbuchan/as3-to-typescript),
which is a fork of [the original
as3-to-typescript](https://github.com/fdecampredon/as3-to-typescript)
implementation.

## Installation

**Option 1: via npm:(for the as3web implementation)**:

```
npm install -g as3-to-ts
```

**Option 2: building the source:**

Make sure you have [Node v6+](https://nodejs.org/) installed.

- Clone the repository
- Run `npm link`

You should have `as3-to-ts` now globaly available in your commandline.

## Usage

```
as3-to-ts <sourceDir> <outputDir> [--commonjs] [--visitors dictionary,stringutil,createjs] [--interactive] [--overwrite]
```

Options:

- `--commonjs`: export .ts files using CommonJS's import style.
- `--visitors [name]`: use custom visitors, separated by comma. implemented
  under `src/custom-visitor/[name]` (currently available: `dictionary`,
  `stringutil`, `createjs`)
- `--overwrite`: force overwrite of previously-converted files.
- `--interactive`: if you've manually changed a generated `.ts` file, you'll be
  asked if you want to overwrite it or not.

## Known issues (may be fixed due to unification but idk)

- `super` calls on constructor need to be moved as the first call after conversion.
- having a comment on `extends` statement causes infinite loop parsing the `.as` file.
- having `break` without a semicolon results in infinite loop parsing the `.as` file.
- having a method without access level will throw `Error: invalid consume`.
  (usually this is result of bad copy & paste without renaming the class constructor)
- having inline multiline comment break the parser (`var i = (/*comment*/true)`)
- namespaces can't have TypeScript keywords, such as `enum`, `class`, etc. (not
  an issue if transpiled using `--commonjs`)
- multiple property definitions generate invalid syntax (`public var velocityX:Number, velocityY:Number;`)

## Planned features

I plan to add an API to use the tool soon, but who knows how long that will take :P

## Note

This tool will not magically transform your AS3 codebase into perfect TypeScript, the goal is to transform the sources into *syntactically* correct TypeScript, and even this goal is not perfectly respected. It also won't try to provide Javascript implementation for flash libraries.

However unlike most attempts that I have seen this tool is based on a true ActionScript parser, and so should be able to handle most of AS3 constructs and greatly ease the pain of porting a large code base written in AS3 to TypeScript.
