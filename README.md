# Digipet - Deployment

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a>

> This is part of Academy's [technical curriculum for **The Mark**](https://github.com/WeAreAcademy/curriculum-mark). All parts of that curriculum, including this project, are licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a>.

Now we'll deploy your Digipet (both frontend and backend), so that others can interact with your digipet over the web without you having to run anything locally.

## Learning Outcomes

- Deploy a Node.js server to Heroku

## Exercise 0: Running your compiled JavaScript server

> 🎯 **Success criterion:** you can run your compiled _JavaScript_ digipet server locally

We've written our server in TypeScript and we've been running it locally using `ts-node` - which effectively compiles our TypeScript into JavaScript for us.

This is fine for development, but in deployment we would typically separate out this 'build' and 'start' process.

We'll do this locally by:

1. Adding a `build` script to compile our TypeScript to JavaScript
2. Changing our `start` script to use `node` to run our compiled JavaScript

`tsc` is used to compile TypeScript to JavaScript.

The `tsconfig.json` provided in your digipet backend starter has `dist` set as the target compilation directory (`outDir`) for the resultant JavaScript, which means we should add the following scripts:

```diff
"scripts": {
-  "start": "ts-node src",
+  "start": "node dist",
   "start:dev": "ts-node-dev src",
+  "build": "tsc",
   "test": "jest",
   "test:watch": "jest --watch"
},
```

Now, test that you can run your compiled JavaScript locally:

1. `yarn build` to compile to JavaScript
2. `yarn start` to run the compiled JavaScript

## Exercise 1: Installing Heroku

> 🎯 **Success criterion:** you can run your compiled server locally with Heroku

We'll be deploying our server to Heroku, a platform which offers support for free deployment of Node.js servers (amongst other types of apps).

To do this, we'll need to complete a couple of prerequisites listed in [the Heroku guide for deploying Node.js apps](https://devcenter.heroku.com/articles/deploying-nodejs#prerequisites):

- [x] Node.js and npm installed
- [x] an existing Node.js app
- [ ] a free [Heroku account](https://signup.heroku.com/dc)
- [ ] the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)

(When following the guide for Heroku CLI, you should log in through the CLI to your Heroku account that you just created. You don't need to create a Heroku app just yet.)

After this, you should be able to run your app locally via the Heroku CLI with `heroku local web` (as documented [here](<(https://devcenter.heroku.com/articles/deploying-nodejs#build-your-app-and-run-it-locally)>)).

### Optional - creating a `Procfile`

You may see the following messages when you do this:

```
[WARN] ENOENT: no such file or directory, open 'Procfile'
[OKAY] package.json file found - trying 'npm start'
```

This is because Heroku, [by default, looks for start instructions in a file called `Procfile`, then falls back on the `package.json` `start` script](https://devcenter.heroku.com/articles/deploying-nodejs#specifying-a-start-script). We haven't created a Procfile (hence the first warning), but we have got a `start` script in our `package.json`, so it falls back to that.

If you want to, you can create a `Procfile` (that's the file name, it has no file extension) in the root of your project with the following content (essentially, identical to our `start` script):

```
web: node dist
```

and the first warning will disappear.
