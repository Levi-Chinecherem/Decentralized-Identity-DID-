
### **Overview**  
This document outlines the structure, components, and interactions of the frontend for the Decentralized Identity and Reputation System. The frontend serves as the user interface, enabling DAO members to interact with smart contracts, zk-SNARK systems, and decentralized storage.

---

### **Frontend Structure**

#### **1. Framework**  
- **Frontend Framework:** React.js with Tailwind CSS for styling.  
- **Libraries:**  
  - `ethers.js`: For blockchain interactions.  
  - `ipfs-http-client`: To manage decentralized storage.  
  - `circomlib`: For zk-SNARK proof handling.  
  - `react-router-dom`: For navigation between sections.  

---

#### **2. Folder Structure**

```plaintext
frontend/
├── public/                      # Public assets
│   └── index.html               # HTML entry point
├── src/                         # Source code
│   ├── components/              # Reusable components
│   │   ├── Navbar.jsx           # Navigation bar
│   │   ├── Footer.jsx           # Footer
│   │   ├── DID/                 # DID-related components
│   │   │   ├── CreateDID.jsx    # DID creation form
│   │   │   ├── UpdateDID.jsx    # DID update form
│   │   │   ├── ViewDID.jsx      # DID display
│   │   ├── Voting/              # Voting components
│   │   │   ├── ProposalList.jsx # List of proposals
│   │   │   ├── VoteForm.jsx     # Vote submission form
│   │   │   ├── Results.jsx      # Voting results
│   │   ├── Messaging/           # Messaging components
│   │   │   ├── MessageList.jsx  # List of messages
│   │   │   ├── SendMessage.jsx  # Form to send messages
│   │   ├── Authentication/      # Authentication-related components
│   │   │   ├── FacialVerification.jsx  # Facial verification UI
│   │   └── Shared/              # Shared utilities and helpers
│   │       ├── Blockchain.jsx   # Blockchain interaction helpers
│   │       ├── IPFSUploader.jsx # IPFS integration helpers
│   ├── pages/                   # Main pages
│   │   ├── Home.jsx             # Landing page
│   │   ├── Dashboard.jsx        # User dashboard
│   │   ├── AdminPanel.jsx       # Admin-specific panel
│   ├── styles/                  # Styling files
│   │   └── tailwind.css         # Tailwind CSS configuration
│   ├── App.jsx                  # Main React component
│   └── index.js                 # React entry point
├── package.json                 # Dependencies and scripts
└── tailwind.config.js           # Tailwind configuration
```

---

### **Key Features**

#### **1. DID Management**  
- **Create DID:**  
  - Allows users to register a new DID.  
  - Metadata is uploaded to IPFS and linked to the DID.  
- **Update DID:**  
  - Enables users to modify their DID metadata.  

#### **2. Voting Interface**  
- **Proposal Submission:**  
  - Admins and eligible members can submit new proposals.  
- **Anonymous Voting:**  
  - Users submit zk-SNARK proofs of their votes.  
  - The interface validates proof generation and submission.  
- **Results Display:**  
  - Real-time tallying of votes and secure presentation of results.  

#### **3. Messaging System**  
- **Send Message:**  
  - Users can send encrypted messages.  
  - Message metadata is stored on-chain.  
- **Message Inbox:**  
  - Displays received messages with metadata (e.g., sender, timestamp).  

#### **4. Facial Verification System**  
- Uses WebRTC to access the user's camera for facial recognition.  
- Interfaces with backend services to verify facial data against registered identities.

---

### **Interactions Between Components**

1. **Blockchain Integration:**  
   - `Blockchain.jsx` connects to smart contracts using `ethers.js`.  
   - Functions like `createDID`, `submitVote`, and `storeMetadata` are wrapped for easy frontend use.  

2. **Decentralized Storage Integration:**  
   - `IPFSUploader.jsx` handles file uploads to IPFS and returns content hashes.  
   - Used for DID metadata storage.  

3. **zk-SNARK Integration:**  
   - Provides interfaces for generating zk-SNARK proofs locally.  
   - Validates proofs before submission to the blockchain.  

---

### **DiGraph Representation**

Below is the Graphviz **DiGraph** code representing the frontend's architecture and its interactions:  

```plaintext
digraph FrontendArchitecture {
    rankdir=LR;
    node [shape=box, fontname="Arial"];

    DIDManagement [label="DID Management\n(Create/Update/View DID)"];
    VotingSystem [label="Voting System\n(Submit Votes/View Results)"];
    MessagingSystem [label="Messaging System\n(Send/Receive Messages)"];
    FacialVerification [label="Facial Verification"];
    Blockchain [label="Blockchain\n(Smart Contracts)"];
    IPFS [label="IPFS\n(Metadata Storage)"];
    zkSNARKs [label="zk-SNARK\nProof Validation"];

    User [label="User Wallet\n(DAO Member)", shape=ellipse];
    Frontend [label="Frontend Interface"];

    User -> Frontend [label="Interact"];
    Frontend -> DIDManagement [label="Manage DID"];
    Frontend -> VotingSystem [label="Vote"];
    Frontend -> MessagingSystem [label="Message"];
    Frontend -> FacialVerification [label="Authenticate"];
    DIDManagement -> Blockchain [label="DID Data"];
    VotingSystem -> zkSNARKs [label="Generate Proof"];
    zkSNARKs -> Blockchain [label="Validate Proof"];
    MessagingSystem -> Blockchain [label="Store Metadata"];
    DIDManagement -> IPFS [label="Upload Metadata"];
}
```
