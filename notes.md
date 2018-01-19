magic bytes:pchMessageStart
28 91 173 51 => 0x1c 0x5b 0xad 0x33 =>0x1c5bad33

POW
129,600 (last block) * 60 = 7,776,000 (POW coins)

PORT


Set up a swapfile if your system has less than 1.5GB of memory:

fallocate -l 2G /swapfile
chown root:root /swapfile
chmod 0600 /swapfile
sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"
mkswap /swapfile
swapon /swapfile

If fallocate doesn’t work, you can use dd if=/dev/zero of=/swapfile bs=1024 count=1024288 instead.

Initialize swapfile automatically on boot

nano /etc/fstab
Add this at the bottom: /swapfile none swap sw 0 0

Install all required dependencies:

apt-get update && apt-get upgrade
apt-get install ntp unzip git build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev libqrencode-dev aptitude && aptitude install miniupnpc libminiupnpc-dev

Pull the source code from github, or upload it yourself:

git clone https://github.com/YOURCOIN

If your coin uses leveldb, compile leveldb:

cd /YOURCOIN/src/leveldb
chmod +x build_detect_platform
make clean
make libleveldb.a libmemenv.a

Return to source directory, and compile the daemon:

cd /YOURCOIN/src
make -f makefile.unix

Strip the file to make it smaller, then relocate it:

strip YOURCOINd
cp YOURCOINd /usr/bin

Now run the daemon:

YOURCOINd

It will return an error, telling you to set up config file in a directory. Now we’ll set up the config file. Note that this is case sensitive.

nano ~/.YOURCOIN/YOURCOIN.conf

Add the following, save and exit:

daemon=1
server=1
rpcuser=(username)
rpcpassword=(strong password)

Run YOURCOINd once more and if you did everything correctly, your daemon is now online! Type YOURCOINd help for a full list of commands available.

run second node
./bitcoinead2 --daemon -datadir=/home/tide/.bitcoinea2 -connect=127.0.0.1:9090

QT make:
qmake RELEASE=1 USE_UPNP=1 BitcoinEA-qt.pro

genesis 0
https://github.com/lhartikk/GenesisH0
https://github.com/Peershares/Peershares/wiki/Genesis-Block-(Starting-a-New-Blockchain-Instance)

mainnet
CBlock(hash=000001351d910fa41a37321874fd820aad78eebe805601d7307095df4c1a460a, ver=1, hashPrevBlock=0000000000000000000000000000000000000000000000000000000000000000, hashMerkleRoot=0fd69a42fb9e9901f35724f272c6180a4cd11bbcd256180ca42019ed2cb54f54, nTime=1514991909, nBits=1e0fffff, nNonce=407333, vtx=1, vchBlockSig=)
  Coinbase(hash=0fd69a42fb, nTime=1514991909, ver=1, vin.size=1, vout.size=1, nLockTime=0)
      CTxIn(COutPoint(0000000000, 4294967295), coinbase 00012a2d576564202033204a616e2031383a30383a303620454154203230313820424954434f494e454120535441525453)
          CTxOut(empty)
            vMerkleTree: 0fd69a42fb 
            block.GetHash() == 000001351d910fa41a37321874fd820aad78eebe805601d7307095df4c1a460a
            block.hashMerkleRoot == 0fd69a42fb9e9901f35724f272c6180a4cd11bbcd256180ca42019ed2cb54f54
            block.nTime = 1514991909 
            block.nNonce = 407333 
            scriptsig = 0 42 576564202033204a616e2031383a30383a303620454154203230313820424954434f494e454120535441525453

testnet
CBlock(hash=0000f121caca746c65613e9e374a88763401ebc998116f7109dca834c5449c16, ver=1, hashPrevBlock=0000000000000000000000000000000000000000000000000000000000000000, hashMerkleRoot=0fd69a42fb9e9901f35724f272c6180a4cd11bbcd256180ca42019ed2cb54f54, nTime=1514494712, nBits=1f00ffff, nNonce=45552, vtx=1, vchBlockSig=)
  Coinbase(hash=0fd69a42fb, nTime=1514991909, ver=1, vin.size=1, vout.size=1, nLockTime=0)
      CTxIn(COutPoint(0000000000, 4294967295), coinbase 00012a2d576564202033204a616e2031383a30383a303620454154203230313820424954434f494e454120535441525453)
          CTxOut(empty)
            vMerkleTree: 0fd69a42fb 
            block.GetHash() == 0000f121caca746c65613e9e374a88763401ebc998116f7109dca834c5449c16
            block.hashMerkleRoot == 0fd69a42fb9e9901f35724f272c6180a4cd11bbcd256180ca42019ed2cb54f54
            block.nTime = 1514494712 
            block.nNonce = 45552 
            scriptsig = 0 42 576564202033204a616e2031383a30383a303620454154203230313820424954434f494e454120535441525453 




mainnet:
CBlock(hash=0000051347d04550049f5c6414394127bad6a6d6798a2877c77a01b93c2977c5, ver=1, hashPrevBlock=0000000000000000000000000000000000000000000000000000000000000000, hashMerkleRoot=1acc7a3c756f1800868468a75e37828a3a374cb12760e19de51e17e90d06ad5c, nTime=1514494712, nBits=1e0fffff, nNonce=413474, vtx=1, vchBlockSig=)
  Coinbase(hash=1acc7a3c75, nTime=1514494712, ver=1, vin.size=1, vout.size=1, nLockTime=0)
      CTxIn(COutPoint(0000000000, 4294967295), coinbase 00012a1e444543454d424552203230313720424954434f494e454120535441525453)
          CTxOut(empty)
            vMerkleTree: 1acc7a3c75 
            block.GetHash() == 0000051347d04550049f5c6414394127bad6a6d6798a2877c77a01b93c2977c5
            block.hashMerkleRoot == 1acc7a3c756f1800868468a75e37828a3a374cb12760e19de51e17e90d06ad5c
            block.nTime = 1514494712 
            block.nNonce = 413474
testnet:
CBlock(hash=00009bd068052e9485896a6b1ec648aa09f9755b558159f09ea5cd2fe08c07b8, ver=1, hashPrevBlock=0000000000000000000000000000000000000000000000000000000000000000, hashMerkleRoot=1acc7a3c756f1800868468a75e37828a3a374cb12760e19de51e17e90d06ad5c, nTime=1514494712, nBits=1f00ffff, nNonce=6300, vtx=1, vchBlockSig=)
  Coinbase(hash=1acc7a3c75, nTime=1514494712, ver=1, vin.size=1, vout.size=1, nLockTime=0)
      CTxIn(COutPoint(0000000000, 4294967295), coinbase 00012a1e444543454d424552203230313720424954434f494e454120535441525453)
          CTxOut(empty)
            vMerkleTree: 1acc7a3c75 
            block.GetHash() == 00009bd068052e9485896a6b1ec648aa09f9755b558159f09ea5cd2fe08c07b8
            block.hashMerkleRoot == 1acc7a3c756f1800868468a75e37828a3a374cb12760e19de51e17e90d06ad5c
            block.nTime = 1514494712 
            block.nNonce = 6300

