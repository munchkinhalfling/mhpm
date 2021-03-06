# mhpm
## MunchkinHalfling's Package Manager
This is a package manager for client-side JavaScript.
### Getting Started
To include MHPM, put the following into your `<head>`:
```html
<script src="https://raw.githack.com/munchkinhalfling/mhpm/master/mhpm.js"></script>
```
Then, you need to set up your script as asynchronous, like so: (this is so you can use `await` to load packages)
```html
<script>
  (async () => {
    // code...
  })();
</script>
```
Then, in a script, you can import any package in the [repository file](https://github.com/munchkinhalfling/mhpm/blob/master/repository.json) with the following:
```js
// ...
const MyModule = await Package.load("Package Name");
// ...
```
You can also load packages from specific configuration files (described below) not listed in the repository file with the following:
```js
const MyUnlistedModule = await Package.loadFromConfig("https://path/to/mhpm-config.json");
```
### Creating Packages
First, create a GitHub repo or something else for your package. Then, create an `mhpm-config.json` file that has the following syntax:
```json
{
  "name": "package name goes here",
  "version": "(optional) package version",
  "dependencies": ["Required, even if it's an empty list"],
  "pkgfile": "(REQUIRED) javascript file of the package (see below)"
}
```
Then, create a JavaScript file (the path/URL goes in the `pkgfile` field) that follows the following syntax:
```js
(function(/* dependencies (in order) */) {
  // code/private variables
  return {
    // exported variables go here
  };
}) //NOTICE: NO SEMICOLON (it must be an anonymous function)
```
After that, go into the repository file and add an entry in the `pkgs` array that has the following format:
```json
{
  "name": "package name (REQUIRED)",
  "conf-file": "path to the configuration file made in the first step"
}
```
Then send me a pull request!
