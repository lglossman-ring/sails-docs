# Using TypeScript in a Sails app

Sails supports using TypeScript to write your custom app code (like [actions](http://sailsjs.com/documentation/concepts/controllers#?actions) and [models](http://sailsjs.com/documentation/concepts/models-and-orm)).  You can enable this support in just a few steps:

1. Run `npm install ts-node --save` in your app folder.
2. Install the necessary typings for your app.  At the very least you'll probably want to:
   ```javascript
   npm install @types/node --save
   npm install @types/express --save
   ```
3. Add the following line at the top of your app's `app.js` file:
   ```javascript
   require('ts-node/register');
   ```
4. Add a `config/extensions.js` file to your project with:
   ```javascript
   module.exports.moduleloader = {
     sourceExt: ['js', 'ts'],
     configExt: ['js', 'ts']
   };
   ```
5. Start your app with `node app.js` instead of `sails lift`.

Here's an example Typescript controller to get you started, courtesy of [@oshatrk](https://github.com/oshatrk):

```typescript
// api/controllers/TsController.js

import util = require('util');
import express = require('express');

declare var sails: any;

export function index(req:any, res:any, next: Function):any {
  console.log('index() from TsController.ts');
  res.status(200).send('Hello from Typescript!');
}

export function config(req: express.Request, res: express.Response, next: Function) {
  console.log('config() from TsController.ts');
  res.status(200)
     .send('<h1>sails.config :</h1><pre>' + util.inspect(sails.config) + '<pre>');
}
```

<docmeta name="displayName" value="Using TypeScript">
