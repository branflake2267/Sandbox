# Using NPM
This guide covers using Sencha Test standalone from the Node Package Manager NPM. 

## Reference

* [Check out more on Sencha Test Standalone guide](./guides/cli_archive_server/sencha_test_cli.html) 

## Login
Start by logging in.

```
npm login --registry=https://npm.sencha.com --scope=@sencha
```

## Install
Add the package to your package.json dependencies. 

```
npm install @sencha/stc-cli
```

Here is an example of how it will look after the install. 
```
{
    "name": "my-project-name",
    "version": "1.0.0",
    "description": "my project description.",
    "scripts": {
    },
    "author": "Sencha, Inc.",
    "dependencies": {
        "@sencha/stc-cli": "~1.0.41"
    }
}
```

## Configure
Open up Sencha Test and configure our browser farm target. 

* [Check out the browser farms guide](./guides/browser_farms/introduction_to_browser_farms.html) 

## Running
Run from your CI enviroment either by adding a run script to your package.json or by directly running the config. 

#### Run with npm
Use a package.json run script like the test script below. `npm

1. Declare the run script in the `scripts`. 
```
{
    "name": "@sencha/orion-stc-cli-test-project",
    "version": "1.0.0",
    "description": "Orion repo tests.",
    "scripts": {
        "test": "npx stc run -p 'saucePool' -s 'test/simple_google_test' -o teamcity --trace"
    },
    "author": "Sencha, Inc.",
    "dependencies": {
        "@sencha/stc-cli": "~1.0.41"
    }
}
```
2. Run the npm run script by calling the script, like `npm test`. 


#### Run with npx
Directly run the config using NPX. NPX will start stc standalone. 

```
npx stc run -p 'saucePool' --scenarioName 'Kitchen Sink Regression - Modern'
```


FAQ
1. Q: When you have problems running because the OS stc package isn't downloading. 
   A: Delete the `./node_modules/@sencha/stc*` files and run `npm install` again. 



