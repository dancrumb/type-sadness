# DefinitelyTyped/ESM SSCCE

This is a pretty simple demonstration of an issue that is present in a number of NPM modules that rely on DefinitelyTyped to provide their typing.

Naturally the first step is:

```shell
npm install
```

If you take a look at `index.ts`, you'll see that it imports the `sign` named import from `jsonwebtoken` and then just logs it to the console.

`tsc` and the TypeScript Lanaguage Server are completely satisfied this this is type-correct.

However, if you then run

```
npx tsc
node dist/index.js
```

You will see the following error:

```
import { sign } from "jsonwebtoken";
         ^^^^
SyntaxError: Named export 'sign' not found. The requested module 'jsonwebtoken' is a CommonJS module, which may not support all module.exports as named exports.
CommonJS modules can always be imported via the default export, for example using:

import pkg from 'jsonwebtoken';
const { sign } = pkg;
```

This error is totally correct, because `jsonwebtoken` doesn't have a named export called `sign`. It has a default export, which is an object, which has a property called `sign`, whose value is the relevant function.
