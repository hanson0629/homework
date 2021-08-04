# Blockchain Wallet


1. Project Setup
    - Clone the hd-wallet-derive tool into the wallet folder and install it.
    - Enter the following commands into terminal:
        - export MSYS=winsymlinks:nativestrict
        - ln -s hd-wallet-derive/hd-wallet-derive.php derive
        - ./derive --key=xprv9zbB6Xchu2zRkf6jSEnH9vuy7tpBuq2njDRr9efSGBXSYr1QtN8QHRur28QLQvKRqFThCxopdS1UD61a5q6jGyuJPGLDV9XfYHQto72DAE8 --cols=path,address --coin=ZEC --numderive=3 -g
![Alt text](Resources/wallet.PNG)

2. wallet setup
    - Create a file called wallet.py -- this will be your universal wallet script.
    - Create a file called constants.py containing the following:
        - BTC = 'btc'
        - ETH = 'eth'
        - BTCTEST = 'btc-test'
3. derive wallet key
    - Create a function called derive_wallets that does the following:
        - Use the subprocess library to create a shell command that calls the ./derive script from Python. Make sure to properly wait for the process. Windows Users may need to prepend the php command in front of ./derive like so: php ./derive.
        - The following flags must be passed into the shell command as variables:
            - Mnemonic (--mnemonic) must be set from an environment variable, or default to a test mnemonic
            - Coin (--coin)
            - Numderive (--numderive) to set number of child keys generated
            - Format (--format=json) to parse the output into a JSON object using json.loads(output)
    - Then create a dictionary object called coins that uses the derive_wallets function to derive ETH and BTCTEST wallets.
![Alt text](Resources/address.PNG)
4. transaction
    - Use bit and web3.py to leverage the keys stored in the coins object by creating three more functions:
        - priv_key_to_account:
            - This function will convert the privkey string in a child key to an account object that bit or web3.py can use to transact.
            - This function needs the following parameters:
                - coin -- the coin type (defined in constants.py).
                - priv_key -- the privkey string will be passed through here.


    - create_tx:
        - This function will create the raw, unsigned transaction that contains all metadata needed to transact.

    - send_tx:
        - This function will call create_tx, sign the transaction, then send it to the designated network.

    - Now its time to fund the wallets.
![Alt text](Resources/transaction.PNG)

![Alt text](Resources/confirm.PNG)

![Alt text](Resources/transaction2.PNG)

![Alt text](Resources/confirm2.PNG)