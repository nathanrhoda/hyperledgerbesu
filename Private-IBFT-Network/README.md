# Privacy Enabled Hyperledger Besu
Implement besu nodes with privacy using tessera

export PATH=$PATH:/mnt/e/Tessera/tessera-21.10.0/bin
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

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



# Adding a tenant

1. In Node-1 folder Generate a private key for operator who uses key pair  to authenticate tenant JWT
`openssl genrsa -out privateKey.pem 2048`
`openssl rsa -pubout -in privateKey.pem -pubout -out publicKey.pem`

2. Generate tessera node keys for 2 additional tenants
`tessera -keygen -filename nodeKey2`
`tessera -keygen -filename nodeKey3`

3. Restart tessera nodes in respective node folders
`tessera -configfile tessera.conf`

4. Restart besu node 1
`besu --data-path=data --genesis-file=../genesis.json --rpc-http-authentication-enabled --rpc-http-authentication-jwt-public-key-file=./publicKey.pem --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,EEA,PRIV --host-allowlist="*" --rpc-http-cors-origins="all" --privacy-enabled --privacy-url=http://127.0.0.1:9102 --privacy-multi-tenancy-enabled --min-gas-price=0`

5. Restart remaining besu nodes
 `besu --data-path=data --genesis-file=../genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,EEA,PRIV --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546 --privacy-enabled --privacy-url=http://127.0.0.1:9202 --privacy-public-key-file=Tessera/nodeKey.pub --min-gas-price=0`

`besu --data-path=data --genesis-file=../genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,EEA,PRIV --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8547 --privacy-enabled --privacy-url=http://127.0.0.1:9302 --privacy-public-key-file=Tessera/nodeKey.pub --min-gas-price=0`  

`besu --data-path=data --genesis-file=../genesis.json --bootnodes=enode://76a7f73431e81475f9d8425c97e85eb7378d946fd4d28e8129db43df35105fb7037618897d8601bbacfb57969e9dc1db92b8dd967cff88503ab858f1676ca6f6@127.0.0.1:30303 --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT,EEA,PRIV --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8548 --privacy-enabled --privacy-url=http://127.0.0.1:9402 --privacy-public-key-file=Tessera/nodeKey.pub --min-gas-price=0`

6. Create a JWT
 - Navigate to https://jwt.io/
 - Change algorithm to RS256
 - Update below payload with tenants public key found in tessara folder
    {
        "permissions": ["*:*"],
        "privacyPublicKey": "<Enter tenants tessara public key ie. 2UKH3VJThkOoKskrLFpwoxCnnRARyobV1bEdgseFHTs=>",
        "exp": 1600899999002
    }

    {
        "permissions": ["*:*"],
        "privacyPublicKey": "ROjLp9sasnwq+C/otYZxrgNPqg+lFpSonl56AOobjTM=",
        "exp": 1669470202000
    }
- Paste above payload in payload data section and generate a jwt

- update curl to have token and, api mehod and urls

curl -X POST -H 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwZXJtaXNzaW9ucyI6WyIqOioiXSwicHJpdmFjeVB1YmxpY0tleSI6IlJPakxwOXNhc253cStDL290WVp4cmdOUHFnK2xGcFNvbmw1NkFPb2JqVE09IiwiZXhwIjoxNjAwODk5OTk5MDAyfQ.KICEhdYbhCjQKZGV_s7g_e8cAyfekUn5_f57EgLyY4O4wxs-VJFgG2Bh5zzhxXHpOwYEOMQmv6hxxBvowG4keT7BH39xx_j_76aGZd7Lz0wogM1qug6fciObWk30Y4u7w8vMJfheI8uWGX0bgAJsCxoy9JKo0t0p_jCVCOcBUISFAVcHRkpARpHlPDrmShqhJTJ66Lo-cYqhq_vDtCTS-dC3dhEbRFaBL5nNJUzbLfIF1jocTP2AsOgt-VXyVhRenElRz-Xu16k46HTbAkbl6504gsMJ5EYcRI9k7Gf1i7BVqahx21l7Qgs74wgVs-kVNt7_V5SnTfOZIyf5gDmFIw' -d '{"jsonrpc":"2.0","method":"<API_METHOD>","params":[],"id":1}' <JSON-RPC-http-hostname:port>

