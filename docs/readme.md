### Documentation Structure for the System  

#### **Folder Structure**
```plaintext
├── docs/                   # Documentation files
│   ├── diagrams/           # Architecture and flow diagrams
│   │   ├── system_architecture.png   # High-level system architecture diagram
│   │   ├── process_flows/            # Folder for detailed flow diagrams
│   │   │   ├── DID_registration_flow.png
│   │   │   ├── voting_flow.png
│   │   │   └── messaging_flow.png
│   └── technical/          # Technical documentation
│       ├── contracts.md    # Details of smart contracts
│       ├── zk_snarks.md    # Documentation on zk-SNARK implementation
│       ├── frontend.md     # Frontend structure and interaction
│       ├── messaging.md    # Decentralized messaging protocol details
│       ├── facial_verification.md   # Explanation of facial verification system
│       └── deployment.md   # Deployment and testing steps
```

---

### **Diagrams Overview**
Below are the diagrams to create and include in the **docs/diagrams** directory:  
1. **System Architecture Diagram:**  
   High-level architecture showing the interaction between the components (frontend, contracts, zk-SNARKs, messaging protocol, facial verification, and storage).

2. **DID Registration Flow:**  
   Steps detailing how users register, verify, and update their DID.

3. **Voting Flow:**  
   Flowchart illustrating the process of proposal creation, zk-SNARK proof submission, and result tallying.

4. **Messaging Flow:**  
   Diagram demonstrating how wallet-to-wallet communication operates within the system.

5. **Facial Verification Flow:**  
   Flowchart showing the process of image submission, verification, and linking to the DID.

---

### **DiGraph Code**
Below is the **Graphviz DiGraph** code demonstrating the system architecture:  

```plaintext
digraph SystemArchitecture {
    rankdir=LR;
    node [shape=box, fontname="Arial"];

    subgraph cluster_frontend {
        label = "Frontend";
        style = filled;
        color = lightgrey;
        "UI Components" -> "Blockchain Interaction" [label="Ethers.js"];
        "UI Components" -> "Facial Verification" [label="API Calls"];
    }

    subgraph cluster_smart_contracts {
        label = "Smart Contracts";
        style = filled;
        color = lightblue;
        "DID Contract" -> "SBT Contract" [label="Credential Updates"];
        "SBT Contract" -> "Voting Contract" [label="Reputation Weight"];
    }

    subgraph cluster_zk_snarks {
        label = "zk-SNARKs";
        style = filled;
        color = lightgreen;
        "Proof Generation" -> "Proof Verification" [label="Voting Privacy"];
    }

    subgraph cluster_messaging {
        label = "Messaging Protocol";
        style = filled;
        color = yellow;
        "Wallet 1" -> "Messaging Server" [label="Encrypted Messages"];
        "Messaging Server" -> "Wallet 2" [label="Notification"];
    }

    subgraph cluster_facial_verification {
        label = "Facial Verification";
        style = filled;
        color = orange;
        "Image Submission" -> "Verification API" [label="Facial Analysis"];
        "Verification API" -> "DID Contract" [label="Link Identity"];
    }

    "Frontend" -> "Smart Contracts" [label="Transaction Calls"];
    "Frontend" -> "zk-SNARKs" [label="Proof Submission"];
    "Frontend" -> "Messaging Protocol" [label="User Interaction"];
    "Frontend" -> "Facial Verification" [label="User Onboarding"];
    "Smart Contracts" -> "Storage" [label="On-chain Data"];
    "Facial Verification" -> "Storage" [label="Encrypted Data"];
    "Messaging Protocol" -> "Storage" [label="Message Logs"];
}
```
