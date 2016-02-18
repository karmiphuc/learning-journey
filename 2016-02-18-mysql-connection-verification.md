## MySQL Connection Verification

> @karmiphuc: Really interesting thing about this is the matching algo - http://dev.mysql.com/doc/refman/5.1/en/connection-access.html

<hr/>

It is possible for the client host name and user name of an incoming connection to match more than one row in the user table. The preceding set of examples demonstrates this: Several of the entries shown match a connection from thomas.loc.gov by fred.

When multiple matches are possible, the server must determine which of them to use. It resolves this issue as follows:

- Whenever the server reads the user table into memory, it sorts the rows.

- When a client attempts to connect, the server looks through the rows in sorted order.

- The server uses the first row that matches the client host name and user name.

The server uses sorting rules that order rows with the most-specific Host values first. Literal host names and IP addresses are the most specific. (The specificity of a literal IP address is not affected by whether it has a netmask, so 192.168.1.13 and 192.168.1.0/255.255.255.0 are considered equally specific.) The pattern '%' means “any host” and is least specific. The empty string '' also means “any host” but sorts after '%'. Rows with the same Host value are ordered with the most-specific User values first (a blank User value means “any user” and is least specific). For rows with equally-specific Host and User values, the order is indeterminate.
