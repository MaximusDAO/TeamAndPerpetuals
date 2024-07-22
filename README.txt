/*
 /$$      /$$                     /$$                                         /$$$$$$$$ /$$$$$$$$  /$$$$$$  /$$      /$$
| $$$    /$$$                    |__/                                        |__  $$__/| $$_____/ /$$__  $$| $$$    /$$$
| $$$$  /$$$$  /$$$$$$  /$$   /$$ /$$ /$$$$$$/$$$$  /$$   /$$  /$$$$$$$         | $$   | $$      | $$  \ $$| $$$$  /$$$$
| $$ $$/$$ $$ |____  $$|  $$ /$$/| $$| $$_  $$_  $$| $$  | $$ /$$_____/         | $$   | $$$$$   | $$$$$$$$| $$ $$/$$ $$
| $$  $$$| $$  /$$$$$$$ \  $$$$/ | $$| $$ \ $$ \ $$| $$  | $$|  $$$$$$          | $$   | $$__/   | $$__  $$| $$  $$$| $$
| $$\  $ | $$ /$$__  $$  >$$  $$ | $$| $$ | $$ | $$| $$  | $$ \____  $$         | $$   | $$      | $$  | $$| $$\  $ | $$
| $$ \/  | $$|  $$$$$$$ /$$/\  $$| $$| $$ | $$ | $$|  $$$$$$/ /$$$$$$$/         | $$   | $$$$$$$$| $$  | $$| $$ \/  | $$
|__/     |__/ \_______/|__/  \__/|__/|__/ |__/ |__/ \______/ |_______/          |__/   |________/|__/  |__/|__/     |__/
                                                                                                                        
                                                                                                                        
                                                                                                                        
                           /$$         /$$     /$$                                                                      
                          | $$        | $$    | $$                                                                      
  /$$$$$$  /$$$$$$$   /$$$$$$$       /$$$$$$  | $$$$$$$   /$$$$$$                                                       
 |____  $$| $$__  $$ /$$__  $$      |_  $$_/  | $$__  $$ /$$__  $$                                                      
  /$$$$$$$| $$  \ $$| $$  | $$        | $$    | $$  \ $$| $$$$$$$$                                                      
 /$$__  $$| $$  | $$| $$  | $$        | $$ /$$| $$  | $$| $$_____/                                                      
|  $$$$$$$| $$  | $$|  $$$$$$$        |  $$$$/| $$  | $$|  $$$$$$$                                                      
 \_______/|__/  |__/ \_______/         \___/  |__/  |__/ \_______/                                                      
                                                                                                                        
                                                                                                                        
                                                                                                                        
 /$$$$$$$                                           /$$                         /$$                                     
| $$__  $$                                         | $$                        | $$                                     
| $$  \ $$ /$$$$$$   /$$$$$$   /$$$$$$   /$$$$$$  /$$$$$$   /$$   /$$  /$$$$$$ | $$  /$$$$$$$                           
| $$$$$$$//$$__  $$ /$$__  $$ /$$__  $$ /$$__  $$|_  $$_/  | $$  | $$ |____  $$| $$ /$$_____/                           
| $$____/| $$$$$$$$| $$  \__/| $$  \ $$| $$$$$$$$  | $$    | $$  | $$  /$$$$$$$| $$|  $$$$$$                            
| $$     | $$_____/| $$      | $$  | $$| $$_____/  | $$ /$$| $$  | $$ /$$__  $$| $$ \____  $$                           
| $$     |  $$$$$$$| $$      | $$$$$$$/|  $$$$$$$  |  $$$$/|  $$$$$$/|  $$$$$$$| $$ /$$$$$$$/                           
|__/      \_______/|__/      | $$____/  \_______/   \___/   \______/  \_______/|__/|_______/                            
                             | $$                                                                                       
                             | $$                                                                                       
                             |__/                                                                                      


// Anyone may choose to mint 1 Perpetual Pool Token per HEX pledged to the Perpetual Pool Contract during the minting phase.
// Pool Tokens are a standard ERC20 token, only minted upon HEX deposit and burnt upon HEX redemption with no pre-mine.
// Pool Token holders may choose to burn their Pool Tokens to redeem HEX principal and yield pro-rata from the Pool Token Contract Address during the reload phase.
// The Perpetual Pools start with an initial minting phase, followed by a stake phase. Then once the HEX stake has ended they enter a reload phase where HEX may be redeemed with Pool Tokens or Pool Tokens may be minted with HEX - all at the same redemption rate.
// Then after the reload phase ends another Stake Phase begins and the cycle repeats forever.


// PHASES:        |----- Minting Phase ----|------ Stake Phase -----...-----|---- Reload Phase ----->|----- Stake Phase ------|----> REPEAT FOREVER
// WHAT HAPPENS?  |       Mint and redeem  |    No Minting or Redeeming     |   Mint and redeem      | No Minting or Redeeming|---->
// FUNCTIONS USED:| pledgeHEX(),redeemHEX()|      mintHedron()              | pledgeHEX(),redeemHEX()|      mintHedron().     |
// TRANSITION FUNCTION:       stakeStart() ^                  endStakeHex() ^           stakeStart() ^          endStakeHex() ^ 

// The Pool Contracts send half of it's Bigger Pays Better Bonus HEX Yield and all of the HDRN the stake accumulated to the Maximus TEAM Contract as a thank you for deploying the pools and an incentive to grow the stake pooling economy.


Maximus TEAM is a contract which distributes incomes received by the contract equally amongst TEAM stakers.

The primary income source to the TEAM contract are the Perpetual Pools - hex stake pools deployed by the TEAM contract that send half of their Bigger Pays Better Bonus HEX earnings plus the accrued HDRN to the Team Contract. If users successfully stake per the Staking Rules, they are eligible to claim their portion of the incomes.

The Maximus TEAM and Perpetual Pool contracts are fully trustless and have no admin keys. This means that users are responsible for the operation of the contract by running certain scheduled functions on behalf of the contract when the time comes.

Deployment and Contract Operation
Day 0: Initial TEAM Contract Deployment
Dip Catcher will run this function. Users should read through the contract themselves to ensure everything is as expected. During deployment the following actions are completed:
Activate the TEAM Minting Phase
Deploy Perpetual Pools
Deploy Stake Reward Distribution Contract
Day 21: Run finalizeMinting() function and run startStake() for each of the Perpetuals
Anyone can run these public functions. Whoever runs it clicks one button and the following are completed:
Disable new TEAM Minting
Burn 20% of the MAXI in the TEAM Contract
Deploy the 369 MAXI Escrow Contract and send it 30% of MAXI in TEAM Contract
Schedule the MAXI redistributions from the Escrow Contract in years 3, 6, and 9
Deploy Mystery Box Smart Contract and send it 50% of MAXI in TEAM Contract and the copy of the TEAM minted
Day 386 and then every time BASE stake ends: prepareClaims() function
Anyone can run prepareClaims() and one person needs to run it before stake rewards from a completed period are claimed. This does the following:
For each token in the Supported Tokens list, record the TEAM Contract’s balance of each coin
Calculate Redemption Rate for each coin. Think of redemption rate as “Number of Tokens claimable per TEAM staked that period”
Transfer the tokens from the TEAM contract to the Stake Reward Distribution Contract.
Every time a Perpetual Pool stake ends run mintHedron() and endStake()
TEAM Minting Rules
One-time only 21 day minting phase
Mint 1 TEAM per 1 MAXI pledged to the Team Contract
You should have no expectations of anything from this
Mint Phase ends when finalizeMinting() function is run.
20% of total MAXI minted into TEAM is Burnt
30% of the MAXI is Transfered to the 369 MAXI Escrow Contract which holds the MAXI until it is sent to the TEAM Contract across years 3, 6, and 9.
50% of the MAXI and a copy of every TEAM minted goes to the Mystery Box Contract.
TEAM Staking Rules
The BASE Contract is the Calendar for TEAM Staking. To earn TEAM staking rewards you must stake your team for an entire 1 year BASE Stake, called a Staking Period.
7 day period between base stakes (BASE Minting/Redemption Phase) is called the TEAM Commitment Phase
When you stake TEAM your TEAM is burnt, when you end stake TEAM it is reminted into your wallet. You do not have to end your entire stake at once, you can end in any increment.
Stake terms last one year at a time, you must check in with the contract by running extendStake() or restakeExpiredStake() at least once per year to keep your TEAM stake active during each consecutive staking year. This is to prevent lost keys or dead people from absorbing the TEAM staker income.
If you end stake TEAM before your stake expires, you experience a 3.69% penalty on the amount you early-end staked. This penalty is simply not minted back into existence. For example, if you stake 1,000,000 TEAM and then early end stake 100,000 team, you only get 96,310 TEAM and the remaining 3,690 TEAM is permanently burnt, forever decreasing the TEAM supply.
Staking
To stake liquid TEAM in your wallet, run stakeTeam(amount). This function:
Creates a stake record with a unique Stake ID for the next staking period, or adds to a stake record for the period if you have already staked into the next staking period.
Increments the Global and User Amount Staked Tallies
Increments the Global and User Active Stake per Period Tallies
Sets the expiry period on their Stake Record
burns the amount of TEAM staked
To end a stake before your stake expiry period is complete, run earlyEndStakeTeam(stakeID, amount)
Decrements Global and User Amount Staked Tallies
Decrements the Global and User Active Stake per Period Tallies
mints the amount of TEAM you requested minus the penalty
To end a stake that has already reached its stake expiry period, run endCompletedStake(stakeID, amount)
Decrements Global and User Amount Staked Tallies
Mints the amount of TEAM you requested
To roll forward an active TEAM stake into the next period, run extendStake(stakeID)
Increments the Global and User Active Stake per Period Tallies for the next period
updates your stake record’s stake expiry period to be the next period
Note: this moves your entire stake into the next period.
to roll forward an expired TEAM stake into the next period, run restakeExpiredStake(stakeID)
Closes out current stake by updating stake.unstakd_amount
Creates new stake record
Claiming Rewards
The contract calculates the claimable rewards per TEAM staked for each supported token.
Users prove to the Stake Reward Distribution Contract which periods they succesfully staked in and how much.
The Stake Reward Distribution contract transfers the claiming user the number of tokens they are eligible to claim and marks them as 'claimed'
Mystery Box
They mystery box is a mystery and all users agree that it does not owe them anything and is not expected to perform or finance critical work to deliver profits. They Mystery Box is a smart contract which is programmed to only be able to send TEAM and MAXI to the Mystery Box Hot Address via flushTeam() and flushMAXI(). These functions are public for anyone to run on behalf of the mystery box, but the public is discouraged from running them by means of a non-refundable transaction fee paid to the Mystery Box Hot Address to run these flush functions.
THE PERPETUAL POOLS CONTRACTS, SUPPORTING WEBSITES, AND ALL OTHER INTERFACES (THE SOFTWARE) IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM
LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

BY INTERACTING WITH THE SOFTWARE YOU ARE ASSERTING THAT YOU BEAR ALL THE RISKS ASSOCIATED WITH DOING SO. AN INFINITE NUMBER OF UNPREDICTABLE THINGS MAY GO WRONG WHICH COULD POTENTIALLY RESULT IN CRITICAL FAILURE AND FINANCIAL LOSS. BY INTERACTING WITH THE SOFTWARE YOU ARE ASSERTING THAT YOU AGREE THERE IS NO RECOURSE AVAILABLE AND YOU WILL NOT SEEK IT.

INTERACTING WITH THE SOFTWARE SHALL NOT BE CONSIDERED AN INVESTMENT OR A COMMON ENTERPRISE. INSTEAD, INTERACTING WITH THE SOFTWARE IS EQUIVALENT TO CARPOOLING WITH FRIENDS TO SAVE ON GAS AND EXPERIENCE THE BENEFITS OF THE H.O.V. LANE. 

YOU SHALL HAVE NO EXPECTATION OF PROFIT OR ANY TYPE OF GAIN FROM THE WORK OF OTHER PEOPLE.

*/
