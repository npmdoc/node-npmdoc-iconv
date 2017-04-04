# api documentation for  [iconv (v2.2.1)](https://github.com/bnoordhuis/node-iconv)  [![npm package](https://img.shields.io/npm/v/npmdoc-iconv.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-iconv) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-iconv.svg)](https://travis-ci.org/npmdoc/node-npmdoc-iconv)
#### Text recoding in JavaScript for fun and profit!

[![NPM](https://nodei.co/npm/iconv.png?downloads=true)](https://www.npmjs.com/package/iconv)

[![apidoc](https://npmdoc.github.io/node-npmdoc-iconv/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-iconv_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-iconv/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-iconv/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-iconv/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Ben Noordhuis",
        "email": "info@bnoordhuis.nl"
    },
    "bugs": {
        "url": "https://github.com/bnoordhuis/node-iconv/issues"
    },
    "dependencies": {
        "nan": "^2.3.5"
    },
    "description": "Text recoding in JavaScript for fun and profit!",
    "devDependencies": {
        "tap": "~0.4.8"
    },
    "directories": {},
    "dist": {
        "shasum": "39b13fdd98987d26aef26c0a2f2a900911fa4584",
        "tarball": "https://registry.npmjs.org/iconv/-/iconv-2.2.1.tgz"
    },
    "engines": {
        "node": ">=0.8.0"
    },
    "gitHead": "3a2cbfeca5dac59d9b7d3ed62c34b68852aaaba8",
    "gypfile": true,
    "homepage": "https://github.com/bnoordhuis/node-iconv",
    "license": "ISC",
    "main": "./lib/iconv",
    "maintainers": [
        {
            "name": "bnoordhuis",
            "email": "info@bnoordhuis.nl"
        }
    ],
    "name": "iconv",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/bnoordhuis/node-iconv.git"
    },
    "scripts": {
        "install": "node-gyp rebuild",
        "test": "tap test/test-*.js"
    },
    "version": "2.2.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module iconv](#apidoc.module.iconv)
1.  [function <span class="apidocSignatureSpan">iconv.</span>Iconv (fromEncoding, toEncoding)](#apidoc.element.iconv.Iconv)

#### [module iconv.Iconv](#apidoc.module.iconv.Iconv)
1.  [function <span class="apidocSignatureSpan">iconv.</span>Iconv (fromEncoding, toEncoding)](#apidoc.element.iconv.Iconv.Iconv)
1.  [function <span class="apidocSignatureSpan">iconv.Iconv.</span>super_ ()](#apidoc.element.iconv.Iconv.super_)



# <a name="apidoc.module.iconv"></a>[module iconv](#apidoc.module.iconv)

#### <a name="apidoc.element.iconv.Iconv"></a>[function <span class="apidocSignatureSpan">iconv.</span>Iconv (fromEncoding, toEncoding)](#apidoc.element.iconv.Iconv)
- description and source-code
```javascript
function Iconv(fromEncoding, toEncoding)
{
  if (!(this instanceof Iconv)) {
    return new Iconv(fromEncoding, toEncoding);
  }

  stream.Stream.call(this);
  this.writable = true;

  var conv = bindings.make(fixEncoding(fromEncoding),
                           fixEncoding(toEncoding));
  if (conv === null) {
    throw new Error('Conversion from ' +
                    fromEncoding + ' to ' +
                    toEncoding + ' is not supported.');
  }

  var convert_ = convert.bind({ conv_: conv });
  var context_ = { trailer: null };

  this.convert = function(input, encoding) {
    if (typeof(input) === 'string') {
      input = new Buffer(input, encoding || 'utf8');
    }
    return convert_(input, null);
  };

  this.write = function(input, encoding) {
    if (typeof(input) === 'string') {
      input = new Buffer(input, encoding || 'utf8');
    }
    try {
      var buf = convert_(input, context_);
    }
    catch (e) {
      this.emit('error', e);
      return false;
    }
    if (buf && buf.length !== 0) {
      this.emit('data', buf);
    }
    return true;
  };

  this.end = function(input, encoding) {
    if (typeof(input) !== 'undefined') {
      this.write(input, encoding);
    }
    this.write(FLUSH);
    this.emit('end');
  };
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.iconv.Iconv"></a>[module iconv.Iconv](#apidoc.module.iconv.Iconv)

#### <a name="apidoc.element.iconv.Iconv.Iconv"></a>[function <span class="apidocSignatureSpan">iconv.</span>Iconv (fromEncoding, toEncoding)](#apidoc.element.iconv.Iconv.Iconv)
- description and source-code
```javascript
function Iconv(fromEncoding, toEncoding)
{
  if (!(this instanceof Iconv)) {
    return new Iconv(fromEncoding, toEncoding);
  }

  stream.Stream.call(this);
  this.writable = true;

  var conv = bindings.make(fixEncoding(fromEncoding),
                           fixEncoding(toEncoding));
  if (conv === null) {
    throw new Error('Conversion from ' +
                    fromEncoding + ' to ' +
                    toEncoding + ' is not supported.');
  }

  var convert_ = convert.bind({ conv_: conv });
  var context_ = { trailer: null };

  this.convert = function(input, encoding) {
    if (typeof(input) === 'string') {
      input = new Buffer(input, encoding || 'utf8');
    }
    return convert_(input, null);
  };

  this.write = function(input, encoding) {
    if (typeof(input) === 'string') {
      input = new Buffer(input, encoding || 'utf8');
    }
    try {
      var buf = convert_(input, context_);
    }
    catch (e) {
      this.emit('error', e);
      return false;
    }
    if (buf && buf.length !== 0) {
      this.emit('data', buf);
    }
    return true;
  };

  this.end = function(input, encoding) {
    if (typeof(input) !== 'undefined') {
      this.write(input, encoding);
    }
    this.write(FLUSH);
    this.emit('end');
  };
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.iconv.Iconv.super_"></a>[function <span class="apidocSignatureSpan">iconv.Iconv.</span>super_ ()](#apidoc.element.iconv.Iconv.super_)
- description and source-code
```javascript
function Stream() {
  EE.call(this);
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
