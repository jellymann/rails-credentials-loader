# rails-credentials-loader

Webpack loader for injecting Rails credentials into JavaScript.

## How to use:

1. Install

   ```
   yarn add rails-credentials-loader
   ```

2. Add to `config/webpack/environment.js`

   ```javascript
   const { environment } = require('@rails/webpacker')

   environment.loaders.prepend('credentials', {
     test: /\.js$/,
     enforce: 'pre',
     exclude: /node_modules/,
     use: 'rails-credentials-loader'
   })

   module.exports = environment
   ```

3. Use your credentials in your JS

   ```yaml
   # credentials.yml
   some_api:
     public_key: 'ABCD123'
   ```

   ```javascript
   const SOME_API_KEY = $$RailsCredentials.some_api.public_key;
   ```

   Output:

   ```javascript
   const SOME_API_KEY = "ABCD123";
   ```

## ⚠️ WARNING ⚠️

Be *very* careful with how you use this. Anything you reference *will* become unencrypted in the resulting JavaScript pack that gets sent to the user's browser. Make sure you *only* reference values that are safe to be out in the open.
