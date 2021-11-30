# Hyperledger Besu
Understanding how to setup and interact with a hyperledger besu POA blockchain network


## Prerequisites
1. Install Hyperledger Besu => https://besu.hyperledger.org/en/stable/HowTo/Get-Started/Installation-Options/Install-Binaries/
2. Install Curl => https://curl.haxx.se/download.html
3. If on windows installing windows terminal + wsl + ubuntu will also be usefull



## Setting up hyperledger nodes

Instead of repeating the steps just follow along with the reference link below everything needed can be found there.

# References

https://besu.hyperledger.org/en/stable/Tutorials/Private-Network/Create-IBFT-Network/


# Useful commands

1. Sets environment variables 
`export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64`

2. Generates node keys from genesis file
`besu operator generate-blockchain-config --config-file=ibftConfigFile.json --to=networkFiles --private-key-file-name=key`

3. Start first Node
`besu --data-path=data --genesis-file=..\genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all"`

4. Start Second Node
`besu --data-path=data --genesis-file=..\genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546`

5. Start Third Node
`besu --data-path=data --genesis-file=..\genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8547`

6. Start Fourth Node
`besu --data-path=data --genesis-file=..\genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8548`





Blockchain Explorer
 docker run --rm -p 8080:80 -e APP_NODE_URL=http://localhost:8545 alethio/ethereum-lite-explorer