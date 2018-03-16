# SAPUI5 Runtime
A package which downloads the official SAPUI5 runtime from [https://tools.hana.ondemand.com/](https://tools.hana.ondemand.com/#sapui5) for local development.

# Installation
By using this npm package you agree to the EULA from SAP: [https://tools.hana.ondemand.com/developer-license-3_1.txt/](https://tools.hana.ondemand.com/developer-license-3_1.txt/)
```bash
$ npm install -D sapui5-runtime
# - or -
$ yarn add -D sapui5-runtime
```
This will download and unzip the latest SAPUI5 runtime. If you want to use a specific version you can write your desired version into your `package.json`:
```json
"sapui5": {
    "version": "latest"
}
```
`latest` is the default value and will download the latest stable/maintained release of SAPUI5. You can find all available version [here](https://sapui5.hana.ondemand.com/versionoverview.html).
Make sure you use the patch version number (e.g `"1.52.7"` instead of `"1.52"`).

# Get started
After a successful installation you can use a server to serve the runtime as static files.


## [Express](https://github.com/expressjs/express) example
```javascript
const express = require('express')
const sapui5 = require('sapui5-runtime')
const app = express()

app.use('/resources', express.static(sapui5))

app.listen(3000)
```

## [Hapi](https://github.com/hapijs/hapi) example
```javascript
const Hapi = require('hapi')
const inert = require('inert')
const sapui5 = require('sapui5-runtime')

const server = Hapi.server({
    port: 3000,
    host: 'localhost'
})

const init = async () => {
    await server.register(inert)
    server.route({
        method: 'GET',
        path: '/resources/{param*}',
        handler: {
            directory: {
                path: sapui5
            }
        }
    });
    await server.start()
}

init()
```

# Contribution
I'm happy to accept Pull Requests! Please note that this project is released with a [Contributor Code of Conduct](https://github.com/bastilimbach/sapui5-runtime/blob/master/CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

# Credits
This project was heavily inspired by [openui5.runtime.downloader](https://github.com/maugenst/openui5.runtime.downloader) by [Marius Augenstein](https://github.com/maugenst).

# License
[MIT](https://github.com/bastilimbach/sapui5-runtime/blob/master/LICENSE) :heart:
