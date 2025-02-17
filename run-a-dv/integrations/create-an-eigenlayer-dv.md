# Create an EigenLayer DV

{% hint style="danger" %}
The Obol-SDK is in a beta state and should be used with caution. Ensure you validate all important data.
{% endhint %}

This is a walkthrough of creating a distributed validator cluster pointing to an [EigenLayer](https://eigenlayer.xyz/) [EigenPod](https://docs.eigenlayer.xyz/eigenlayer/restaking-guides/restaking-user-guide/native-restaking/create-eigenpod-and-set-withdrawal-credentials/), using the [DV Launchpad](https://docs.obol.org/next/learn/intro/launchpad) and other applications.

### Pre-requisites[​](https://docs.obol.org/next/run/integrations/quickstart-eigenpod#pre-requisites) <a href="#pre-requisites" id="pre-requisites"></a>

* The Ethereum addresses or ENS names for the node operators in the cluster. (Currently the DV Launchpad only supports Metamask or equivalent injected web3 browser wallets.)
* If creating more than one validator, the ability to use the [obol-sdk](https://docs.obol.org/next/adv/advanced/quickstart-sdk) is required.

### Create a SAFE to own the EigenPod[​](https://docs.obol.org/next/run/integrations/quickstart-eigenpod#create-a-safe-to-own-the-eigenpod) <a href="#create-a-safe-to-own-the-eigenpod" id="create-a-safe-to-own-the-eigenpod"></a>

Deploy a [SAFE](https://app.safe.global/) with the addresses of the node operators as signers. A reasonable signing threshold is the same as a cluster (>2/3rds) but use good judgement if a different threshold or signer set suits your use case. The principal ether for these validators will be returned to this address.

### Create an EigenPod[​](https://docs.obol.org/next/run/integrations/quickstart-eigenpod#create-an-eigenpod) <a href="#create-an-eigenpod" id="create-an-eigenpod"></a>

Select the "Create EigenPod" option on the [EigenLayer App](https://app.eigenlayer.xyz/)'s 'Restake' page, using the created SAFE account via WalletConnect. Note the EigenPod's address.

### Create a Splitter for the block reward[​](https://docs.obol.org/next/run/integrations/quickstart-eigenpod#create-a-splitter-for-the-block-reward) <a href="#create-a-splitter-for-the-block-reward" id="create-a-splitter-for-the-block-reward"></a>

Create a Splitter on [splits.org](https://app.splits.org/), to divide the block reward and MEV amongst the operators. Note the split's address.

{% hint style="success" %}
To be recognised as a part of Obol's [1% for Decentralisation](https://blog.obol.tech/1-percent-for-decentralisation/) campaign, you must contribute 3% of execution layer rewards by setting [this address](https://etherscan.io/address/0xDe5aE4De36c966747Ea7DF13BD9589642e2B1D0d) as a recipient on your split. Upcoming Obol EigenPods will support contributing 1% of total rewards instead of 3% of only execution rewards.
{% endhint %}

### Create the DV cluster invite[​](https://docs.obol.org/next/run/integrations/quickstart-eigenpod#create-the-dv-cluster-invite) <a href="#create-the-dv-cluster-invite" id="create-the-dv-cluster-invite"></a>

With these contracts deployed, you can now create the DV cluster invitation to send to Node Operators, this can be done through the DV Launchpad or the Obol SDK.

{% tabs %}
{% tab title="DV Launchpad" %}
* Use the "Create a cluster with a group" [flow](https://docs.obol.org/next/run/start/quickstart_group) on the [DV Launchpad](https://docs.obol.org/next/learn/intro/launchpad.md).
* Choose a cluster name and invite your operator's addresses.
* When setting the withdrawal credentials, select "Custom".
* For "Withdrawal Address", set the EigenPod contract address.
* For "Fee Recipient", set the Split contract address.
* Continue the process of creating a cluster normally, share the invitation link with the operators and have them complete the Distributed Key Generation ceremony.
{% endtab %}

{% tab title="SDK" %}
* If you are creating a cluster with more than one validator, you will need to craft the cluster invitation with the [SDK](https://www.npmjs.com/package/@obolnetwork/obol-sdk).
* Follow the [Create a cluster using the SDK](https://docs.obol.org/next/run/integrations/quickstart-sdk) guide.
* For `withdrawal_address`, set the EigenPod contract address.
* For `fee_recipient_address`, set the Split contract address.
* Continue the process of creating the cluster as per the guide, share the invitation link with the operators and have them complete the Distributed Key Generation ceremony.
{% endtab %}
{% endtabs %}

### Deposit and restake your Distributed Validator[​](https://docs.obol.org/next/run/integrations/quickstart-eigenpod#deposit-and-restake-your-distributed-validator) <a href="#deposit-and-restake-your-distributed-validator" id="deposit-and-restake-your-distributed-validator"></a>

Once you have completed the DKG ceremony, you can continue the flow on the EigenLayer app to activate these validators and restake them. Consult the EigenLayer [documentation](https://docs.eigenlayer.xyz/eigenlayer/restaking-guides/restaking-user-guide/native-restaking/create-eigenpod-and-set-withdrawal-credentials/enable-restaking) to continue the process.

