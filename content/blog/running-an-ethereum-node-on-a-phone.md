+++
author = "Vimarsh"
categories = ["Tutorial", "Crypto", "Tech"]
date = 2022-03-14T18:30:00Z
description = ""
images = ["/uploads/ 2022/06/ethereum-on-a-computer-decor-image-by-kanchanara.jpg"]
tags = ["Running a node", "Crypto", "Ethereum"]
title = "Running an Ethereum node on a phone"
url = "/blog/running-ethereum-node-on-your-phone"

+++
Whenever you are using a cryptocurrency to transact with someone, you are trusting the node to provide you with correct details and properly executing the trade. When using Metamask, by default you use the Ethereum node provided by [infura](https://infura.io/). In general they are not rogue and will not 'scam' you, but for several reasons you might want to run your own node.

![Ethereum coin on computer (decor image)](/uploads/ 2022/06/ethereum-on-a-computer-decor-image-by-kanchanara.jpg)

## These reasons:

* Infura (or some other provider) might be legally asked to not server users in your region. This supposedly happened with users in Venezuela. But this yields massive power, where you could just not be able to send your Ethereum or make it a hassle.
* Nodes might be hacked and exploited, reporting you wrong details and so forth.
* There is a massive trust you need to keep with these node providers (be it Coinbase wallet, Metamask, etc.) kinda defeating purpose of not relying on a third party.

## 'Solution'

_Just run your own node._ This unfortunately is quite difficult for most people. Ethereum requires 500 GB+ in storage, good internet connection and a decent machine. People don't have that nor do they carry it with them. Ethereum hence provides an option with its geth client called “light” sync mode. A light node basically, stores the headers of all blocks. It can verify the validity all of the data against the roots in the chain. For everything else (like requesting data, sending a transaction, executing a smart contract, signing a transaction, etc) it contacts a full node and asks the node to do it for you. If a node goes rogue, then based on the changes of Merkle tree, it will invalidate the chain.

This basically provides you with ability to personally verify whatever these node providers are saying, with several sources of information and use the chain. With zK-SNARKS this could be taken to a whole new trustless model, which is already [being researched](https://eprint.iacr.org/2021/1657.pdf) on.

You can [simply](https://ethereum.org/en/developers/tutorials/run-light-node-geth/) run a light node on your PC, without a lot of problem. But, what if you run it on your phone...

## Running Ethereum light node on an android phone

* Install termux from [fdroid](https://f-droid.org/en/packages/com.termux/) on your Android phone. If you are using a closed platform _iOS_, well get an open one.
* To make your life easier, you could access your phone via SSH from your laptop and run from there. (This is mostly for my reference though, could be useful) [details](https://wiki.termux.com/wiki/Remote_Access)

      # Installing openSSH
      
      pkg install openssh
      
      # Get the username
      
      whoami
      
      # Setup a password
      
      passwd
      
      # Get IP address of your phone
      
      ifconfig
      
      # Run openSSH server
      
      sshd
      
      # It will be running and accessible on <ip-address>:8022 by default
* Install geth Termux maintains a latest [packaged](https://github.com/termux/termux-packages/tree/master/packages/geth) copy of geth, which you can install simply by `pkg install geth`
* Run the light node `geth --syncmode "light" --http` [details for CLI options](https://geth.ethereum.org/docs/interface/command-line-options)

geth will start syncing the node, although it won't take time and will consume way less space. You can now add [http://127.0.0.1:8545](http://127.0.0.1:8545/) as a new RPC endpoint on your Metamask app on phone. One could also use something like [fast reverse proxy](https://github.com/fatedier/frp) to access it remotely by tunneling it via a VPS.

## ummm...

Here you are still trusting the nodes from where your light node is syncing data from to provide you with correct data. Very often then not only a few nodes will be shown connected and those which you are syncing with. So verifying the state is still important, but this reduces the chances of any of above mentioned problems.

Thanks to [Krish](https://krishpatel.cc/) and [Aryan](https://aryantiwari.com/) for helping with this post.