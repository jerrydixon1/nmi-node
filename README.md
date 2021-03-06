Node SDK for Networking Merchants Inc's (NMI) Three Step Redirect API

# Installation
```
npm install nmi-node
```

# Documentation

[Module documentation](docs.md)

[NMI Three Step Redirect API docs](https://secure.networkmerchants.com/gw/merchants/resources/integration/integration_portal.php#3step_methodology)

# Notes

All attribute names recieved from NMI will be converted to `camelCase` for uniformity. Attribute names sent to NMI will be converted to the appropriate `hypen-case` and `param_case` where appropriate. Additionally, some fields are aliased (e.g, `postalCode` => `postal`) to provide consistent access between the Three Step and Query APIs. 

You can disable this completely by specifying `transform: false` in the configuration options.

Dispatched XML is generated by [xmlbuilder](https://github.com/oozcitak/xmlbuilder-js/wiki/Conversion-From-Object).

# Usage


## Setup
```
const nmi = require('nmi-node');
nmi.configure({
  apiKey: 'your-key-here',
  username: 'your-username',
  password: 'your-password'
});
```

## Transaction
```
// create a sale
nmi.transaction.create('sale', {
  amount: 2.99,
  redirectUrl: 'http://127.0.0.1/example',
  billing: {
    firstName: 'John',
    lastName: 'Doe'
  }
});

// execute a token
nmi.transaction.execute('the-token');
```

## Handling Errors
```
try {
  let txn = await nmi.transaction.execute('some-token');

  // success!

} catch(err) {

  if(err.isNMI) {
    // payment or gateway error - see err.response
  } else {
    // connection or outside error
  }

}
```