# riparian

A package manager for Bosque programming language.

## The concept

Riparian ([Wikipedia](https://en.wikipedia.org/wiki/Riparian_zone)) would be the package manager for Bosque with which you can install, update & publish packages.

## The design

### Design changes

There are few changes:
   - Namespaces don't have to start with `NS` and can only have alphanumerical characters.
   - There's a `exported` keyboard, used to know which functions & co can be used when the package is imported.
   - A Bosque script can be directly executed only if the namespace is `Main` and there is an `entrypoint` called `main`.

### The packages/ directory

There's a directory called `packages` where packages are saved & loaded. You can install packages locally in a directory (see [src](src)) or in the `bosque/packages` directory.

A package has always got a file called `package.json`, which contains all the package information, including the name (not the namespace, but the name that will be used while executing `riparian`, e.g. `riparian install io` if the name is `io`, see [src/packages/io/package.json](src/packages/io/package.json)), the description, the default version (i.e. the version that will be loaded if no version is specified, see [src/hello-file.bsq](src/hello-file.bsq)) and a list of all the versions of the package.

The name of the directory under `packages` will be the same as the one specified in `package.json`.

### The package directory

Except for `package.json`, all under the package directory is a directory that represents a version (see [src/packages/io](src/packages/io)).

### The version directory

Scripts are placed here. Every scripts must have the same namespace and every variables, types, etc... are shared.

### Importing a package

To import a package, you use the `import` keyword followed by the package namespace. By default, you import the *default version* (see [src/packages/io/package.json](src/packages/io/package.json)).

If you want to import a different version, you can use the `version` keyword followed by the version you want to use (see [src/hello-file.bsq](src/hello-file.bsq)).

### Exported variables

By default, nothing is exported. If you want to make a variable, a type, an entity, etc... accessible you have to use the `exported` keyword (see [src/packages/io/dev/file.bsq](src/packages/io/dev/file.bsq)).

`exported` things are always `public`, but not all `public` things are always `exported`. Remember this.
`exported` things are accessible under the namespace used in the package (see [src/hello-world.bsq](src/hello-world.bsq)).
