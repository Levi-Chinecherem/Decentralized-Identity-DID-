### **Overview**  
This document explains the decentralized messaging system within the Decentralized Identity and Reputation System for DAOs. It enables DAO members to communicate securely and anonymously using wallet-to-wallet messaging powered by decentralized protocols.  

---

### **Key Features**

1. **End-to-End Encryption**:  
   - Ensures messages are encrypted on the sender's side and decrypted only by the recipient.  
   - Public/private key cryptography is used, leveraging Ethereum wallet keys.  

2. **Decentralized Storage**:  
   - Message metadata is stored on-chain for auditability.  
   - Message content is stored off-chain in a decentralized manner (e.g., IPFS).  

3. **Wallet-to-Wallet Messaging**:  
   - Messages are sent directly between wallet addresses.  

4. **Message Metadata**:  
   - Includes sender address, recipient address, timestamp, and message hash.  

---

### **Workflow for Messaging**

#### **1. Sending a Message**  
- The sender encrypts the message using the recipient’s public key.  
- The encrypted message is uploaded to IPFS, returning a content hash.  
- Metadata, including the content hash, is stored on-chain.  

#### **2. Receiving a Message**  
- The recipient queries the blockchain for messages addressed to their wallet.  
- The content hash is retrieved and used to fetch the encrypted message from IPFS.  
- The recipient decrypts the message using their private key.  

#### **3. Message Deletion**  
- Messages cannot be deleted from the blockchain, ensuring immutability.  
- Off-chain content may include an expiration feature to remove the data after a specified duration.

---

### **Messaging Data Flow**

1. **Sender Side**:  
   - Encrypt message → Upload to IPFS → Store metadata on-chain.  

2. **Recipient Side**:  
   - Query metadata → Fetch encrypted message → Decrypt using private key.  

---

### **Smart Contract Functions**  

#### **Store Metadata**  
Metadata is recorded on the blockchain to ensure message auditability.  

- **Inputs:**  
  - Sender Address  
  - Recipient Address  
  - IPFS Content Hash  
  - Timestamp  

- **Outputs:**  
  - Message ID  

- **Example Function:**
  ```solidity
  function sendMessage(address recipient, string memory ipfsHash) public {
      require(msg.sender != recipient, "Cannot send message to self");
      emit MessageStored(msg.sender, recipient, ipfsHash, block.timestamp);
  }
  ```

#### **Query Messages**  
Fetch metadata for messages sent to a specific wallet.  

- **Example Function:**
  ```solidity
  function getMessages(address recipient) public view returns (Message[] memory) {
      return messages[recipient];
  }
  ```

---

### **Libraries and Tools**  

1. **Encryption**:  
   - Use `eth-crypto` for keypair-based encryption and decryption.  

2. **Storage**:  
   - **IPFS**: Store encrypted message content.  
   - **Blockchain**: Store message metadata.  

3. **Frontend**:  
   - React components for sending and displaying messages.  

---

### **DiGraph Representation**

Below is the Graphviz **DiGraph** code illustrating the messaging system's flow:  

```plaintext
digraph MessagingSystem {
    node [shape=box, fontname="Arial"];
    rankdir=TB;
    ranksep=0.5; // Adjust for spacing between layers
    nodesep=0.5; // Adjust for spacing between nodes

    // Define nodes with ellipses and labels
    Sender [label="Sender Wallet", shape=ellipse];
    Recipient [label="Recipient Wallet", shape=ellipse];
    Encrypt [label="Encrypt Message"];
    IPFS [label="Store Encrypted Message\n(IPFS)"];
    Blockchain [label="Store Metadata\n(Blockchain)"];
    Decrypt [label="Decrypt Message"];
    FetchMessage [label="Retrieve Encrypted Message"];
    QueryMetadata [label="Query Message Metadata"];

    // Create circular flow by connecting nodes in sequence
    Sender -> Encrypt [label="Encrypt using Recipient's Public Key"];
    Encrypt -> IPFS [label="Upload Encrypted Message"];
    IPFS -> Blockchain [label="Save Metadata"];
    Blockchain -> Recipient [label="Notify Recipient"];
    Recipient -> QueryMetadata [label="Query Metadata"];
    QueryMetadata -> FetchMessage [label="Fetch Encrypted Content"];
    FetchMessage -> Decrypt [label="Decrypt using Private Key"];
    Decrypt -> Sender [label="Communication Complete"]; // Completes the circular flow
}
```

---

### **Advantages of the Messaging System**

1. **Privacy**:  
   - Messages are encrypted and visible only to the intended recipient.  

2. **Decentralization**:  
   - The system does not rely on centralized servers for storage or delivery.  

3. **Transparency**:  
   - Metadata stored on-chain ensures accountability and traceability.  

4. **Security**:  
   - Blockchain immutability prevents tampering with metadata.  
