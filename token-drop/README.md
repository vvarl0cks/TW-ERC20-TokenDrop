## Token Drop Example

In this guide, we will utilize the [**Token Drop**](https://portal.thirdweb.com/contracts/token-drop) contract to release ERC-20 tokens!

We also utilize the token drop's [claim phases](https://portal.thirdweb.com/pre-built-contracts/token-drop#setting-claim-phases) feature, to release the tokens for a price, and only allow a certain amount to be claimed per wallet.

🤖 **Check out the Demo here**: https://warlocks-erc20-tokendrop.vercel.app   

<a href="https://github.com/vvarl0cks/TW-ERC20-TokenDrop"><img src="https://iili.io/HLyqum7.jpg" alt="HLyqum7.jpg" border="0" /></a>

## Tools:

- [**thirdweb Token Drop**](https://portal.thirdweb.com/contracts/token-drop): thirdweb's Token Drop contract is a way of releasing your ERC20 tokens!

- [**thirdweb React SDK**](https://docs.thirdweb.com/react): To connect to our NFT Collection Smart contract via React hooks such as [useTokenDrop](https://docs.thirdweb.com/react/react.usetokendrop), connect user's wallets, and other awesome hooks like [useActiveClaimCondition](https://docs.thirdweb.com/react/react.useactiveclaimcondition) and [useClaimIneligibilityReasons](https://docs.thirdweb.com/react/react.useclaimineligibilityreasons).

- [**thirdweb TypeScript SDK**](https://docs.thirdweb.com/typescript): To claim/mint tokens from the token drop with [.claim](https://portal.thirdweb.com/pre-built-contracts/token-drop#claiming-tokens) , view token balance with [.balanceOf](https://portal.thirdweb.com/pre-built-contracts/token-drop#token-balance), and transfer tokens with [.transfer](https://portal.thirdweb.com/pre-built-contracts/token-drop#transfer-tokens).

## Using This Repo   
   
```bash
$ npx thirdweb create@latest create app
Need to install the following packages:
  thirdweb@0.10.25
Ok to proceed? (y) 

    $$\     $$\       $$\                 $$\                         $$\       
    $$ |    $$ |      \__|                $$ |                        $$ |      
  $$$$$$\   $$$$$$$\  $$\  $$$$$$\   $$$$$$$ |$$\  $$\  $$\  $$$$$$\  $$$$$$$\  
  \_$$  _|  $$  __$$\ $$ |$$  __$$\ $$  __$$ |$$ | $$ | $$ |$$  __$$\ $$  __$$\ 
    $$ |    $$ |  $$ |$$ |$$ |  \__|$$ /  $$ |$$ | $$ | $$ |$$$$$$$$ |$$ |  $$ |
    $$ |$$\ $$ |  $$ |$$ |$$ |      $$ |  $$ |$$ | $$ | $$ |$$   ____|$$ |  $$ |
    \$$$$  |$$ |  $$ |$$ |$$ |      \$$$$$$$ |\$$$$$\$$$$  |\$$$$$$$\ $$$$$$$  |
     \____/ \__|  \__|\__|\__|       \_______| \_____\____/  \_______|\_______/ 

 💎 thirdweb-cli v0.10.18 💎
```

- Create a Token Drop contract via the thirdweb dashboard on the Mumbai test network.
- Create a project using this example by running:

```bash
npx thirdweb create --template token-drop
```

- Replace my demo token drop contract address (`0x33dEb4e6b8442F6d06f7b46DC9598Dc72edEdA49`) with your token drop contract address!

# Guide

## Configuring the ThirdwebProvider

The thirdweb provider is a wrapper around our whole application.

It allows us to access all of the React SDK's helpful hooks anywhere in our application.

```jsx
// This is the chain your dApp will work on.
const activeChainId = "mumbai";

function MyApp({ Component, pageProps }) {
  return (
    <ThirdwebProvider desiredChainId={activeChainId}>
      <Component {...pageProps} />
    </ThirdwebProvider>
  );
}
```

## Connecting User's Wallets

We use the [useMetamask](https://portal.thirdweb.com/react/react.usemetamask) hook to connect with user's wallets.

```jsx
const connectWithMetamask = useMetamask();

// ...
<button onClick={connectWithMetamask}>Connect with Metamask</button>;
```

## Getting the token drop contract

We use the [useContract](https://docs.thirdweb.com/react/react.useContract) hook to get the token drop contract:

```jsx
const { contract: tokenDropContract } = useContract(
  "0x33dEb4e6b8442F6d06f7b46DC9598Dc72edEdA49",
  "token-drop"
);
```

## Claiming Tokens

We use the `claim` function and pass in the desired amount of tokens to claim inside a `Web3Button` component:

We store a value the user types into an input field in state:

```jsx
const [amountToClaim, setAmountToClaim] = useState("");

// ...

<div className={styles.claimGrid}>
  <input
    type="text"
    placeholder="Enter amount to claim"
    onChange={(e) => setAmountToClaim(e.target.value)}
    className={`${styles.textInput} ${styles.noGapBottom}`}
  />
  <Web3Button
    colorMode="dark"
    contractAddress="0x33dEb4e6b8442F6d06f7b46DC9598Dc72edEdA49"
    action={(contract) => contract.erc20.claim(amountToClaim)}
    onSuccess={() => alert("Claimed!")}
    onError={(err) => alert(err)}
  >
    Claim Tokens
  </Web3Button>
</div>;
```

## Join our Discord!

For any questions, suggestions, join our discord at [https://discord.gg/cd thirdweb](https://discord.gg/thirdweb).    

## <p align="center">[🤖 Warlocks!](http://warlocks.netlify.app)
