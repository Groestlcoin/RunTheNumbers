# RunTheNumbers
 audit the total groestlcoin supply at future block height using your full node

This is a very simple script that runs in the command line. It's intended to be easy enough to use that anyone with a Groestlcoin node can participate without having extensive technical knowledge, but you do need a full node such as Groestlcoin Core to participate. Currently this script also relies on **Python** to parse the data it recieves from your node.

If you are a Windows user, the process requires extra steps which are not well defined, because this script is designed for Linux and Mac operating systems. A Python version will be released later.

# Why?

The goal is to coordinate the largest **synchronized decentralized audit** of Groestlcoin's monetary supply in history. Participants agree on a target block height, and the script will fetch the [block count](https://developer.bitcoin.org/reference/rpc/getblockcount.html) from your node every few seconds, counting down the remaining blocks

When the target block is reached, the script calls [gettxoutsetinfo](https://developer.bitcoin.org/reference/rpc/gettxoutsetinfo.html), which provides statistics about Groestlcoin's unspent transaction output set. If all goes well, users can take screenshots to post online to mark the occassion, and more importantly, verify that all nodes are in agreement about the total amount of groestlcoin in existence.

### Linux/MacOS users

1. Download [runthenumbers.sh](https://github.com/Groestlcoin/RunTheNumbers/raw/master/runthenumbers.sh) or save the raw text to a new file.

2. Copy the script to the machine that is running your node.

3. Locate your groestlcoin.conf file.

    a. If your data directory doesn't have a groestlcoin.conf file, create a new text file and save it as `groestlcoin.conf`.

    b. If your groestlcoin.conf file doesn't have the `rpcuser` and `rpcpassword` variables, go ahead and add them, save the file, and **restart your node**. They should look like this:

    `rpcuser=any_username`

    `rpcpassword=any_password`

4. Edit the script you downloaded so that the `USERNAME` and `PASSWORD` variables match your `rpcuser` and `rpcpassword` variables in your groestlcoin.conf file.

5. Also edit the `TARGET_BLOCK` variable to a future block date. Ideally you will select the same block to audit as other people, so that you can all compare results at the same time.

6. Open your command line or Terminal application. Navigate to the directory where you saved the script by using `cd` to *change directory*, followed by the file path to the script folder.

    `cd /path/to/folder`

7. Run the script:

    `sh runthenumbers.sh`

    or

    `bash runthenumbers.sh`

If the script runs successfully, you should see something like this:

  `3231325/3231500: 175 blocks remaining`

The script will listen to your node for new blocks and count down accordingly. Once the target block height is reached, the script will call `gettxoutsetinfo` which will return results like this:

    {
      "height": 3231325,
      "bestblock": "0000000000000239fd6e87f636cde4963849b3036bfcec2b8cb4505a4354b48d                                                                                                             ",
      "transactions": 160874,
      "txouts": 436844,
      "bogosize": 32786848,
      "hash_serialized_2": "618d7a0f0a3bd4c8fb7ee2b8ca90c089334201a3a41729ced39e2bc7b836b7c2",
      "disk_size": 24003816,
      "total_amount": 75764513.88738880
    }

See that `total_amount` line? You just verified exactly how many groestlcoin exist right now!

Take a screenshot of the output and post your results to social media using the [#RunTheNumbers](https://twitter.com/search?q=%23RunTheNumbers&src=typed_query&f=live) hashtag to compare the output of your node with that of your friends' nodes.
