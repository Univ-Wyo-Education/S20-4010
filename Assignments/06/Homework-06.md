## Assignment 6 - Develop a Document Contract.

One of the common uses of the blockchain is as a proof of authenticity
for external data.   The way that this works is to take some set of external
data, generate a hash for that data (SHA1 hash, or PGP2 signature example) and then write the
hash to the chain.  The outside code is reasonably streight forward -
in some fashion you read a document, hash it - then you call a smart contract
on chain to store the data on chain.   The on chain contract
provides the time and proof of authenticity.

A number of companies are using this kind of a system.  There is an ISO900/ISO9002 document
tracking company that is doing this.   IOHK / BeefChain is using this approach for supply chain tracking.

This is often referred to as a "metta-data tracking" system.

In this homework we will implement the smart contract in Ethereum/Solidity to do the
on-chain tracking.   You will need to write the contract and to develop some tests
that show that your contract works.

Develop the contract using truffle and solidity.

Turn in your contract and the test code.

400pts - due - Apr 15th.





Take a "document" signature and associate it with a user/acct - to mark the 
	1. Keep track of a users set of documents
	2. Allow search for a document "hash" to see when signed
	3. Keep validity of documents - time when signed
	4. Sign based on user-hash / notization signature (mult-sig)

Contract

	Data
		User [ acct ] [ Document Hash ]
		NoterizationSignature [ acct ] [ Document Hash ]
		Norterizers [ acct ]
		PayAmt

	Constructor

	Set Payment ( pay ) - Only Owner

	Register Document ( Act, Hash ) + Payment		// Save document with user info

	Notarize Document ( msg.sender==Notarizer,  Act , Hash )				// Mark document as noterized

	List Documents ( acct, nth=0..N-1 )	// Return info on a document
	N of Documents ( acct )	 // get # of documents that a user has


	List Documents by Date
	N of List Documents by Date


	List Documents by Notarizer
	N of List Documents by Notarizer

	TransferPaymet

