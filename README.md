## Setup CLI:

1. Install Node.js (18+) https://nodejs.org/en/download
2. Open the terminal and run: `mkdir XPCLI`
3. `cd XPCLI`
4. `npm init` and fill the prompt
5. `mkdir bin` 
6. `touch bin/index.js`
7. Edit package.json and update the main object:
``"main": "bin/index.js",``
8. Add this object to the base object: `"bin": { "xp": "./bin/index.js"},`

package.json

```json
{
  "name": "xpcli",
  "version": "1.0.0",
  "description": "",
  "main": "bin/index.js",
  "bin": {
    "xp": "./bin/index.js"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

9. Edit `bin/index.js` and add this to it -> 

```javascript
#! /usr/bin/env node 
console.log("Hello Experimenter!");
```

10. Save and in the terminal run: `npm install -g .`
11. Now run -> `xp`
12. The terminal should now show `Hello Experimenter!`

## Use arguments in the CLI

1. In the Terminal run: `npm i yargs`
2. edit `bin/index.js` and replace the contents with:

```javascript
#! /usr/bin/env node 
const yargs = require('yargs/yargs');
const { hideBin } = require('yargs/helpers');
const argv = yargs(hideBin(process.argv)).argv;

if(argv.number1 && argv.number2) {
    const result = argv.number1 + argv.number2;
    console.log(`Addition ${result}`);
}
else {
    console.log('no numbers provided');
}
```
3. save and run `xp` the result should be:

```console
no numbers provided
```
4. Now type `xp --number1=2 --number2=2` and the result should be:

```console
Addition 4
```
5. can you make the math operation dynamic? as in `xp --number1=2 --number2=3 --operation=*` 

```console
Multiplication 6
```

## Reading the context folder

1. Edit `bin/index.js` and use a new argument to enable this functionality

```javascript
if(argv.detect) {
    console.log("Current directory:", process.cwd());
    fs.readdir(process.cwd(), function (err, files) {
        if (err) {
            return console.log('Unable to scan directory: ' + err);
        }
        if(files.includes('next.config.js')) {
            console.log(`the project is detected as next.js`);
        }
        else {
            console.log(`the project is detected as unknown`);
        }
    });
}
```

2. save the changes and Go to the `growthbook-integration-example` folder and type `xp --detect` it should return:

```console
the project is detected as unknown
```

3. go to next.js folder `cd nextjs` and type `xp --detect` it should return:

```console
the project is detected as next.js
```
4. Can you do the detection for the Java and Javascript projects? can you tell the difference between next.js and Javascript projects?
