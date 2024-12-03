digraph DIDRegistrationFlow {
    rankdir=TB;
    node [shape=box, fontname="Arial"];

    User [label="User (Wallet)", shape=ellipse];
    Frontend [label="Frontend Interface"];
    DIDContract [label="DID Contract"];
    Storage [label="Decentralized Storage\n(IPFS/Filecoin)"];
    Blockchain [label="Blockchain\n(Ethereum Mainnet/Testnet)"];

    User -> Frontend [label="Enter Details & Connect Wallet"];
    Frontend -> DIDContract [label="Transaction: Create DID"];
    DIDContract -> Blockchain [label="Store DID Metadata"];
    DIDContract -> Storage [label="Store Encrypted Data (e.g., Credentials)"];
    Frontend -> User [label="DID Generated\nSuccess Message"];
}
