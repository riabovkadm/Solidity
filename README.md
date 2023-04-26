pragma solidity ^0.8.0;

contract Voting {
    mapping (address => bool) public hasVoted;
    mapping (uint256 => uint256) public votes;

    function vote(uint256 candidateId) public {
        require(!hasVoted[msg.sender], "You have already voted.");
        votes[candidateId]++;
        hasVoted[msg.sender] = true;
    }

    function getWinner() public view returns (uint256) {
        uint256 maxVotes = 0;
        uint256 winnerId = 0;
        for (uint256 i = 0; i < candidates.length; i++) {
            if (votes[i] > maxVotes) {
                maxVotes = votes[i];
                winnerId = i;
            }
        }
        return winnerId;
    }
}
