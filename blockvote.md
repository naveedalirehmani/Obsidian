
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Election {
    struct Candidate {
        uint id;
        string name;
        string party;
        string symbol;
        uint voteCount;
    }

    struct Voter {
        bool authorized;
        bool voted;
        uint vote; // Candidate ID
    }

    address public owner;
    string public electionName;
    bool public electionStarted;

    mapping(address => Voter) public voters;
    Candidate[] public candidates;

    uint public totalVotes;

    event ElectionStarted();
    event ElectionEnded();
    event VoteCast(address indexed voter, uint candidateId);

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this function.");
        _;
    }

    modifier electionOngoing() {
        require(electionStarted, "Election is not ongoing.");
        _;
    }

    modifier electionNotStarted() {
        require(!electionStarted, "Election already started.");
        _;
    }

    constructor(string memory _name) {
        owner = msg.sender;
        electionName = _name;
    }

    // Add candidate with general information
    function addCandidate(string memory _name, string memory _party, string memory _symbol) public onlyOwner electionNotStarted {
        candidates.push(Candidate({
            id: candidates.length,
            name: _name,
            party: _party,
            symbol: _symbol,
            voteCount: 0
        }));
    }

    // Authorize voter by owner before election starts
    function authorizeVoter(address _voter) public onlyOwner electionNotStarted {
        require(!voters[_voter].authorized, "Voter is already authorized.");
        voters[_voter].authorized = true;
    }

    // Start the election (owner only)
    function startElection() public onlyOwner electionNotStarted {
        electionStarted = true;
        emit ElectionStarted();
    }

    // Stop the election (owner only)
    function endElection() public onlyOwner electionOngoing {
        electionStarted = false;
        emit ElectionEnded();
    }

    // Cast vote to a candidate
    function vote(uint _candidateId) public electionOngoing {
        Voter storage sender = voters[msg.sender];
        require(sender.authorized, "You are not authorized to vote.");
        require(!sender.voted, "You have already voted.");
        require(_candidateId < candidates.length, "Invalid candidate ID.");

        sender.voted = true;
        sender.vote = _candidateId;
        candidates[_candidateId].voteCount++;
        totalVotes++;

        emit VoteCast(msg.sender, _candidateId);
    }

    // Get total number of candidates
    function getNumCandidates() public view returns (uint) {
        return candidates.length;
    }

    // Get details of a specific candidate
    function getCandidate(uint _candidateId) public view returns (string memory, string memory, string memory, uint) {
        require(_candidateId < candidates.length, "Invalid candidate ID.");
        Candidate memory candidate = candidates[_candidateId];
        return (candidate.name, candidate.party, candidate.symbol, candidate.voteCount);
    }

    // Get list of candidates with vote count
    function getAllCandidates() public view returns (Candidate[] memory) {
        return candidates;
    }

    // Get vote status of a voter
    function getVoterVote(address _voter) public view returns (bool, uint) {
        require(voters[_voter].authorized, "Voter is not authorized.");
        return (voters[_voter].voted, voters[_voter].vote);
    }
}

```