curl -X POST -H 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwZXJtaXNzaW9ucyI6WyIqOioiXSwicHJpdmFjeVB1YmxpY0tleSI6IlJPakxwOXNhc253cStDL290WVp4cmdOUHFnK2xGcFNvbmw1NkFPb2JqVE09IiwiZXhwIjoxNjAwODk5OTk5MDAyfQ.KICEhdYbhCjQKZGV_s7g_e8cAyfekUn5_f57EgLyY4O4wxs-VJFgG2Bh5zzhxXHpOwYEOMQmv6hxxBvowG4keT7BH39xx_j_76aGZd7Lz0wogM1qug6fciObWk30Y4u7w8vMJfheI8uWGX0bgAJsCxoy9JKo0t0p_jCVCOcBUISFAVcHRkpARpHlPDrmShqhJTJ66Lo-cYqhq_vDtCTS-dC3dhEbRFaBL5nNJUzbLfIF1jocTP2AsOgt-VXyVhRenElRz-Xu16k46HTbAkbl6504gsMJ5EYcRI9k7Gf1i7BVqahx21l7Qgs74wgVs-kVNt7_V5SnTfOZIyf5gDmFIw' -d '{"jsonrpc":"2.0","method":"<API_METHOD>","params":[],"id":1}' <JSON-RPC-http-hostname:port>
-bash: syntax error near unexpected token `newline'

curl -X POST -H 'Authorization: Bearer curl -X POST -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJwZXJtaXNzaW9ucyI6WyIqOioiXSwicHJpdmFjeVB1YmxpY0tleSI6IlJPakxwOXNhc253cStDL290WVp4cmdOUHFnK2xGcFNvbmw1NkFPb2JqVE09IiwiZXhwIjoxNjAwODk5OTk5MDAyfQ.J8n8iObjb9RQaFdfUTDAljn9iY3JfbAqNjtaTzym79g' -d '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":1}' http://localhost:8545' -d '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":1}' http://localhost:8545


curl -X POST -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJwZXJtaXNzaW9ucyI6WyIqOioiXSwicHJpdmFjeVB1YmxpY0tleSI6IlJPakxwOXNhc253cStDL290WVp4cmdOUHFnK2xGcFNvbmw1NkFPb2JqVE09IiwiZXhwIjoxNjAwODk5OTk5MDAyfQ.J8n8iObjb9RQaFdfUTDAljn9iY3JfbAqNjtaTzym79g' -d '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":1}' http://localhost:8545

curl -X POST -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJwZXJtaXNzaW9ucyI6WyIqOioiXSwicHJpdmFjeVB1YmxpY0tleSI6Im1TZXA5TmNSaStoWTN3V0ZXbk83OE1VRUQ0Y3Z0dGxnSEdjeENiNUV5RTg9IiwiZXhwIjoxNjAwODk5OTk5MDAyfQ.pRiKiUso86NgUMO-3KvV8f3RbZZmjvns4tYd7rl5Uls' -d '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":1}' http://localhost:8545


curl -X POST -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJwZXJtaXNzaW9ucyI6WyIqOioiXSwicHJpdmFjeVB1YmxpY0tleSI6IlJPakxwOXNhc253cStDL290WVp4cmdOUHFnK2xGcFNvbmw1NkFPb2JqVE09IiwiZXhwIjoxNjY5NDcwMjAyMDAwfQ.hy0jrZgvMMxZe_AYU_jc49ch9XgmxfPyL-T-5V5KEcQ' -d '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":1}' http://localhost:8545