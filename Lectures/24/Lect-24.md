Lecture 24 - Zero Knowledge Identification System
=====================================

Paper: [https://arrow.dit.ie/cgi/viewcontent.cgi?article=1031&context=itbj](https://arrow.dit.ie/cgi/viewcontent.cgi?article=1031&context=itbj)

Look at page 38, section 7.9. to 7.12 on page 43 (this is the page numbers in the PDF - it is the 28th page OF the PDF).

Walk through of algorithm with the example from the paper.

Also see: [https://blog.cryptographyengineering.com/2017/01/21/zero-knowledge-proofs-an-illustrated-primer-part-2/](https://blog.cryptographyengineering.com/2017/01/21/zero-knowledge-proofs-an-illustrated-primer-part-2/)

Also: the reading from last time - has a nice section on this method for identification of users.


First a tiny detour - how to authenticate a QR or RFID tag.
-------------------------------------------------------------

QR codes encode some sort of text.  Some RFID tags encode just a number.  Others like NFC encode a chunk of text between 84 and 1084 characters long.
Usually these chunks of text are URLs to some website or set of information.   People would like to use the tags as proof-of-authenticity.   The problem
is how to get them to be secure.   NFC tags can have computation built int - but it is really a small amount - the power for the NFC is coming from
radio waves being transmitted from the source.  So you take you Android and its tiny transmitter and send the NFC tag a tiny bit of power - that then
looses lots of power because it has to be picked up by a tiny antenna in the "chip" and then used to do a small, small amount of computation and then
using that same power send back an answer.  So building any kind of "authentication" that is meaningful into the chip is difficult.
A QR code is a static image - so it will not do any computation at all.

So if you can't do the authentication on the chip or device.  What about just adding Two Factor Authentication after the device is scanned.
Basically have the QR or RFID send you to a page where you have to authenticate using a device (iPhone, Android) and provide proof of your
authenticity at that point.


Zero knowledge proof for use as ID
----------------------------------

```
package main

import (
    "fmt"
    "math/big"
)

// From: https://arrow.dit.ie/cgi/viewcontent.cgi?article=1031&context=itbj
// IdProtocalsInCrypto.pdf

func main() {
    // From p40
    p := big.NewInt(88667)
    q := big.NewInt(1031)
    alpha := big.NewInt(70322)
    a := big.NewInt(755)

    // v = (alpha ^ ( q-a )) % p
    t1 := big.NewInt(0)
    t1.Sub(q, a)
    v := big.NewInt(0)
    v.Exp(alpha, t1, p)

    fmt.Printf("Setup Complete: v=%s\n", v)

    // Alice is the Client:

    // ----------------------------------------------------------
    // Message 1 - Client to Server
    // ----------------------------------------------------------

    // Alice Chooses, and send to Bob
    r := big.NewInt(543) // Should be random, but for this example
    x := big.NewInt(0)
    x.Exp(alpha, r, p) // x=(alpha^r) % p

    fmt.Printf("Send To Bob : x=%s\n", x)

    // ------------------------------------------------------------------------
    // Response to Message 1, Server back to client
    // ------------------------------------------------------------------------

    // Bob is the Server:
    // Bob sends the challenge 'e' back to Alice e to do the computation
    e := big.NewInt(1000) // how chose (random?)

    // Alice now computes: y = a*e % q
    t2 := big.NewInt(0)
    t2.Mul(a, e)
    t2.Mod(t2, q) // 45664
    t2.Add(t2, r) // 851 is correct

    y := t2
    fmt.Printf("y=%s\n", y) // Prints 851

    // ------------------------------------------------------------------------
    // Message 2 - Client (Alice) with response to challenge.
    // ------------------------------------------------------------------------

    // Bob (server) verifies: x == z == (a^y) * (v^e) % p
    // Bob (server) verifies: x == z == ((a^y)%p)*((v^e)%p) % p

    t3 := big.NewInt(0)
    t3.Exp(alpha, y, p)
    t4 := big.NewInt(0)
    t4.Exp(v, e, p)
    t5 := big.NewInt(0)
    t5.Mul(t3, t4)
    t5.Mod(t5, p)

    z := t5
    fmt.Printf("z=%s\n", z)

    // ------------------------------------------------------------------------
    // Response 2 - Success/Fail message from server back to client
    // ------------------------------------------------------------------------
    if x.Cmp(z) == 0 {
        fmt.Printf("Authoized! Yea\n")
    } else {
        fmt.Printf("Nope nope nope\n")
    }

}

```


