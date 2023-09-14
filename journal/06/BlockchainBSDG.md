# Jim McKeeth on Smart Contracts

Cryptography to blockchain, slides will be available

Crypto as filling the gap between commodity and peer-to-peer w/o being under fiat banking (vs cash or gold)

Publics keys are combo/product of two very large prime numbers

Quantum encryption is trying to get around this

remainder is cypher text of the primes after divisions
Blockchain does not use encryption, just signatures
collisions are possible, but rare (two different hashes that produce same output)
message = hash, signature is a hash encrypted w/ private key, other can use public key to validate
256bits is 1.158*10^77

hot (online holding of private key - which holds all transactions) vs cold (offline ) wallet
wallets do not hold bitcoin, but your private wallet that can conduct/verfiy transactions
    the people with money do not use hot wallets, haha <-- which is definitely fair enough

exchanges function to do transactions - theft tends to happen here - with wallet keys being compromised so as to steal $

hot wallet metamask.io is higher on the safety ranking, def better than exchanges

Ethereum is key to smart contracts
    programs running on ethereum virtual machine
        computer run on blockchain

Blockchains are compromised when over half the nodes (transactions) are run by one user
    if you can hash the next block (gen the longest chain) fastest, you "win"
        literal chain in the sense that previous hash block is part of next block - latest block hash ==validation of whole chain
consensus is based on longest chain
there is illegal material in the blocks - technically owning a node could get you a Federal knock for illegal possession
    the real reason illicit photographic content will never be made illegal

cost of transactions is how much power is used, how much is held det value
costly transactions to maintain smart contract, so you get bounced once you can no longer afford to maintain the contract
you cannot put a bunch of crap if you cannot afford it - buying islands is better use of funds
speed of light req all the energy in the universe, hence cannot go faster


hash algorithms are quick, if you go back far enough, you know it is valid, as rows prior are the foundation to the following
you can force recalc,
    mining/proof of work is to prevent this
        do I have enough preceding binary 0s to validate this   <-- proves you did the work
            more 0s is more difficult
                demo - 10 zeroes took 205 tries
                    more people = more zeroes added for req (more people really is more machines)

    Proff of stake - 32 ether, volunteer stake by random selection of pool - lower energy, higher speed, larger stake
    stake token = having tokens to stake
        invalid block is loss of stake
            valid is get your stake back and a percentage of the transaction fee
proof of work is democratic, proof of stake is oligarchic - need to have the money to pony up, can centralize

vice-oriented legislation is hard on society, but virtue-oriented also lends to vice when the cost of virtue is intrinsically higher than that of vice, and the goal of a piece of legislation is to lower the amount of effort to live in a society
    this is why revolt happens under the conditions of growing freedoms and privileges, not constriction
        people bunker under constriction
            organizational power at this time is critical, and there is more to gain from power to disrupt lower levels than incorporate them
        virtue-oriented would bill a government, which it will not fo, even when being on the backs of the populace
    modern revolt for freedom will necessitate an entity that can produce parallel centralized power
the value of the scale/stack of society is as the first and last defence against the existing legislators

trust is default in infrastructure - it fails when the infrastructure fails
    identifying your actual infrastructure is essential to understanding the foundation of your trust
        point of blockchain is the enter a trustless society
            works well in medical contracting, not last mile usage in direct pt care, but in admin
        trustless societies are minimally comprehensible to high-trust societies
    trustless societies are fundamentally unable to comprehend high-trust societies
high trust lowers personal cost of existence absent high regulation

existing in mid-level trust means people misunderstand both tail ranges as false in their very existence
    mid-level trust is prime for arbitrage, as it is a preying on high trust-low security
        the potential for wealth and advancement primes for lowering trust for those who exist on the tail-ends and can afford it
            when the pay-off tapers, people will cash out --> en masse this is people who cannot be bothered to generate new avenues of growth
        the resulting scramble craters trust even more for some and consolidates it in bubbles - re-tribalism
    People now have to literally pay to enter high trusst societies, and as money lessens in certain values, signaling come in
class segregation happens by who can trust whom, which is signalled by trust proxies

communities can bypass this how?

    churches have the benefit of existing as a format of de facto decentralized/centralized tribes, i.e. denominations
        sequencing trust is why orthodoxy interpretations generate so much heat
            aligning with "outsiders" means that there is social arbitrage occuring
                social arbitrage has environmental consequences - loss of space and areas of access even in 3rd party locations
            aligning insiders becomes stringent and learning curve rises
        trust...has to operate as trust to revert this
    physical presence in other areas can mitigate the initial devolution and instigate reconstruction, or else taking oaths as valid *can*

centralized goal decentralized efforts are hard to coordinate, though easy to scale
    must use tangentials - saving parallel to immediate things like food and healing
        encompassing trust as the mechanism for the sustainable arches
            even bad original planning can be buttressed by primary goal of raising a roof
        attention to detail in visual appeal need not be *positive* so much as *strange*
    tangentials create the patterns upon which a people is built from persons
planting and succession become options, but vertical leaps are limited - possibly grow more so
    vision of "management" comes into play
        hired-hands and mercenaries do not treat community like it is theirs
            communities feel the positive effects of efficiency before negative ones as higher levels of base knowledge replace interecoonected specilaization
        communities increasingly need to outsource from more intact or successfully stacked peers/competitors
    laterals made by unqualified, and true glass ceiling evolves with neck arranging visual field
        eyes still can manipulate visual field
            head can withstand more hits than neck
        with proper incentive, will resolve by eying better goals
    power is intrinsically conservative and centralized - wants to maintain and grow itself
ability for qualified to tap into centralized w/o being it generates scale



smart programs are programs w/in the blockchain
    microservice that runs TRUSTLESS on the backend of your application
        not run distributively, but validated across multiple systems when public, and cannot be modified or removed
            autonomous ways - no centralized 3rd party
                if I do X, I get Y, no bank
mathematically provable, not in lawyer speak, but coder - bypasses existing knowledge base
    translated by programmer, not lawyer
        transfers power base away from existing one
        no terms subject to change, confidentiality, etc
        cost of contract is to put on
        cost to run is not borne by you, but the person who runs it
            again, maintained by money - can you afford to uphold the contract
                viewing is free, changing it is the cost
remix.ethereum.org
    can link code from Github
            make a smart contract
    pay per run/compile is expensive
        testnets to avoid high costs
            have "facucets" ethereum given to run on their sandbox, when you are happy with the result, you pay for real ether to put it on blockchain
                ie - you spin it locally so you don't flub it publicly at cost
