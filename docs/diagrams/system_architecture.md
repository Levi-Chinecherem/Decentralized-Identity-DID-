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
        "Image Capture" -> "Liveness Detection API" [label="Real-time Analysis"];
        "Liveness Detection API" -> "Access Granted" [label="Human Verification"];
    }

    "Frontend" -> "Smart Contracts" [label="Transaction Calls"];
    "Frontend" -> "zk-SNARKs" [label="Proof Submission"];
    "Frontend" -> "Messaging Protocol" [label="User Interaction"];
    "Frontend" -> "Facial Verification" [label="User Onboarding"];
    "Smart Contracts" -> "Storage" [label="On-chain Data"];
    "Facial Verification" -> "Storage" [label="Temporary Data"];
    "Messaging Protocol" -> "Storage" [label="Message Logs"];
}
