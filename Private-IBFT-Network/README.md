# Privacy Enabled Hyperledger Besu
Implement besu nodes with privacy using tessera

export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export PATH=$PATH:/mnt/e/Tessera/tessera-21.10.0/bin
/mnt/e/Tessera/tessera-21.10.0/bin

## Prerequisites
1. Install Tessera -> https://docs.tessera.consensys.net/en/stable/HowTo/Get-started/Distribution/
2. Setup up environment variable -> export PATH=$PATH:/mnt/e/Tessera/tessera-21.10.0/bin
3. tessera -keygen -filename nodeKey
4. tessera -configfile config.json
5. curl http://localhost:9081/upcheck
6. Start Tessera Node in each Node directory 
`tessera -configfile tessera.conf`
7. Start besu nodes
 a) besu --data-path=data --genesis-file=../genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,EEA,PRIV --host-allowlist="*" --rpc-http-cors-origins="all" --privacy-enabled --privacy-url=http://127.0.0.1:9102 --privacy-public-key-file=Tessera/nodeKey.pub --min-gas-price=0

 b) besu --data-path=data --genesis-file=../genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,EEA,PRIV --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546 --privacy-enabled --privacy-url=http://127.0.0.1:9202 --privacy-public-key-file=Tessera/nodeKey.pub --min-gas-price=0

c) besu --data-path=data --genesis-file=../genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,EEA,PRIV --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8547 --privacy-enabled --privacy-url=http://127.0.0.1:9302 --privacy-public-key-file=Tessera/nodeKey.pub --min-gas-price=0  

d) besu --data-path=data --genesis-file=../genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,EEA,PRIV --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8548 --privacy-enabled --privacy-url=http://127.0.0.1:9402 --privacy-public-key-file=Tessera/nodeKey.pub --min-gas-price=0