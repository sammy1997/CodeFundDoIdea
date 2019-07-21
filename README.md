# CodeFundDoIdea

## Theme:
Elections, referenda, and polls are very important processes & tools for the smooth operation of a modern democracy.
Build a Proof-of-Concept to demonstrate how you can make these processes more secure, reliable, and transparent using  Blockchain.

## Election Issues:

![Election Issues](https://s3.amazonaws.com/cbi-research-portal-uploads/2018/10/30153611/blockchain-election-security-vulnerabilities-feature-image-10.30.2018.png)

<br>

The above image (Source: CBINSIGHTS) shows what are the possible vulnurablilities before, during and after an election process. To list a few issues:

* __Fake news & information warfare__
* __Illegal voter registrations and removals from database__
* __Hacked voting hardware__
* __Compromised election reporting systems__
* __Problems in post-election vote counting and audit(they are often inaccurate and take quite a long time)__

For our idea submission, we aim to make an easy to use mobile application which will help users vote and we will use blockchain and crypto for ensuring genuine digital information and securing the polling process and data. We aim to solve most of the above problems either partly or wholly via the proposed system.

## The Solution:

We will explain how we want to tackle each issue. But first we want to make a few assumptions and explain the Election Commisions role. All the members of election commision will get a private-public key pair using which they can sign off on digital information. While explaining the working in the following points, if we come across the mention of a consortium, it is meant as a consortium of designated EC members. For voting, the Voting Officers consortium will have both EC memebers as well as teachers, govt officers etc who have been alloted election duties. Also, to maintain information, we will use 2 different chains - a vote chain and a registration chain. Also, we are assuming Indian elections, so we will use Aadhar, PAN cards as valid IDs.

We will first explain some data structures that will define the type of data objects that will be stored in the ledger.

1. `Proposal {
      address ID;
      int voteCount;     
    }
    `
2. `Voter {         boolean isVoted;         boolean hasRightToVote;         int vote;         address ID;     }`

Proposals[] is an array of Proposal objects.



* __Reducing fake news and information__ : The app will have a public election news board/page. This board will have all the news related to election. The users will be notified to trust only information published on the board as valid. Any news channel or site can sign up as a node and request to publish an article on the board. To get an article published, the news needs to be proposed to all the nodes of the EC consortium. Then, the EC members verifies the source of the news and any one of them signs it with his/her key. The rest of the consortium then votes to decide if the news gets published. Once the article gets a majority, it gets pushed to the board's database and gets displayed. The advantage? All news reaching voters is verified. Also, as the entire consortium is voting, it is not possible to corrupt a single member to publish fake news.

* __Illegal voter registrations and removals from database__ : All voters can register directly on the app. To register, they will have to upload a government ID, face data and if possible fingerprint data as well(for phones with fingerprint sensors). A consortium member verfies the data and proposes the voter to be registered. If the consortium allows, a unique digital voter address and a voter object is generated and added to the registration blockchain. This address is saved in the voters app as well, and this address(like Etherium wallet address) becomes the voter's identity in the system. A single block can have multiple such identified voters(just like transactions). As the ledger is immutable, it can't be deleted or morphed. Any address can be validated by simply checking the longest chain in registration blockchain. So an initial voter object might look like - 
`
Voter x = {
    isVoted: false;
    hasRightToVote: true;
    vote: -1;
    ID: 0xF40877673bbea2C068c6721A2E43DF5AE8771C23;
}
`

* __Hacked voting hardware__: We often hear about hacked EVMs, where people complain that votes cast to one party are often counted in other's vote count. Using our system, any citizen can vote from their mobile phone once they are registered. For the voting process, the EC publishes a list of all proposals(people who are contesting in the election). Each valid user(one who has a generated digital ID after verification) can cast a vote by selecting one element out of the proposal list.The voting consortium decides whether to add it into a block once a miner validates multiple votes and proposes it. Once it has been cast, his isVoted becomes true and hasRightToVote becomes false. Also, his vote field stores the index in Proposals array that he/she selected while voting. As soon as the vote gets added to the main chain, the proposal's vote count is increased and the voter is notified that his vote was counted.


* __Compromised result reporting and vote counting__: After elections, the vote count process involves manual checking of ballots and EVMs. This takes time and is inaccurate often. In our system, all the voting counts are maintained across proposal objects. Once the election is closed by the EC, the results can be instantly generated by comparing counts of all the proposals. This information is then published on the news board as the official result and all the users are notified.



