# Programming Concepts

The Vyper Hello World !

```python

@view
@external
def answer_to_everything() -> uint256:
    return 42

``` 

## From Computers to the EVM

In the old era code or software is often run on your usual computer, a computer is in essence an information processing unit with various *bridges* to the outside world such as keyboards for user input, screens for output etc...

When we are in the context of Ethereum we will use the words code, program and smart contract interchangebly (they represent the same thing).

In a similar analogy **Ethereum** is a blockchain-based computer, the blockchain represents a historical record of every **transaction** that happened on-chain. Here the blockchain represents an *authenticated* hard-drive.
The [*state trie*](https://eth.wiki/en/fundamentals/patricia-tree) represents the last known live view of the hard-drive wallets are *keyboards* and [etherscan.io](https://etherscan.io) the screen.

From information processing computers rely on *CPUs* which in Ethereum on the otherhand to process transactions and code we rely on the EVM.

![eth-state-computer-analogy](../assets/eth-analogy.png)

Let's start with a simple example[^1] [transaction](https://etherscan.io/tx/0x211b2babfeec81dcecb544a2343d4006b41bc708ea7d54bd6ae0d43250ab1e29):

![example-transaction](../assets/example-tx-1.png)

From the summary you can see that the transactions *revoked* access to a user's token from the *1.inch* exchange.

This action simply tells the Ethereum state that the *1.inch* smart contract isn't approved to **spend** the user's *SHIB* tokens.

Let's unpack this because it is kinda complex. When you go to *1.inch* to execute a swap (i.e exchange tokens) you need to first **approve** an amount of tokens that the *1.inch* contract can access and execute the swap.

This *approve* step essentially permits the *1.inch* token to move your token once you sign the second transaction that does the actual
swap.

By going to **Logs** tab you can see clearly which *function* was called in the *SHIB* contract in this example `approve` with value 0[^2] for balance and with spender address `0x11111112542d85b3ef69ae05771c2dccff4faa26`[^3] .

![example-transaction-logs](../assets/example-tx-1-logs.png)

[^1]: Etherscan summarizes all the effects a single transaction can have on the world state.
[^2]: The ERC20 standard describes a generic smart contract implementation for a form of pseudo-bank.
[^3]: This is the mainnet address of the [1.inch](https://app.1inch.io/) smart contract which is an exchange router.

## The Ethereum World State

In the above drawing we used the word *World State* to describe the __environment__ that encodes the last
known state version, as transactions arrive bundled in blocks all the transaction in that block execute
and give use a new version of the state.

Because the blockchain records all the blocks (blocks are *state transitions* in a more precise language) you can 
always *replay* back the full state history.

When an Ethereum node first joins the network it does just that, it will replay all past blocks until it *syncs* meaning has the same state as all the other nodes in the network[^4].

<figure>
  <img src="../assets/eth-state-trie-advanced.png" width="600" />
  <figcaption>What the State Trie really looks like courtesy of <a href="https://ethereum.stackexchange.com/questions/268/ethereum-block-architecture">atomh33ls</a></figcaption>
</figure>


[^4]: With [snapsync](https://blog.ethereum.org/2020/07/17/ask-about-geth-snapshot-acceleration/) nodes now can sync only a last known good copy of the state trie and replay the last *k*-blocks.
