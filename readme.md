# OrdiSwap

In the wake of BTC's significant upgrades like [Segregated Witness](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki) (SigWit) and [Taproot](https://trustmachines.co/learn/bitcoin-taproot-upgrade-basic-breakdown/), which enhanced scalability and privacy, and the advent of [Ordinals](https://docs.ordinals.com/), the ecosystem has seen a surge in innovative applications. One such evolution is the emergence of [BRC-20 tokens](https://domo-2.gitbook.io/brc-20-experiment/), poised to unlock new decentralized possibilities on BTC's secure infrastructure.

Despite Bitcoin's technological progress, the full potential of BTC and BRC-20 tokens remains underutilized due to the lack of specialized exchange infrastructure, a gap further emphasized by data showing **78% of Bitcoin's supply as illiquid**, highlighting the urgent need for a tailored platform that can both meet BRC-20's unique demands and unlock Bitcoin's latent value within the broader DeFi ecosystem.

![image](https://hackmd.io/_uploads/BkG3cM-IT.png)
###### <Center>Liquid and Illiquid Supply: (Source: Glassnode)
</Center>

To bridge this gap, we're excited to introduce **OrdiSwap** - a pioneering swap protocol, marks a significant leap in the Bitcoin network, introducing a visionary and transformative platform tailored for the trading of BRC-20 assets. This innovation not only inherits the robust security framework of BTC but also revolutionizes it by unlocking unprecedented liquidity, thereby transforming Bitcoin into a dynamic, [interest-earning asset](https://www.pm-research.com/content/iijpormgmt/23/2/86). OrdiSwap's unique approach to liquidity provision and asset exchange ensures efficiency and security in transactions, facilitating seamless token swaps while democratizing liquidity in an unprecedented manner. Our vision extends beyond mere facilitation; it's about catalyzing a new era in decentralized finance, leveraging BTC's evolving ecosystem. This launch signifies the dawn of a new decentralized finance era for Bitcoin, enabling a vibrant, inclusive financial ecosystem where Bitcoin transitions from digital gold to a cornerstone in decentralized finance.


This article unfolds in four concise yet comprehensive parts.

- First, we delve into **OrdiSwap's technical architecture**, explaining its integration and functionality in the BTC ecosystem.
- The second part focuses on the **OrdiAMM mechanism**, highlighting its role in enhancing BRC-20 assets liquidity and price efficiency.
- The third section introduces the **OrdiBridge**, a key feature enabling interoperability between BRC-20 and ERC-20 tokens, thereby expanding liquidity across the EVM chain.
- Finally, we discuss our **token economic design**, outlining how it supports sustainable growth and protocol health.

Together, these sections offer a complete understanding of OrdiSwap's innovative approach in the DeFi space.

## OrdiSwap Tech Archtretucre

OrdiSwap adeptly integrates the BTC network and [RGB protocols](https://blackpaper.rgb.tech/), positioning BRC-20 assets to leverage BTC's foundational security layer while utilizing RGB for application and protocol functionalities. This architecture not only guarantees the absolute security of assets but also maximizes the liquidity and transactional efficiency of BRC-20 assets. It achieves this while concurrently reducing transaction costs and minimizing the burden on the BTC network.

The operational mechanics of OrdiSwap are elucidated through the complete lifecycle of a transaction, encompassing the creation of a liquidity pool, execution of a Swap transaction, and the subsequent withdrawal of assets back to the BTC network:

#### 1. Creation of a Liquidity Pool

Creation of a Liquidity Pool: To initiate a liquidity pool for BRC-20 Token A and BRC-20 Token B, users simply transfer their assets to an Ordi-Lock address. This mechanism securely locks both tokens A & B on the BTC network, simultaneously minting equivalent RGB20 Tokens in the RGB layer for Token A and Token B.

![1](https://hackmd.io/_uploads/rkr0ODW8p.png)
###### <Center>Liquidity Pool Creation Diagram (Add Liquidity)
</Center>

This process establishes a TokenA:TokenB swap pool in the RGB layer. Notably, each BRC-20 to RGB-20 asset conversion is accompanied by the automatic generation of a [commitment proof](https://www.iacr.org/archive/asiacrypt2010/6477178/6477178.pdf), ensuring verifiable asset ownership and mitigating the risk of third-party malfeasance.

#### 2. Swap Execution in the OrdiAMM

The core of OrdiSwap's functionality lies in the RGB layer, where the OrdiAMM model is implemented. OrdiAMM is based on the traditional AMM model, and use [x * y = k](https://ethresear.ch/t/improving-front-running-resistance-of-x-y-k-market-makers/1281) formula.

This model, uniquely designed for BRC-20 asset swaps, allows for efficient, low-cost trading of two BRC-20 tokens. Diverging from traditional AMM models, OrdiAMM optimizes liquidity concentration within specific price ranges, **dynamically adjusting** with the pool's asset volume. This feature ensures maximum liquidity utilization, thereby enhancing LP returns.
![Bitcoin (4)](https://hackmd.io/_uploads/BkU6gI-8p.png)
###### <Center>OrdiAMM Liquidity and Price Equilibrium Formulas
</Center>

The effectiveness of OrdiAMM is further evidenced through comparative data analysis, contrasting the cost-efficiency and returns against traditional AMM models and BTC network swaps.

![Bitcoin (7)](https://hackmd.io/_uploads/rk1k08W8a.png)
###### <Center>OrdiAMM Liquidity Protection Efficacy Compared to General AMM
</Center>


#### 3. Withdrawal Logic

Post-swap, users or LPs wishing to withdraw assets back to the BTC network are facilitated by a streamlined process. They simply submit the automatically generated [commitment proof](https://www.iacr.org/archive/asiacrypt2010/6477178/6477178.pdf), validating their RGB20 asset ownership. OrdiSwap rigorously verifies each withdrawal commitment, annihilating an equivalent amount of RGB20 assets upon verification, and correspondingly transferring BRC-20 assets to the designated BTC network address.

![3](https://hackmd.io/_uploads/rJOXFPZUT.png)
###### <Center>Liquidity Pool Creation Diagram (Remove Liquidity)
</Center>

Additionally, a comparative analysis of the time and cost efficiencies of BRC-20 transfers and transactions via OrdiSwap, as opposed to traditional BTC network processes, highlights OrdiSwap's superior performance metrics.

We firmly believe that OrdiSwap is at the forefront of a revolutionary shift in decentralized finance. By harmoniously integrating the security of the BTC network with the efficiency of the RGB and Lightning networks, OrdiSwap sets the stage for a new era of hybrid protocols. This innovative approach not only exemplifies the untapped potential of Bitcoin-based systems but also paves the way for a burgeoning ecosystem of decentralized applications.

We envision a future where the robust security of BTC and the agility of the RGB and Lightning networks coalesce, fostering a wave of decentralized innovation. OrdiSwap is not just a platform; it's a catalyst for a decentralized Bitcoin-based renaissance, redefining the boundaries of what's possible in the blockchain domain.

## OrdiBridge

OrdiBridge is a key innovation in OrdiSwap's suite, designed to seamlessly connect the BTC and Ethereum ecosystems. Its primary role is to solve the challenge of liquidity fragmentation in the world of decentralized finance.

The OrdiBridge operates through smart contracts deployed on **both the RGB and EVM layers** (Layer 1 and Layer 2s). This dual deployment enables efficient and secure transactions between these two major blockchain ecosystems. The process for Ethereum users to engage with BTC's BRC-20 tokens is streamlined:

1. **Lock and Mint:** Users can lock ERC-20 assets, such as WETH or USDC, into the OrdiBridge smart contract on EVM. In response, [an equivalent amount of RGB20 tokens is minted on the RGB layer](https://bitcoinops.org/en/topics/htlc/), typically within [12 to 15 minutes](https://ethereum.org/fil/roadmap/single-slot-finality/#:~:text=It%20takes%20about%2015%20minutes%20for%20an%20Ethereum%20block%20to%20finalize.). These RGB20 tokens can then be used to transfer or swap with BRC-20 tokens via OrdiSwap.
    
    ![2](https://hackmd.io/_uploads/rJ4WFwZI6.png)
    ###### <Center>How Ordibridge Works
    </Center>

2. **Wallet Integration and Network Switching:** We're also focusing on direct integration of OrdiSwap with well-known EVM wallets like [MetaMask](https://metamask.io/) and [Rabby](https://rabby.io/). This integration will allow Ethereum users to easily switch networks to RGB layer after lock their ERC-20 assets and mint RGB-20 assets, and trade with their new RGB-20 assets directly in OrdiSwap, and [natively in their MetaMask wallet](https://dappradar.com/blog/guide-on-how-to-switch-network-in-metamask), without the need for develop additional wallets.

    ![Bitcoin (10)](https://hackmd.io/_uploads/HJxR1dW8T.png)
    ###### <Center>Revolutionizing Composability: Igniting Innovation with the EVM-RGB Compiler
    </Center>

This approach is groundbreaking. It opens up the BTC ecosystem to a vast pool of liquidity - estimated at around [$60 billion](https://defillama.com/chains/EVM) - from Ethereum's Layer1 and Layer2 platforms.

By bridging these two ecosystems, OrdiBridge not only enhances liquidity but also makes decentralized finance more interconnected and accessible. It's a significant step towards a more fluid, dynamic, and prosperous blockchain environment.

## Token Economic