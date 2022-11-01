# npm Code-Along

## Learning Goals

- Use a `package.json` file to manage project dependencies
- Install a project dependency using npm
- Import code from a package into a JavaScript file

## Introduction
A complication with modern app development, particularily JavaScript, is managing
the complex, recursive dependency tree relating the packages. `npm`, the default
package manager for JS, helps in two major ways:
- install packages: **`npm install <self>`** => collects `"dependencies"` from
(default) `./packages.json` directory and adopts a './nodes_modules' subdirectory
to install packages necessary for **running the application or program**
- create packages: **`npm init <self>`** => collects `"devDependencies"` from (default)
`./packages.json` and `./package-lock.json` and installs packages necessary for
**developing the application or program**
_Along with the specified dependencies, installs and manages necessary dependencies of_
_the packages_
### 

We will see in future labs that as the number of packages increases, more and
more happens when we run `npm install`. All _we_ need to worry about, though, is
the top level — what is listed in _our_ application's `package.json` file.

This code-along demonstrates the process of setting up a `package.json` file to
install and utilize npm packages in our code. 

## Getting Started
Need to specify a project name to store all files. Dependecies will be defined in
the `package.json` or `package_lock.json` file in the project directory (if neither
files are present, npm will make one). A child `project>node_modules` will store the
packages necessary to **run** the application (`--save-dev`-> also installs `devDependencies`)


```html
<script src="index.js" type="module"></script>
```

Taking a look inside `index.js`, we can see that this script relies on a unique
function call, `format(new Date(), "MMMM do yyyy, h:mm:ss a")`. We're also
**importing** that function from a `node_modules` folder that contains a date
formatting library called `date-fns`. Our goal is to get this code working. **We
do not need to change `index.js`**. Instead, we will need to set up a
`package.json` file and install the
[`date-fns`](https://www.npmjs.com/package/date-fns) package.

## Navigate to the Project Directory

The first thing to do is change directory into this folder in your terminal by
typing the command `cd color-clock`.

> **Note**: The next step will create a `package.json` file in whatever
> directory you are in, which in turn will be where the `node_modules` folder
> is. If you do not change directory into `color-clock`, you'll end up creating
> a file in the main directory of this lesson, and `color-clock/index.js` will
> be looking for `node_modules` in the wrong directory.

### Create a package.json File

The `package.json` can be written quickly from scratch, but we actually have a
handy command for creating these files: `npm init`.

Run `npm init` and you will be prompted to confirm the information that will be
stored in `package.json`, starting with the name of the project.

Most prompts will provide a default value. Some are blank and can be left this
way for now. Follow the prompts by pressing enter in the terminal on each prompt
until you reach the end, when you will be prompted to type 'yes' to confirm. A
fully constructed `package.json` file will then appear in the `color-clock`
directory.

### Add a Script

In the process of creating the `package.json` file, you were prompted to write a
test script. Let's add a working script in to see how this works.

Open the newly created `package.json` file and look for a section titled
`"scripts"`. Let's replace the default `"test"` script with a shell command:

```json
"scripts": {
  "test": "echo 'Hello World!'"
}
```

We can now call this script and have it run by using the command `npm test` in
the terminal (if that doesn't work, try `npm run test`). You should see a print
out of `Hello World!`.

In all the JavaScript-based labs you've encountered so far, this sort of script
is how we run tests. If you look at the `"test"` script on previous labs, most
will have something like this:

```txt
"test": "mocha -R mocha-multi --reporter-options spec=-,json=.results.json"
```

This is actually a command that you can run in the terminal. This is a call to
the testing package, `mocha`, along with a second package, `mocha-multi` that
helps with reporting. When you run `learn test` in a lab, `npm test` _gets
called_.

Scripts are often useful for things like testing or to start a necessary
process, like a local server.

### Install a Package

With `package.json` set up, we can now add a package we want to include in our
project.

Now, we're building a colorful clock — the project is simple enough that we
_could_ build it entirely out of custom code. Here's the thing though: one of
the reasons packages exist and are so useful is because programmers often run
into the same problems over and over. Node packages are written so we don't have
to recreate a solution to a problem other programmers have already solved.

In the case of a colorful clock, we have to deal with formatting time. This is
such a common problem, that a package has been created to help us:
[`date-fns`][date-fns]. `date-fns` is a handy package that comes with a number
of functions that make displaying dates and times simpler than trying to figure
out JavaScript's built-in functions.

Let's install `date-fns` and incorporate it into our clock. To install a package
and save it to your `package.json` file, run `npm install` followed by the
package name. In our case, that would be:

```console
$ npm install date-fns
```

This command will add the package to the list of dependencies in `package.json`.
When `npm install` is run, all dependencies are installed. If you were to
publish this repository on GitHub, other users would now be able to clone down
the repo and install whatever is listed in `package.json` to get the program
working.

We'll also need one more package to run our application in the browser. Run this
command:

```console
$ npm install serve
```

This [`serve`](https://www.npmjs.com/package/serve) package will run a
lightweight server. Set up another npm script to run the server using the
`serve` package:

```json
"scripts": {
  "test": "echo 'Hello World!'",
  "start": "serve"
}
```

Run `npm start` to run this script, and open up
[localhost:3000](http://localhost:3000) in the browser.

If `package.json` file has the correct package, and the node module has been
installed, you should see a colorful clock appear!

## Conclusion

When building our own applications, we will often rely on existing packages to
handle specific pieces of a project. Although we only installed a couple of
packages for this code-along, there were additional layers of dependencies for
them so many additional dependencies were installed as well. It isn't necessary
to understand _how_ each of these works. The main thing to grasp is how to
implement and use the specific dependencies you need.

[date-fns]: (https://www.npmjs.com/package/date-fns)
