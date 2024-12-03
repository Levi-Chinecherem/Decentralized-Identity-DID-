
### **Overview**  
This document provides a detailed explanation of the smart contracts used in the system, their responsibilities, key functions, and relationships. These contracts collectively manage decentralized identifiers (DIDs), Soulbound Tokens (SBTs), anonymous voting, and metadata for messaging.

---

### **Contracts Structure**

#### **1. DID Contract**  
**Purpose:**  
This contract handles the creation, management, and retrieval of Decentralized Identifiers (DIDs) and their associated metadata.  

**Key Features:**  
- **Decentralized Identifier (DID):** A unique string tied to each user, enabling decentralized identity representation.  
- **Metadata Storage:** Stores links to user data on decentralized storage systems like IPFS.  
- **Security:** Allows users to control and update their data.  

**Key Functions:**  
- `createDID(address user, string metadataURI)`  
  Creates a new DID for the user and links it to the metadata stored in decentralized storage.  
- `updateDID(address user, string newMetadataURI)`  
  Updates the user's DID metadata.  
- `getDID(address user)`  
  Retrieves the DID metadata associated with the user.

---

#### **2. Soulbound Token (SBT) Contract**  
**Purpose:**  
This contract manages non-transferable tokens (SBTs) issued as credentials, badges, or reputation scores for DAO members.  

**Key Features:**  
- Non-transferability ensures tokens represent unique achievements or credentials tied to individuals.  
- Supports issuing and revocation of SBTs.  

**Key Functions:**  
- `mintSBT(address user, uint256 tokenId, string metadataURI)`  
  Issues a Soulbound Token to the user with associated metadata.  
- `revokeSBT(address user, uint256 tokenId)`  
  Revokes an SBT from the user.  
- `getSBTs(address user)`  
  Retrieves all SBTs issued to the user.

---

#### **3. Voting Contract**  
**Purpose:**  
This contract facilitates DAO proposals and voting while ensuring privacy using zk-SNARKs.  

**Key Features:**  
- **Proposal Submission:** Members can submit proposals for DAO activities.  
- **Private Voting:** zk-SNARKs allow members to vote anonymously while ensuring votes are valid.  
- **Result Tallying:** Maintains vote counts and displays results securely.  

**Key Functions:**  
- `createProposal(string proposalDetails, uint256 deadline)`  
  Allows members to submit new proposals with a voting deadline.  
- `submitVote(uint256 proposalId, bytes zkProof)`  
  Accepts zk-SNARK proofs for vote submissions.  
- `tallyVotes(uint256 proposalId)`  
  Calculates and stores the results of a proposal.

---

#### **4. Messaging Metadata Contract**  
**Purpose:**  
This contract logs metadata for messages exchanged via the decentralized messaging system.  

**Key Features:**  
- Stores metadata such as sender, recipient, timestamp, and message hash.  
- Ensures on-chain transparency while preserving the privacy of actual message content.  

**Key Functions:**  
- `storeMetadata(address sender, address recipient, string messageHash, uint256 timestamp)`  
  Logs metadata for a sent message.  
- `getMetadata(uint256 messageId)`  
  Retrieves metadata for a specific message.

---

### **DiGraph Representation**

Below is the Graphviz **DiGraph** code illustrating the relationship between the contracts:  

```plaintext
digraph ContractsStructure {
    rankdir=LR;
    node [shape=box, fontname="Arial"];

    DIDContract [label="DID Contract"];
    SBTContract [label="Soulbound Token\n(SBT) Contract"];
    VotingContract [label="Voting Contract"];
    MessagingContract [label="Messaging Metadata\nContract"];

    User [label="User Wallet\n(DAO Member)", shape=ellipse];
    Frontend [label="Frontend Interface", shape=box, style=dotted];

    User -> Frontend [label="Interact"];
    Frontend -> DIDContract [label="Manage DID"];
    Frontend -> SBTContract [label="Earn/Revoke SBTs"];
    Frontend -> VotingContract [label="Submit Votes"];
    Frontend -> MessagingContract [label="Store Message Metadata"];

    DIDContract -> User [label="DID Linked"];
    SBTContract -> User [label="SBT Issued"];
    VotingContract -> Blockchain [label="Store Proposal & Votes"];
    MessagingContract -> Blockchain [label="Log Metadata"];
}
```
