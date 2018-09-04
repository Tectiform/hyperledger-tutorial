# hyperledger-tutorial
Simple hyper ledger chaincode development tutorial

1. Install prerequisites as described here https://hyperledger-fabric.readthedocs.io/en/latest/prereqs.html
2. Install samples (and other stuff) as described here https://hyperledger-fabric.readthedocs.io/en/release-1.2/install.html
3. Clone this sample to fabric-samples/chaincode (Keep it simple). You should endup with folder spare in chaincode folder.
4. Open terminal and cd to spare folder in chaincode folder.
5. Install Hyperledger Fabric Client SDK for Go as described here https://github.com/hyperledger/fabric-sdk-go
6. go get github.com/hyperledger/fabric/core/chaincode/shim
7. go get github.com/hyperledger/fabric/protos/peer
8. go build (all should be fine)
9. Opet 3 terminals (yup, 3) and cd to fabric-samples/chaincode-docker-devmode
10. in Terminal 1 run  docker-compose -f docker-compose-simple.yaml up. Matrix style information will be written to console output. Dont panic!
11. in Terminal 2 run docker exec -it chaincode bash
12. in Terminal 2 cd to spare
13. in Terminal 2 go build
14. in Terminal 2 run CORE_PEER_ADDRESS=peer:7052 CORE_CHAINCODE_ID_NAME=mycc:0 ./spare (See this CORE_CHAINCODE_ID_NAME? It's name of your chain code). Last Console output log message will be starting up ... Dont panic!
15. In Terminal 3 run docker exec -it cli bash
16. In Terminal 3 run peer chaincode install -p chaincodedev/chaincode/spare -n mycc -v 0 (See -n mycc? That's name of your chaincode and must be same as in step 14)
17. In Terminal 3 run peer chaincode instantiate -n mycc -v 0 -c '{"Args":[]}' -C myc
18. You are all set! Let's run some transactions. In Terminal 3 run peer chaincode invoke -n mycc -c '{"Args":["addPartRecord", "P1", "Brake","123","No comment is a comment"]}' -C myc (P1 will be written at the end of the Console output log)
19. In Terminal 3 run peer chaincode invoke -n mycc -c '{"Args":["getPartRecord", "P1"]}' -C myc (Previously entered data in JSON form will be written to the Console output.)
20. In Terminal 3 type exit and press enter
21. In Terminal 2 press ctrl+c and exit
22. In Terminal 1 press ctrl+c and when back to command prompt run docker-compose -f docker-compose-simple.yaml down 
