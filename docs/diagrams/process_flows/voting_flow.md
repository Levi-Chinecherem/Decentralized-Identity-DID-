digraph VotingFlow {
    rankdir=LR;
    node [shape=box, fontname="Arial"];

    User [label="User (DAO Member)", shape=ellipse];
    Frontend [label="Voting Interface"];
    VotingContract [label="Voting Contract"];
    zkSnark [label="zk-SNARK Proof Generation"];
    Verifier [label="zk-SNARK Verifier"];
    Results [label="Proposal Results"];
    Blockchain [label="Blockchain\n(Ethereum)"];

    User -> Frontend [label="Select Proposal & Submit Vote"];
    Frontend -> zkSnark [label="Generate Proof"];
    zkSnark -> Frontend [label="Return Proof"];
    Frontend -> VotingContract [label="Submit Proof"];
    VotingContract -> Verifier [label="Verify Proof"];
    Verifier -> VotingContract [label="Valid/Invalid"];
    VotingContract -> Blockchain [label="Update Vote Count"];
    VotingContract -> Results [label="Update Tally"];
    Results -> Frontend [label="Display Results"];
}
