# SpamAssassin client

## Installation

Follow the [instructions](https://docs.halon.io/manual/comp_install.html#installation) in our manual to add our package repository and then run the below command.

### Ubuntu

```
apt-get install halon-extras-spamassassin
```

### RHEL

```
yum install halon-extras-spamassassin
```

## Exported functions

These functions needs to be [imported](https://docs.halon.io/hsl/structures.html#import) from the `extras://spamassassin` module path.

### spamc(fp[, options])

Client for the [SpamAssassin (spamd) Network Protocol](https://github.com/apache/spamassassin/blob/trunk/spamd/PROTOCOL).

**Params**

- fp `File` - the mail file
- options `array` - options array

**Returns**: class object.

The following options are available in the **opts** array.

- path `string` - Path to a the spamd unix socket.
- address `string` - Address of the spamd server. The default is `127.0.0.1`
- port `number` - TCP port. The default is `783`.
- user `string` - Username of the user for which the scan is being performed.
- sender `string` - Prepends a "Return-Path" header to the mail file with the provided envelope sender.
- size_limit `number` - Size limit in bytes. The default is 512 000.
- timeout `number` - Timeout in seconds. The default is 30 seconds.
- tls `array` - TLS settings.
- report `boolean` - Return symbols including scores per symbol. The default is false

The following options are available in the **tls** array.

- enabled `boolean` - Enable TLS for the specific socket
- opts `array` - All available options can be found on [here](http://docs.halon.se/hsl/functions.html?highlight=tlssocket#TLSSocket)

**Returns**: An associative array with a `spam` (boolean) if the message is spam, `score` (number) representing the spam score, `threshold` (number) representing the spam limit and a `symbols` property contaning all matched symbols (string) or in case of report = true all matched symbols with their corresponding scores. If an error occures an `error` property (string) is set containing the error message.
