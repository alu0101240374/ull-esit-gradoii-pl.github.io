---
title: Hello Actions World!
---

## Introduction

In this guide, you'll learn about the basic components needed to create and use a 
packaged JavaScript action. 

To focus this guide on the components needed to package the action,
the functionality of the action's code is minimal. 

The action prints 

```
Hello World
```

in the logs or 

```
Hello [who-to-greet]
``` 

if you provide a custom name.

This guide uses the [GitHub Actions Toolkit](https://github.com/actions/toolkit) Node.js module to speed up development. 

For more information, see the [actions/toolkit](https://github.com/actions/toolkit) repository.

To ensure your JavaScript actions are compatible with all GitHub-hosted runners (Ubuntu, Windows, and macOS), the packaged JavaScript code you write should be pure JavaScript and not rely on other binaries. 

JavaScript actions run directly on the runner and use binaries that already exist in the virtual environment.

## Prerequisites

Create a new empty repository on GitHub. You can choose any repository name or use `hello-world-javascript-action`. Then on your terminal:

```
$ mkdir hello-world-javascript-action
$ cd hello-world-javascript-action/
$ echo "# hello-world-javascript-action" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git remote add origin git@github.com:ULL-ESIT-PL-1920/hello-world-javascript-action.git
$ git push -u origin master
```

Create a `package.json`

```
[~/.../hello-world-javascript-action(master)]$ npm init -y
```
```js
{
  "name": "hello-world-javascript-action",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/ULL-ESIT-PL-1920/hello-world-javascript-action.git"
  },
  "keywords": [],
  "author": "Casiano Rodriguez-Leon <casiano.rodriguez.leon@gmail.com> (https://github.com/crguezl)",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/ULL-ESIT-PL-1920/hello-world-javascript-action/issues"
  },
  "homepage": "https://github.com/ULL-ESIT-PL-1920/hello-world-javascript-action#readme"
}
```

## Create an action metadata file

Create a new file `action.yml` in the `hello-world-javascript-action` directory with the following example code:

```
[~/.../hello-world-javascript-action(master)]$ cat action.yml
```
```yml
name: 'Hello World'
description: 'Greet someone and record the time'
inputs:
  who-to-greet:  # id of input
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  time: # id of output
    description: 'The time we greeted you'
runs:
  using: 'node12'
  main: 'index.js'
```

This file defines 

- the `who-to-greet` input and 
- `time` output. 

It also tells the action runner how to start: running `index.js`.

## Add actions toolkit packages

The actions toolkit is a collection of Node.js packages that allow you to quickly build JavaScript actions with more consistency.

The toolkit `@actions/core` package provides an interface to 

- the workflow commands, 
- input and output variables, 
- exit statuses, and 
- debug messages.

The toolkit also offers a `@actions/github` package that returns an authenticated **Octokit REST client** and access to GitHub Actions **contexts**.

The toolkit offers more than the **core** and **github** packages. 

For more information, see the <a href="https://github.com/actions/toolkit" target="_blank">actions/toolkit</a> repository.

At your terminal, install the actions toolkit core and github packages.

```
npm install @actions/core
npm install @actions/github
```

Now you should see 

1. a `node_modules` directory with the modules you just installed and 
2. a `package-lock.json` file with the installed module dependencies and the versions of each installed module.

## Write the action code

This action uses the toolkit to get the `who-to-greet` input variable required in the action's metadata file 

```js
const nameToGreet = core.getInput('who-to-greet');
```

and prints `Hello [who-to-greet]` in a debug message in the log. 

```js
console.log(`Hello ${nameToGreet}!`);
```

Next, the script gets the current time and **sets it as an output variable** that actions running later in a job can use.

```js
const time = (new Date()).toTimeString();
core.setOutput("time", time);
```

GitHub Actions provide **context** information about the webhook event, Git refs, workflow, action, and the person who triggered the workflow: 

```
 GITHUB_CONTEXT: {
  ...
  "event_name": "push",
  "event": {
       ...
     "commits": [
       ...
    ],
    ...
    "organization": {
      ...
    },
    "pusher": {
      ...
    },
  ...
}
```

To access the context information, you can use the **github** package. The action you'll write will print the webhook event payload the log.

```js
  const payload = JSON.stringify(github.context.payload, undefined, 2)
  console.log(`The event payload: ${payload}`);
```

Add a new file called `index.js`, with the following code:

```
[~/.../hello-world-javascript-action(master)]$ cat index.js
```
```js
const core = require('@actions/core');
const github = require('@actions/github');

try {
  // `who-to-greet` input defined in action metadata file
  const nameToGreet = core.getInput('who-to-greet');
  console.log(`Hello ${nameToGreet}!`);
  const time = (new Date()).toTimeString();
  core.setOutput("time", time);
  // Get the JSON webhook payload for the event that triggered the workflow
  const payload = JSON.stringify(github.context.payload, undefined, 2)
  console.log(`The event payload: ${payload}`);
} catch (error) {
  core.setFailed(error.message);
}
```

If an error is thrown in the above `index.js` example, `core.setFailed(error.message);` uses the actions toolkit [@actions/core](https://github.com/actions/toolkit/tree/master/packages/core) package to log a message and set a failing exit code.

For more information, see "[Setting exit codes for actions](https://help.github.com/en/actions/building-actions/setting-exit-codes-for-actions)."

## Create a README

To let people know how to use your action, you can create a README file. A README is most helpful when you plan to share your action publicly, but is also a great way to remind you or your team how to use the action.

In your `hello-world-javascript-action` directory, create a `README.md` file that specifies the following information:

1. A detailed description of what the action does.
2. Required input and output arguments.
3. Optional input and output arguments.
4. Secrets the action uses.
5. Environment variables the action uses.
6. An example of how to use your action in a workflow.

```
[~/.../hello-world-javascript-action(master)]$ cat README.md
# Hello world javascript action

This action prints "Hello World" or "Hello" + the name of a person to greet to the log.

## Inputs

### `who-to-greet`

**Required** The name of the person to greet. Default `"World"`.

## Outputs

### `time`

The time we greeted you.

## Example usage

uses: actions/hello-world-javascript-action@v1
with:
  who-to-greet: 'Mona the Octocat'
```

## Commit, tag, and push your action to GitHub

GitHub downloads each action run in a workflow during runtime and executes it as a complete package of code before you can use workflow commands like run to interact with the runner machine. 

This means **you must include any package dependencies required to run the JavaScript code**. You'll need to check in the toolkit core and github packages to your action's repository.

From your terminal, commit 

1. your `action.yml`, 
2. `index.js`, 
3. `node_modules`, 
4. `package.json`, 
5. `package-lock.json`, and 
6. `README.md` files. 
   
If you added a `.gitignore` file that lists `node_modules`, you'll need to remove that line to commit the `node_modules` directory.

```
git add action.yml index.js node_modules/* package.json package-lock.json README.md
git commit -m "My first action is ready"
```

It's best practice to also add a `version` tag for releases of your action. 

```
git tag -a -m "My first action release" v1
git push --follow-tags
```

For more information on versioning your action, see 
  
* [About actions](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/about-actions#versioning-your-action).
* [Versioning Actions](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)

As an alternative to checking in your `node_modules` directory you can use a tool called [zeit/ncc](https://github.com/zeit/ncc) to compile your code and modules into one file used for distribution.

1. Install [zeit/ncc](https://github.com/zeit/ncc) by running this command in your terminal: `npm i -g @zeit/ncc`
2. Compile your `index.js` file. `ncc build index.js`
   You'll see a new `dist/index.js` file with your code and the compiled modules.
3. Change the `main` keyword in your `action.yml` file to use the new `dist/index.js` file. main: `'dist/index.js'`
4. If you already checked in your `node_modules` directory, remove it. `rm -rf node_modules/*`
5. From your terminal, commit the updates to your `action.yml`, `dist/index.js`, and `node_modules` files.

    ```
    git add action.yml dist/index.js node_modules/*
    git commit -m "Use zeit/ncc"
    git tag -a -m "My first action release" v1
    git push --follow-tags
    ```

## Testing out your action in a workflow

Now you're ready to test your action out in a workflow. 

When an action is in a private repository, the action can only be used in workflows in the same repository.

Public actions can be used by workflows in any repository.

Let us create  a new repo in GitHub and also set it in your machine:

```
$ git remote add origin git@github.com:ULL-ESIT-PL-1920/use-hello-world-javascript-action.git
```

The following workflow code uses the completed hello world action in the `ULL-ESIT-PL-1920/hello-world-javascript-action` repository. 

Copy the workflow code into a `.github/workflows/main.yml` file, but replace the `ULL-ESIT-PL-1920/hello-world-javascript-action` repository with the repository you created. You can also replace the `who-to-greet` input with your name.


```
$ cat .github/workflows/main.yml
```

```yml
name: Using hello world
on: [push]

jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: A job to say hello
    steps:
      # To use this repository's private action, you must check out the repository
      - name: Checkout
        uses: actions/checkout@v2
      - name: Hello world action step
        uses: ULL-ESIT-PL-1920/hello-world-javascript-action@v1
        id: hello
        with:
          who-to-greet: 'Procesadores de Lenguajes at ULL'
      # Use the output from the `hello` step
      - name: Get the output time
        run: echo "The time was ${{"{{ steps.hello.outputs.time"}} }}"
```

Observe the `id` attribute in the `Hello world action step`. 

We use the `id` `hello` to refer to this step
in the next step `Get the output time` and to refer to its `output` using 
the expression `steps.hello.outputs`. 

Since in our `action.yml` file we set the name
of the output to `time` 

```yml
name: 'Hello World'
description: 'Greet someone and record the time'
inputs:
  who-to-greet:  # id of input
    ...
outputs:
  time: # id of output
    description: 'The time we greeted you'
runs:
  ...
```

we can refer to it with the expression `${{ "{{ steps.hello.outputs.time" }} }}`


The setting of the output was achieved inside the `index.js` file by calling the 
`setOutput` method of the `core` module:

```js
  const time = (new Date()).toTimeString();
  core.setOutput("time", time);
```

After adding and commiting the files, we push the changes to the remote 

```
[~/.../use-hello-world-javascript-action(master)]$ git push -u origin master
```

the action is triggered.

From our repository, We click the Actions tab, and select the latest workflow run. We can see `Hello Procesadores de Lenguajes at ULL` or the name we use for the `who-to-greet` input 

![]({{site.baseurl}}/assets/images/hello-world-js-action.png)

and the timestamp printed in the log:

![]({{site.baseurl}}/assets/images/hello-world-js-action-output-time.png)


## Publishing your action to GitHub Marketplace

When a repository contains an action metadata file (`action.yml` or `action.yaml`), you'll see a banner to publish the action to GitHub Marketplace. Click **Draft a release**.

![Publish this action to markeplace button](https://help.github.com/assets/images/help/repository/publish-github-action-to-markeplace-button.png)

The whole process requires a few steps, among them you have to **tag** your Action with a version. People will see the version in the action's dedicated GitHub Marketplace page.

![](https://help.github.com/assets/images/help/repository/marketplace_actions_version.png)


See [Publishing actions in GitHub Marketplace](https://help.github.com/en/actions/building-actions/publishing-actions-in-github-marketplace) for more information


## Versioning

GitHub recommends using [semantic versioning](http://semver.org/) when creating actions.

*   Create a GitHub **release** using semantic versioning (`v1.0.9`). For more information, see "[Creating releases](https://help.github.com/en/articles/creating-releases)."
*   Move the major version tag (`v1`, `v2`, etc.) to point to the Git ref of the current release. For more information, see "[Git basics - tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)."
*   Introduce a new major version tag (`v2`) for breaking changes that will break existing workflows. For example, changing an action's inputs would be a breaking change.


Inside the action client, We specified the version to use with the line:

```yml
uses: ULL-ESIT-PL-1920/hello-world-javascript-action@v1
```

The workflow references an action using a [git ref](https://git-scm.com/book/en/v2/Git-Internals-Git-References).

Hare are some more examples:

```yaml
steps:
    - uses: actions/javascript-action@v1        # recommended. starter workflows use this
    - uses: actions/javascript-action@v1.0.0    # if an action offers specific releases 
    - uses: actions/javascript-action@41775a4da8ffae865553a738ab8ac1cd5a3c0044 # sha
```

The idea is that with releases, binding to a major version is the **latest** of that major version.

That is, to say `v8` is the same as saying `"8.*"`.

Therefore, as an action developer, you can add new capabilities to a release, 
but **you should not break existing input compatibility or break existing workflows**. 

Here is an example of versioning workflow:

<img src="{{site.baseurl}}/assets/images/action-releases.png" style='background-color: white'/>


## Next Steps on Learning GitHub Actions {#next-step}

Use the repo [actions/javascript-action](https://github.com/actions/javascript-action)
as a template and follow the instructions. 

## Learning to use GitHub Actions at GitHub Learning Lab

{% include github-learning-lab.md %}

* [Search at GitHub Learning Lab for GitHub Action courses](https://lab.github.com/search?q=actions)

## References

{% include github-js-actions-references.md %}