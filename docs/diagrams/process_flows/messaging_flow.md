digraph MessagingFlow {
    rankdir=LR;
    node [shape=box, fontname="Arial"];

    Wallet1 [label="User Wallet 1", shape=ellipse];
    Wallet2 [label="User Wallet 2", shape=ellipse];
    MessagingApp [label="Messaging Interface"];
    MessagingServer [label="Decentralized Messaging Server"];
    Blockchain [label="Blockchain\n(for Metadata)"];

    Wallet1 -> MessagingApp [label="Compose & Send Message"];
    MessagingApp -> MessagingServer [label="Encrypt & Relay"];
    MessagingServer -> Blockchain [label="Log Message Metadata"];
    MessagingServer -> Wallet2 [label="Deliver Message"];
    Wallet2 -> MessagingApp [label="Read Message"];
}
