# ssh2-sftp-server : SFTP server for node.js

Works in win32 and linux style.


[ssh2-sftp-server](https://github.com/idjem/ssh2-sftp-server) is sftp server module written in pure JavaScript it use excellent [ssh2 library](https://github.com/mscdex/ssh2) by Brian White.


[![Build Status](https://github.com/131/ssh2-sftp-server/actions/workflows/test.yml/badge.svg?branch=master)](https://github.com/131/ssh2-sftp-server/actions/workflows/test.yml)
[![Version](https://img.shields.io/npm/v/ssh2-sftp-server.svg)](https://www.npmjs.com/package/ssh2-sftp-server)

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](http://opensource.org/licenses/MIT)
[![Code style](https://img.shields.io/badge/code%2fstyle-ivs-green.svg)](https://www.npmjs.com/package/eslint-plugin-ivs)

![Available platform](https://img.shields.io/badge/platform-win32-blue.svg)
![Available platform](https://img.shields.io/badge/platform-linux-blue.svg)



# Installation

```
npm install ssh2-sftp-server
```

# Supported API
support most of client requests:

- `OPEN`
- `CLOSE`
- `REALPATH`
- `STAT`
- `OPENDIR`
- `READ`
- `REMOVE`
- `RMDIR`
- `MKDIR`
- `RENAME`
- `READDIR`
- `WRITE`

# Usage

```js
"use strict";

const fs         = require('fs');
const {Server}   = require('ssh2');
const SftpServer = require('ssh2-sftp-server');

new ssh2.Server({
  hostKeys: [fs.readFileSync('host.key')]
}, function(client) {
  client.on('authentication', function(ctx) {
    ctx.accept();
  }).on('ready', function() {
    client.on('session', (accept) => {
      const session = accept();
      session.on('sftp', (accept) => {
        const sftpStream = accept();
        new SftpServer(sftpStream);
      });
    });
  });
});
```

# Credits

* [idjem](https://github.com/idjem)
* [131](https://github.com/131)



