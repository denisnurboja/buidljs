# Buidl.js 

Buidl.js is a wrapper for the bitcoinjs-lib library. This is intended as a tool for developers, curious hobbyists and crypto-enthusiasts looking for an easy way to programmably create bitcoin keys, and build and sign transactions offline. These transactions are live bitcoin transactions that could potentially be broadcast to a node or API if you choose. This wrapper is a simplified approach to bitcoin javascript development for beginners without having to learn the bitcoinjs-lib library, which means it is very limited in features and customizations compared to what one can do with bitcoinjs-lib. It is NOT intended for production use -- it is 100% client-side javascript. USE AT YOUR OWN RISK.

# Usage    

## 0. Save a copy of buidl.js or clone the repo

 *  `git clone https://github.com/coinables/buidljs.git`
 
NOTE: If you cloned the repository the create.js file is the pre-browserify source to buidl.js.
 
## 1. Include `buidl.js` in your HTML

 *  `<script src="path/to/buidl.js"></script>`


## 2. Create a random key pair

        <head>
		<script src="buidl.js"></script>
		</head>
		<body>
		<script>
		let newPair = buidl.createP2PKH();
		let address = newPair.addr;
		let privateKey = newPair.pk;
		console.log(address, privateKey);
		</script>
		</body>

## 3. Create key pair from sha256 hash of an input aka brainwallet

		<head>
		<script src="buidl.js"></script>
		</head>
		<body>
		<script>
		let newPair = buidl.createFrom("satoshi");
		let address = newPair.p2pkh;
		let privateKey = newPair.pk;
		console.log(address, privateKey);
		</script>
		</body>

## 4. Get details of a private key

        <head>
		<script src="buidl.js"></script>
		</head>
		<body>
		<script>
		let WIF = "L4tm7p16LZ7e3EwydFTNFBDdknKrU7E1e6iXxkbFSF4FDFxcnyXG";
		let details = buidl.getDetails(WIF);
		console.log(details);
		</script>
		</body>

		
## 5. Build and sign a transaction 

 * createTransaction(typei, txidi, outni, outputi, amounti, wifi, changeout, changeamt, inputvalue)
 
 typei - string, indicate input type by using the first character of address type spending from      
 txidi - string, transaction id of unspent output being spent       
 outni - integer, nout value of the unspent output being spent      
 outputi - string, address of output "receiving" address      
 amounti - integer, amount to send to output in satoshis (100,000,000 satoshis = 1 BTC)        
 wifi - string, WIF private key of unspent output being spent      
 changeout - string, Optional, change address or 2nd output address      
 changeamt - integer, Optional, amount in satoshis to send to change address      
 inputvalue - integer, Only required when spending from segwit unspent outputs, this is the full value of the unspent output being spent       	
 
		createTransaction("1", "34eceJ...  > spends from p2pkh
		createTransaction("3", "34eceJ...  > spending from p2sh-p2wpkh
		createTransaction("b", "34eceJ...  > spending from p2wpk(bech32)

		createTransaction("3", "34eceJ..", 0, "1P5Ef7FsaD1KsJNSTUcACceEWN9vsUe3eN", 350000, "L1RLQhjuGoQ37QP4jfaEFTHMuEUeh4JdUDkx32xeafhnpzRMDMXD", null, null, 4000000)
		
		//returns {"signedtx":"894291f54d..."}

This function will return an object with the key "signedtx" which will contain the raw hex signed transaction that can now be broadcast to any node or API.		
		
See test.html for an example of using the `createTransaction()` function.    

	
## Available Functions

`createP2PKH` - Creates a random legacy Pay-to-Public-Key-Hash key pair     
`createP2WPKH` - Creates a random native (bech32) segwit key pair      
`createP2SHP2WPKH` - Creates a random p2sh wrapped segwit key pair      
`getNewAddress` - Creates a random key pair and outputs all 3 address types (P2PKH, P2WPKH, P2SH-P2WPKH)      
`createFrom("molly aqua jump tuba ratchet while")` - 1 parameter (string). Creates a key pair from a sha256 of an arbitrary string a.k.a. brain wallet.      
`getDetails("L1RLQhj...")` - 1 parameter (string). Takes a WIF private key and outputs all 3 address types, redeem script and public key      
`validateAddress("bc1hq...")` - 1 parameter (string). Returns true if input is a valid bitcoin address      
`createTransaction` - 9 Parameters see Section 5 above. Builds and signs a raw transaction    
`bip38Encrypt("L1RLqh...","satoshi")` - 2 parameters (string, string). Takes a WIF private key and a passphrase to encrypt the private key using BIP38.      
`bip38Decrypt("6PYUz..","satoshi")` - 2 parameters (string, string). Takes a BIP38 encrypted key and a passphrase to reveal the decrypted WIF private key.   


Please consider donating if you find this tool useful.		

BTC:  3LnBzPmb3BkDUZBHLHdEj5vgxS6D6HjKLW


