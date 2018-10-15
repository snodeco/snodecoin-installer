# [Snodecoin](https://snode.co).  

Shell script to install a Snodecoin Masternode on a Linux server running Ubuntu 16.04. Use it on your own risk.
***

## VPS installation for version **3.0.0**
```
wget -N https://raw.githubusercontent.com/snodeco/snodecoin-installer/master/snodecoin-installer.sh
bash snodecoin-installer.sh
```
***

## Desktop wallet setup

After the Masternode is up and running, you need to configure the desktop wallet accordingly. Here are the steps:
1. Open the Snodecoin Desktop Wallet.
2. Go to RECEIVE and create a New Address: **MN1**
3. Send **10000** SND to **MN1**. You need to send all 10000 coins in one single transaction.
4. Wait for 15 confirmations.
5. Go to **Help -> "Debug Window - Console"**
6. Type the following command: **masternode outputs**
7. Go to  **Tools -> "Open Masternode Configuration File"**
8. Add the following entry:
```
[Alias] [Address] [Privkey] [TxHash] [TxIndex]
```
* Alias: **MN1**
* Address: **VPS_IP:PORT**
* Privkey: **Masternode Private Key**
* TxHash: **First value from Step 6**
* TxIndex:  **Second value from Step 6**
9. Save and close the file.
10. Go to **Masternode Tab**. If you tab is not shown, please enable it from: **Settings - Options - Wallet - Show Masternodes Tab**
11. Click **Update status** to see your node. If it is not shown, close the wallet and start it again. Make sure the wallet is unlocked.
12. Select your MN and click **Start Alias** to start it.
13. Alternatively, open **Debug Console** and type:
```
startmasternode alias false MN1
```
14. Login to your VPS and check your masternode status by running the following command to confirm your MN is running:
```
snodecoin-cli masternode status
```
***

## Usage:
```
snodecoin-cli masternode status
snodecoin-cli getinfo
snodecoin-cli mnsync status
```
Also, if you want to check/start/stop **Snodecoin**, run one of the following commands as **root**:

```
systemctl status SND #To check if Snodecoin service is running
systemctl start SND #To start Snodecoin service
systemctl stop SND #To stop Snodecoin service
systemctl is-enabled SND #To check if Snodecoin service is enabled on boot
```
***

## Masternode update:
In order to update your Snodecoin Masternode to version 3.0.0, please run the following commands:
```
# stop service
systemctl stop SND

# create backup
cp -r ~/.snodecoin ~/.snodecoin.bakup

# remove data from old wallet
rm -rf ~/.snodecoin/*

# copy the wallet and config files back
cp ~/.snodecoin.bakup/wallet.dat ~/.snodecoin.bakup/snodecoin.conf ~/.snodecoin.bakup/masternode.conf ~/.snodecoin

# download new wallet 
cd /tmp
wget -N https://github.com/snodeco/snode-coin/releases/download/v3.0.0/snodecoin-3.0.0-linux64.tar.gz
tar xvzf snodecoin-3.0.0-linux64.tar.gz --strip 2
chmod +x snodecoind snodecoin-cli
mv snodecoind snodecoin-cli /usr/local/bin

#start it
systemctl start SND
rm snodecoin-3.0.0-linux64.tar.gz

snodecoin-cli getinfo
```
Open your desktop wallet and start the node from there.
***

## Donations
Any donation is highly appreciated


