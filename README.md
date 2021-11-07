# Upgrade

## Add Git Repository

Use `https://github.com/GammaGate/api.git` for the "Remote Git repository" field.

## Node.js

If there has been a new release, first click the "NPM Install button", then "Run script" with `Bootstrap`. It may be that a restart is necessary.

# Installation

## Directus Shared Hosting with Plesk

On many shared hosts you are not allowed to directly invoke node commands but you have to use the Plesk configuration panel instead. Unfortunately, Plesk does not allow the interactive execution of node scripts. Therefore we can't use Directus' `init`script and have to set up the project by our own.

## Setup a project folder

On the server, create a project folder with 4 files in it.

### [#](https://docs.directus.io/getting-started/installation/plesk/#_1-add-env-file) 1. Add .env file

This file is used to configure Directus. Normally, the `init` script would create it for us. So now we have to do it manually. You can just copy it from another Directus installation or use the [example file](https://github.com/directus/directus/blob/main/api/example.env)

### [#](https://docs.directus.io/getting-started/installation/plesk/#_2-add-package-json) 2\. Add package.json

Add Directus and your database connector as a dependency. To execute Directus' `bootstrap` command you also have to add a script entry for it.

```
{
	"scripts": {
		"bootstrap": "directus bootstrap"
	},
	"dependencies": {
		"directus": "*",
		"mysql": "^2.18.1"
	}
}

```

### [#](https://docs.directus.io/getting-started/installation/plesk/#_3-add-application-startup-file-index-js) 3. Add application startup file index.js

Instead of a start command, Plesk wants a startup file. So create a `index.js` with the following content:

```
var { startServer } = require('directus/server');

startServer();

```

### [#](https://docs.directus.io/getting-started/installation/plesk/#_4-add-npmrc) 4. Add .npmrc

Lastly, we need to make a small configuration for npm by creating a `.npmrc` file with the following content:

```
scripts-prepend-node-path=true

```

### [#](https://docs.directus.io/getting-started/installation/plesk/#activate-and-configure-node-js) Activate and configure node.js

In Plesk, choose your website and click "Node.js". You should then see a button "Enable Node.js" and click on it.

Now, change the "Document root" and "Application root" to the location of your project folder. "Application startup
file" must point to the `index.js` file from the former step. The screen should now look like this:

![Plesk Screenshot](https://docs.directus.io/assets/img/plesk-screenshot.2e2f90c2.png)

You can now install the dependencies by clicking on the button "NPM install".

### [#](https://docs.directus.io/getting-started/installation/plesk/#bootstrap-directus) Bootstrap Directus

To set up the database tables (and the first user) for Directus, click on the button "Run script" and input `bootstrap`. You get the console output after the script has run through.

### [#](https://docs.directus.io/getting-started/installation/plesk/#test-directus-access) Test Directus Access

The Directus app should now work under your configured url. If not, try changing the development mode and wait a couple of seconds

---

[This installation guide is from: **_docs.directus.io_**](https://docs.directus.io/getting-started/installation/plesk/)
