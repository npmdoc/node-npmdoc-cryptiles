# api documentation for  [cryptiles (v3.1.1)](https://github.com/hapijs/cryptiles#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-cryptiles.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-cryptiles) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-cryptiles.svg)](https://travis-ci.org/npmdoc/node-npmdoc-cryptiles)
#### General purpose crypto utilities

[![NPM](https://nodei.co/npm/cryptiles.png?downloads=true)](https://www.npmjs.com/package/cryptiles)

[![apidoc](https://npmdoc.github.io/node-npmdoc-cryptiles/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-cryptiles_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-cryptiles/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-cryptiles/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-cryptiles/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "bugs": {
        "url": "https://github.com/hapijs/cryptiles/issues"
    },
    "dependencies": {
        "boom": "4.x.x"
    },
    "description": "General purpose crypto utilities",
    "devDependencies": {
        "code": "3.x.x",
        "lab": "11.x.x"
    },
    "directories": {},
    "dist": {
        "shasum": "86a9203f7367a0e9324bc7555ff0fcf5f81979ee",
        "tarball": "https://registry.npmjs.org/cryptiles/-/cryptiles-3.1.1.tgz"
    },
    "engines": {
        "node": ">=4.0.0"
    },
    "gitHead": "2c34befad99084806bf8471a2fb870615ab7225b",
    "homepage": "https://github.com/hapijs/cryptiles#readme",
    "keywords": [
        "cryptography",
        "security",
        "utilites"
    ],
    "license": "BSD-3-Clause",
    "main": "lib/index.js",
    "maintainers": [
        {
            "name": "hueniverse",
            "email": "eran@hueniverse.com"
        },
        {
            "name": "ceejbot",
            "email": "ceejceej@gmail.com"
        }
    ],
    "name": "cryptiles",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/hapijs/cryptiles.git"
    },
    "scripts": {
        "test": "lab -a code -t 100 -L",
        "test-cov-html": "lab -a code -r html -o coverage.html"
    },
    "version": "3.1.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module cryptiles](#apidoc.module.cryptiles)
1.  [function <span class="apidocSignatureSpan">cryptiles.</span>fixedTimeComparison (a, b)](#apidoc.element.cryptiles.fixedTimeComparison)
1.  [function <span class="apidocSignatureSpan">cryptiles.</span>randomBits (bits)](#apidoc.element.cryptiles.randomBits)
1.  [function <span class="apidocSignatureSpan">cryptiles.</span>randomDigits (size)](#apidoc.element.cryptiles.randomDigits)
1.  [function <span class="apidocSignatureSpan">cryptiles.</span>randomString (size)](#apidoc.element.cryptiles.randomString)



# <a name="apidoc.module.cryptiles"></a>[module cryptiles](#apidoc.module.cryptiles)

#### <a name="apidoc.element.cryptiles.fixedTimeComparison"></a>[function <span class="apidocSignatureSpan">cryptiles.</span>fixedTimeComparison (a, b)](#apidoc.element.cryptiles.fixedTimeComparison)
- description and source-code
```javascript
fixedTimeComparison = function (a, b) {

    if (typeof a !== 'string' ||
        typeof b !== 'string') {

        return false;
    }

    let mismatch = (a.length === b.length ? 0 : 1);
    if (mismatch) {
        b = a;
    }

    for (let i = 0; i < a.length; ++i) {
        const ac = a.charCodeAt(i);
        const bc = b.charCodeAt(i);
        mismatch |= (ac ^ bc);
    }

    return (mismatch === 0);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cryptiles.randomBits"></a>[function <span class="apidocSignatureSpan">cryptiles.</span>randomBits (bits)](#apidoc.element.cryptiles.randomBits)
- description and source-code
```javascript
randomBits = function (bits) {

    if (!bits ||
        bits < 0) {

        return Boom.internal('Invalid random bits count');
    }

    const bytes = Math.ceil(bits / 8);
    try {
        return Crypto.randomBytes(bytes);
    }
    catch (err) {
        return Boom.internal('Failed generating random bits: ' + err.message);
    }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cryptiles.randomDigits"></a>[function <span class="apidocSignatureSpan">cryptiles.</span>randomDigits (size)](#apidoc.element.cryptiles.randomDigits)
- description and source-code
```javascript
randomDigits = function (size) {

    const buffer = exports.randomBits(size * 8);
    if (buffer instanceof Error) {
        return buffer;
    }

    const digits = [];
    for (let i = 0; i < buffer.length; ++i) {
        digits.push(Math.floor(buffer[i] / 25.6));
    }

    return digits.join('');
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cryptiles.randomString"></a>[function <span class="apidocSignatureSpan">cryptiles.</span>randomString (size)](#apidoc.element.cryptiles.randomString)
- description and source-code
```javascript
randomString = function (size) {

    const buffer = exports.randomBits((size + 1) * 6);
    if (buffer instanceof Error) {
        return buffer;
    }

    const string = buffer.toString('base64').replace(/\+/g, '-').replace(/\//g, '_').replace(/\=/g, '');
    return string.slice(0, size);
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
