[![Build Status](https://travis-ci.org/IBM/Decentralized-energy-fabric-on-IBP20.svg?branch=master)](https://travis-ci.org/IBM/Decentralized-energy-fabric-on-IBP20)

# Decentralized Energy with IBM Blockchain Platform

>Hyperledger Fabric sample Decentralized Energy on IBM Blockchain Platform

This code pattern demonstrates setting up a network on the IBM Blockchain Platform and deploying the Decentralized smart contract on the network.  Next, we generate client-side certificates so the developer can subsequently enroll an application identity and then submit transactions on the smart contract.   The application is setup with a Node.js server using the Fabric Node SDK to process requests to the network.

A key application of Blockchain being currently explored is a Decentralized Energy network. The idea stems from a neighborhood where certain Residents are producing energy through Solar panels or other means, and can sell excess energy to Residents needing energy. The transactions would be based on coins in each Resident's account. As per a pre-determined contract and rate, the coins would be debited from the consumer and credited to the producer, for a certain billing period. Each transaction would need to be atomic and added to a Blockchain ledger for trust and verification. The network can include Banks to transact coins for Fiat currency (USD). The network can have Utility Company who can buy or provide energy through the network.

The network consists of Residents, Banks and Utility Companies. Residents can exchange coins for energy among each other.  The application assumes a pre-paid system where transactions occur after the energy is consumed and the values are updated.  The Resident can exchange coins for Fiat money (USD) with Banks on the network.  The Residents can also transact coins for energy with a Utility company on the network.

The code pattern demonstrates how a Node.js smart contract can be packaged using the IBM Blockchain Platform Extension for VS Code. Then, using the extension, you can set up a local instance of the Hyperledger Fabric network, on which you can install and instantiate the contract. Lastly, the application is setup with a Node.js server using the Fabric Node SDK to process transactions that communicate with the network.

When you have completed this code pattern, you will understand how to:

* Package the smart contract using IBM Blockchain Platform Extension for VS Code
* Setup a Hyperledger Fabric network on IBM Blockchain Platform
* Install and instantiate smart contract package onto the IBM Blockchain Platform
* Develop a Node.js server with the Hyperledger Fabric SDK to interact with the deployed network
* Interact with the contract and execute transactions using the SDK.


# Architecture flow

<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/8854447/72169371-fd8ccf80-339c-11ea-99f3-e46a7e005ebe.png">
</p>

1. The Blockchain Operator clones the GitHub repo with the Decentralized Energy smart contract.
2. The Blockchain Operator uses the IBM Blockchain VSCode Extension to package the smart contract.
3. The Blockchain Operator creates a IBM Blockchain Platform 2Install chaincode on the peer node.
4. The IBM Blockchain Platform creates a Hyperledger Fabric network onto a IBM Cloud Kubernetes Service, enabling us to install and instantiate the Decentralized Energy smart contract on the network.
5. The Decentralized Energy web app uses the Hyperledger Fabric Node.js SDK to submit transactions to the Hyperledger Fabric network running on IBM Cloud.
6. The Residents, Banks, and Utility Companies interact with the Decentralized Energy web-app and all transaction details are saved onto the IBM Blockchain Platform, unbeknown to the end-user. 


# Included components
*   [IBM Blockchain Platform](https://www.ibm.com/cloud/blockchain-platform) Gives you total control of your blockchain network with a user interface that can simplify and accelerate your journey to deploy and manage blockchain components on the IBM Cloud Kubernetes Service.
*   [IBM Cloud Kubernetes Service](https://www.ibm.com/cloud/container-service) Creates a cluster of compute hosts and deploys highly available containers. A Kubernetes cluster lets you securely manage the resources that you need to quickly deploy, update, and scale applications.
* [IBM Blockchain Platform Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=IBMBlockchain.ibm-blockchain-platform) Designed to assist users in developing, testing, and deploying smart contracts -- including connecting to Hyperledger Fabric environments.


## Featured technologies
+ [Hyperledger Fabric v1.4](https://hyperledger-fabric.readthedocs.io) is a platform for distributed ledger solutions, underpinned by a modular architecture that delivers high degrees of confidentiality, resiliency, flexibility, and scalability.
+ [Node.js](https://nodejs.org) is an open source, cross-platform JavaScript run-time environment that executes server-side JavaScript code.


### Prerequisites

* [IBM Cloud account](https://cloud.ibm.com/registration/?target=%2Fdashboard%2Fapps)
* [Node v8.x or v10.x and npm v6.x or greater](https://nodejs.org/en/download/)
* [VSCode version 1.38.0 or greater](https://code.visualstudio.com)
* [IBM Blockchain Platform Extension for VSCode](https://marketplace.visualstudio.com/items?itemName=IBMBlockchain.ibm-blockchain-platform)


# Running the application

Follow these steps to set up and run this code pattern. The steps are described in detail below.


### Steps

1. [Clone the repo](#1-clone-the-repo)
2. [Package the smart contract](#2-package-the-smart-contract)
3. [Create IBM Cloud services](#3-create-ibm-cloud-services)
4. [Build a network](#4-build-a-network)
5. [Deploy Decentralized Energy Smart Contract on the network](#5-deploy-decentralized-energy-smart-contract-on-the-network)
6. [Connect application to the network](#6-connect-application-to-the-network)
7. [Run the application](#7-run-the-application)


## 1. Clone the repo

Clone this repository in a folder your choice:

```
git clone https://github.com/IBM/decentralized-energy-fabric-on-IBP20
```


## 2. Package the smart contract

We will use the IBM Blockchain Platform extension to package the smart contract.
* Open Visual Studio code and open the `contract` folder from Decentralized Energy repository that was cloned earlier.

* Press the `F1` key to see the different VS code options. Choose `IBM Blockchain Platform: Package Open Project`.

<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71910509-05036d00-3140-11ea-8b15-7c8aeb403974.png">
</p>

* Click the `IBM Blockchain Platform` extension button on the left. This will show the packaged contracts on top and the blockchain connections on the bottom.

<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/8854447/72169372-fd8ccf80-339c-11ea-8c5a-363d4177fc0d.png">
</p>

* Next, right click on the packaged contract (in this case, select decentralized-energy@0.0.1) to export it and choose `Export Package`.

* Choose a location on your machine and save `.cds` file.  We will deploy this smart contract package on the IBM Blockchain Platform service in a later step.


Now, we will start creating our Hyperledger Fabric network on the IBM Cloud.


## 3. Create IBM Cloud services

* Create the [IBM Cloud Kubernetes Service](https://cloud.ibm.com/kubernetes/catalog/cluster). You can find the service in the `Catalog`. For this code pattern, we can use the `Free` cluster, and give it a name. Note, that the IBM Cloud allows one instance of a free cluster which expires after 30 days. **Note: it could take 20 minutes for the IBM Cloud Kubernetes Service setup to complete**.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71910506-046ad680-3140-11ea-9f4b-8bcb4d2a651b.gif">
</p>
<br>

* Create the [IBM Blockchain Platform](https://cloud.ibm.com/catalog/services/blockchain-platform) service on the IBM Cloud. You can find the service in the `Catalog`, and give it a name.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71910502-046ad680-3140-11ea-9853-3598b9363d91.gif">
</p>
<br>

* After your kubernetes cluster is up and running, you can deploy your IBM Blockchain Platform on the cluster. Again - wait for the IBM Cloud Kubernetes service to indicate it was deployed. The IBM Blockchain Platform service walks through few steps and finds your cluster on the IBM Cloud to deploy the service on.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71910501-046ad680-3140-11ea-8440-9d2fef0be426.gif">
</p>
<br>

* Once the Blockchain Platform is deployed on the Kubernetes cluster, you can launch the console to start configuring your blockchain network.


## 4. Build a network

We will build a network as provided by the IBM Blockchain Platform [documentation](https://cloud.ibm.com/docs/services/blockchain/howto?topic=blockchain-ibp-console-build-network#ibp-console-build-network). This will include creating a channel with a single peer organization with its own MSP and CA (Certificate Authority), and an orderer organization with its own MSP and CA. We will create the respective identities to deploy peers and operate nodes.


#### Create your peer organization CA
  - Navigate to the <b>Nodes</b> tab in the left navigation and click <b>Add Certificate Authority</b>.
  - Click <b>Create an IBM Cloud Certificate Authority</b> and <b>Next</b>.
  - Give it a <b>CA display name</b> of `Org1 CA` and click <b>Next</b>.
  - Specify an <b>CA Administrator Enroll ID</b> of `admin` and <b>CA Administrator Enroll Secret</b> of `adminpw`, then click <b>Next</b>.
  - Review the summary and click <b>Add Certificate Authority</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71913565-bb1d8580-3145-11ea-9eaa-1b4e8a10e985.gif">
</p>
<br>


#### Associate the peer organization CA admin identity
  - In the Nodes tab, select the <b>Org1 CA</b> once it is running (indicated by the green box in the tile).
  - Click <b>Associate identity</b> on the CA overview panel.
  - On the side panel, select <b>Enroll ID</b>. 
  - Provide an <b>Enroll ID</b> of `admin` and an <b>Enroll secret</b> of `adminpw`. Use the default value of `Org1 CA Identity` for the <b>Identity display name</b>.
  - Click <b>Associate identity</b> to add the identity into your wallet and associate the admin identity with the <b>Org1 CA</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71913744-1e0f1c80-3146-11ea-85e4-eea5280aa8e9.gif">
</p>
<br>


#### Use peer organization CA to register the peer and org1 admin identities
  - Select the <b>Org1 CA</b> Certificate Authority and ensure the `admin` identity that was created for the CA is visible in the table.
  - We will register an admin for our organization "org1". Click on the <b>Register User</b> button. Give an <b>Enroll ID</b> of `org1admin`, and <b>Enroll Secret</b> of `org1adminpw`. Set the <b>Type</b> for this identity as `client`. We can specify to <b>Use root affiliation</b> or uncheck this field and select from any of the affiliated organizations from the drop-down list. We will leave the <b>Maximum enrollments</b> field blank. Click <b>Next</b>.
  - We will not be adding any attributes to this user. Click <b>Register user</b>.
  - We will repeat the process to create an identity of the peer. Click on the <b>Register User</b> button. Give an <b>Enroll ID</b> of `peer1`, and <b>Enroll Secret</b> of `peer1pw`. Set the <b>Type</b> for this identity as `peer`. We can specify to <b>Use root affiliation</b> or uncheck this field and select from any of the affiliated organizations from the drop-down list. Click <b>Next</b>.
  - We will not be adding any attributes to this user. Click <b>Register user</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71913929-7c3bff80-3146-11ea-9930-a455f1e45fe2.gif">
</p>
<br>


#### Create the peer organization MSP definition
  - Navigate to the <b>Organizations</b> tab in the left navigation and click <b>Create MSP definition</b>.
  - Enter the <b>MSP Display name</b> as `Org1MSP` and an <b>MSP ID</b> of `Org1MSP`.
  - Under <b>Root Certificate Authority</b> details, specify the peer CA that we created `Org1 CA` as the root CA for the organization.
  - Give the <b>Enroll ID</b> and <b>Enroll secret</b> for your organization admin, `org1admin` and `org1adminpw`. Then, give the Identity name as `Org1 Admin`.
  - Click the <b>Generate</b> button to enroll this identity as the admin of your organization and export the identity to the wallet. Click <b>Export</b> to export the admin certificates to your file system. Finally click <b>Create MSP definition</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71914115-e5bc0e00-3146-11ea-891c-6422bc4c2c4e.gif">
</p>
<br>


#### Create a peer
  - Navigate to the <b>Nodes</b> tab in the left navigation and click <b>Add peer</b>.
  - Click <b>Create an IBM Cloud peer</b> and then click <b>Next</b>.
  - Give the <b>Peer display name</b> as `Peer Org1` and click <b>Next</b>.
  - On the next screen, select `Org1 CA` as the <b>Certificate Authority</b>. Then, give the <b>Peer enroll ID</b> and <b>Peer enroll secret</b> for the peer identity that you created for your peer, that is, `peer1`, and `peer1pw`. Select the <b>Organization MSP</b> as `Org1MSP`, from the drop-down list. Leave the <b>TLS CSR hostname</b> blank. Click <b>Next</b>.
  - The next step is to Associate an identity with this peer to make it the admin of your peer. Select your peer admin identity `Org1 Admin` and click <b>Next</b>.
  - Review the summary and click <b>Add peer</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71914297-53683a00-3147-11ea-9ecb-bace14e5e5c5.gif">
</p>
<br>


#### Create your orderer organization CA
  - Navigate to the <b>Nodes</b> tab in the left navigation and click <b>Add Certificate Authority</b>.
  - Click <b>Create an IBM Cloud Certificate Authority</b> and <b>Next</b>.
  - Give it a <b>CA display name</b> of `Orderer CA` and click <b>Next</b>.
  - Specify an <b>CA Administrator Enroll ID</b> of `admin` and <b>CA Administrator Enroll Secret</b> of `adminpw`, then click <b>Next</b>.
  - Review the summary and click <b>Add Certificate Authority</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71914392-86123280-3147-11ea-9a6f-b6eddab790b1.gif">
</p>
<br>


#### Associate the orderer organization CA admin identity
  - In the Nodes tab, select the <b>Orderer CA</b> once it is running (indicated by the green box in the tile).
  - Click <b>Associate identity</b> on the CA overview panel.
  - On the side panel, select <b>Enroll ID</b>. 
  - Provide an <b>Enroll ID</b> of `admin` and an <b>Enroll secret</b> of `adminpw`. Use the default value of `Orderer CA Identity` for the <b>Identity display name</b>.
  - Click <b>Associate identity</b> to add the identity into your wallet and associate the admin identity with the <b>Orderer CA</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71914593-e73a0600-3147-11ea-8944-1c5e2bbecfba.gif">
</p>
<br>


#### Use orderer organization CA to register orderer and orderer admin identities
  - Select the <b>Orderer CA</b> Certificate Authority and ensure the `admin` identity that was created for the CA is visible in the table.
  - We will register an admin for the "orderer" organization. Click on the <b>Register User</b> button. Give an <b>Enroll ID</b> of `ordereradmin`, and <b>Enroll Secret</b> of `ordereradminpw`. Set the <b>Type</b> for this identity as `client`. We can specify to <b>Use root affiliation</b> or uncheck this field and select from any of the affiliated organizations from the drop-down list. We will leave the <b>Maximum enrollments</b> field blank. Click <b>Next</b>.
  - We will not be adding any attributes to this user. Click <b>Register user</b>.
  - We will repeat the process to create an identity of the orderer. Click on the <b>Register User</b> button. Give an <b>Enroll ID</b> of `orderer1`, and <b>Enroll Secret</b> of `orderer1pw`. Set the <b>Type</b> for this identity as `orderer`. We can specify to <b>Use root affiliation</b> or uncheck this field and select from any of the affiliated organizations from the drop-down list. Click <b>Next</b>.
  - We will not be adding any attributes to this user. Click <b>Register user</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71914721-35e7a000-3148-11ea-8db6-2d3584fca238.gif">
</p>
<br>


#### Create the orderer organization MSP definition
  - Navigate to the <b>Organizations</b> tab in the left navigation and click <b>Create MSP definition</b>.
  - Enter the <b>MSP Display name</b> as `OrdererMSP` and an <b>MSP ID</b> of `OrdererMSP`.
  - Under <b>Root Certificate Authority</b> details, specify the peer CA that we created `Orderer CA` as the root CA for the organization.
  - Give the <b>Enroll ID</b> and <b>Enroll secret</b> for your organization admin, `ordereradmin` and `ordereradminpw`. Then, give the Identity name as `Orderer Admin`.
  - Click the <b>Generate</b> button to enroll this identity as the admin of your organization and export the identity to the wallet. Click <b>Export</b> to export the admin certificates to your file system. Finally click <b>Create MSP definition</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71914893-95de4680-3148-11ea-8a9d-5952c26c8cdc.gif">
</p>
<br>


#### Create an orderer
  
  - Navigate to the <b>Nodes</b> tab in the left navigation and click <b>Add ordering service</b>.
  - Click <b>Create an IBM Cloud Ordering service</b> and then click <b>Next</b>.
  - Give the <b>Ordering service display name</b> as `Orderer` and click <b>Next</b>.
  - On the next screen, select `Orderer CA` as the <b>Certificate Authority</b>. Then, give the <b>Ordering service enroll ID</b> and <b>Ordering service enroll secret</b> for the peer identity that you created for your orderer, that is, `orderer1`, and `orderer1pw`. Select the <b>Organization MSP</b> as `OrdererMSP`, from the drop-down list. Leave the <b>TLS CSR hostname</b> blank. Click <b>Next</b>.
  - The next step is to Associate an identity with this peer to make it the admin of your peer. Select your peer admin identity `Orderer Admin` and click <b>Next</b>.
  - Review the summary and click <b>Add ordering service</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71915205-42b8c380-3149-11ea-8050-5edfd461ae10.gif">
</p>
<br>


#### Add organization as Consortium Member on the orderer to transact
  - Navigate to the <b>Nodes</b> tab, and click on the <b>Orderer</b> that we created.
  - Under <b>Consortium Members</b>, click <b>Add organization</b>.
  - From the drop-down list, select `Org1MSP`, as this is the MSP that represents the peer's organization "Org1".
  - Click <b>Add organization</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71915342-88758c00-3149-11ea-98e2-2ed00dc9c8c3.gif">
</p>
<br>


#### Create the channel
  - Navigate to the <b>Channels</b> tab in the left navigation and click <b>Create channel</b>.
  - Give the <b>Channel name</b> as `mychannel`.
  - Select the orderer you created, `Orderer` from the <b>Ordering service</b> drop-down list.
  - Under <b>Organizations</b>, select `Org1MSP (Org1MSP)` from the drop-down list to add the organization "Org1" as a member of this channel. Click <b>Add</b> button. Set the permissions for this member as <b>Operator</b>.
  - Scroll down to the <b>Channel creator organization</b> section and select `Org1MSP (Org1MSP)` from the dropdown as the <b>Channel creator MSP</b> and select `Org1 Admin` from the dropdown under <b>Identity</b>.
  - Click <b>Create channel</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71915595-15b8e080-314a-11ea-9843-d7df9be30fe5.gif">
</p>
<br>


#### Join your peer to the channel
  - Click <b>Join channel</b> to add a peer to the channel.
  - Select your `Orderer` as the <b>Ordering service</b> and click <b>Next</b>.
  - Enter the name of the <b>Channel</b> as `mychannel` and click <b>Next</b>.
  - Next we need to select which peers should be added to the channel. In our case, we just want to add the peer we created under "Org1". Select `Peer Org1` .
  - Click <b>Join channel</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71915747-67fa0180-314a-11ea-984b-80deb0877d03.gif">
</p>
<br>


## 5. Deploy Decentralized Energy Smart Contract on the network

#### Install a smart contract
  - Navigate to the <b>Smart contracts</b> tab in the left navigation and click <b>Install smart contract</b>.
  - Browse to the location of the Decentralized Energy smart contract package file (it is probably named `decentralizedenergy@0.0.1.cds`), which we packaged earlier using the IBM Blockchain Platform extension for Visual Studio code.
  - Click on <b>Add file</b> and find your packaged smart contract. 
  - Once the contract is uploaded, click <b>Install smart contract</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/72175842-24520280-33ab-11ea-8743-db41298ce204.gif">
</p>
<br>


#### Instantiate smart contract
  - Under <b>Installed smart contracts</b>, find the smart contract from the list (**Note: ours is called decentralizedenergy**) installed on our peer and click <b>Instantiate</b> from the overflow menu on the right side of the row.
  - On the side panel that opens, select the channel, `mychannel` on which to instantiate the smart contract. Click <b>Next</b>.
  - Select the organization members to be included in the endorsement policy. In our case, we need to select `Org1MSP`. Click <b>Next</b>.
  - We can skip the <b>Setup private data collection</b> step and simply click <b>Next</b>.
  - Leave the <b>Function name</b> and <b>Arguments</b> blank.
  - Click <b>Instantiate</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/72175998-7dba3180-33ab-11ea-9025-a560ad942b2c.gif">
</p>
<br>


## 6. Connect application to the network

#### Connect with sdk through connection profile
  - Scroll down to the <b>Instantiated smart contracts</b> section and find the "decentralizedenergy" contract in the list. Click on `Connect with SDK` from the overflow menu on the right side of the row.
  - From the dropdown for <b>MSP for connection</b> choose `Org1MSP`.
  - From the dropdown for <b>Certificate Authority</b> choose `Org1 CA`.
  - Download the connection profile by scrolling down and clicking <b>Download Connection Profile</b>. This will download the connection json which we will use to establish a connection between the Node.js web application and the Blockchain Network.
  - You can click <b>Close</b> once the download completes.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/72176057-9c202d00-33ab-11ea-84f5-4a806decd973.gif">
</p>
<br>


#### Create an application admin
  - Navigate to the <b>Nodes</b> tab in the left navigation, and under <b>Certificate Authorities</b>, choose your organization CA, <b>Org1 CA</b>.
  - Click on <b>Register user</b>.
  - Give an <b>Enroll ID</b> of `app-admin` and <b>Enroll Secret</b> of `app-adminpw`. Set the <b>Type</b> for this identity as `client`. We can specify to <b>Use root affiliation</b> or uncheck this field and select from any of the affiliated organizations from the drop-down list. We will leave the <b>Maximum enrollments</b> field blank. Click <b>Next</b>.
  - Under <b>Attributes</b>, click on <b>Add attribute</b>. Give attribute as `hf.Registrar.Roles` = `*`. This will allow this identity to act as a registrar and issue identities for our app. Click <b>Add attribute</b>.
  - Click <b>Register user</b>.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/71916456-fd49c580-314b-11ea-925f-9103d51cbb57.gif">
</p>
<br>


#### Update application connection profile
  - Copy the connection profile you downloaded into [server folder](web-app/server) and [application folder](/application)
  - Update the [server/config.json](web-app/server/config.json) and the [application/config.json](application/config.json) file with:
    - The connection json file name you downloaded.
    - The <b>enroll id</b> and <b>enroll secret</b> for your app admin, which we earlier provided as `app-admin` and `app-adminpw`.
    - The orgMSP ID, which we provided as `Org1MSP`.
    - The caName, which can be found in your connection json file under "organization" -> "Org1MSP" -> certificateAuthorities". This would be like an IP address and a port.
    - The username you would like to register.
    - Update gateway discovery to `{ enabled: true, asLocalhost: false }` to connect to IBP.
    
Once all this is done, your config.json should look something like this:

```bash
 {
    "connection_file": "mychannel_decentralizedenergy_profile.json",
    "channel_name": "mychannel",
    "smart_contract_name": "decentralizedenergy",
    "appAdmin": "app-admin",
    "appAdminSecret": "app-adminpw",
    "orgMSPID": "Org1MSP",
    "caName": "169.46.208.151:30404",
    "userName": "user1",
    "gatewayDiscovery": { "enabled": true, "asLocalhost": false }
 }
```


## 7. Run the application

### Run the application as admin

* #### Enroll admin

  - First, navigate to the `web-app` directory, and install the node dependencies.
  
    ```bash
    cd web-app/server
    npm install
    ```

  - Run the `enrollAdmin.js` script
  
    ```bash
    node enrollAdmin.js
    ```

  - You should see the following in the terminal:
  
    ```bash
    msg: Successfully enrolled admin user app-admin and imported it into the wallet
    ```

* #### Start the application server

  - From the `server` directory, start the server.

    ```bash
    npm start
    ```

* #### Start the Angular app

  - In a new terminal, open the web client folder and install the dependencies.
  
    ```bash
    cd web-app/angular-app
    npm install
    ```

  - Start the client:
  
    ```bash
    npm start
    ```

You can find the app running at http://localhost:4200/
Click on the green "Authorized Access" button to authorize access. Once that is done, you will be able to register Participants such as Residents, Banks and Utility Companies as well as post transactions between these participants.

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/72174249-3a5dc400-33a7-11ea-9d64-251467f68f10.gif">
</p>
<br>

You can go to the IBM Blockchain Platform v2 console to monitor your network and get information on your channel.


### Run the application as participants

- Navigate to the `application` directory, and install the node dependencies.

  ```bash
  cd application
  npm install
  ```

- Run the `enrollAdmin.js` script

  ```bash
  node enrollAdmin.js
  ```

  You should see the following in the terminal:
  
  ```bash
  msg: Successfully enrolled admin user app-admin and imported it into the wallet
  ```

- Now let's register each of our participants. We will register `R1` as resident, `B1` as bank, `U1` as utility company.  Navigate to `add-participants` folder and register the resident identity:  

  ```bash
  cd add-participants
  node registerResident.js
  ```

  You should see the following in the terminal:
  
  ```bash
  Successfully registered and enrolled user "R1" and imported it into the wallet
  ```

  Similarly register bank and utility company on the network.
  
  ```bash
  node registerBank.js
  ```

  ```bash
  node registerUtilityCompany.js
  ```

- Now add the participants on the state.  The contract stores the id of the identity creating the participant as their `participantId`.  Let's add our resident:

  ```bash
  node addResident.js
  ```

  You should see the following in the terminal:
  
  ```bash
  2019-02-27T06:38:29.252Z - info: [TransactionEventHandler]: _strategySuccess: strategy success for transaction "c092df4098775057a7b712db402e45f3c8420d98fc022dfc331accb580448d4a"

  ...

  ```

  Similarly add bank and utility company on the network.
  ```bash
  node addBank.js
  ```

  ```bash
  node addUtilityCompany.js
  ```

- Now let's perform the `EnergyTrade` and `CashTrade` transactions.  These transactions will verify the sender's id, as the id on the world state before updating the state.  In our case that is our resident R1:

  ```bash
  cd ../invoker-tx/
  node energy-trade.js
  ```

  You should see the following in the terminal followed by updated state of the resident and utility company:
  
  ```bash
  2019-02-27T06:38:29.252Z - info: [TransactionEventHandler]: _strategySuccess: strategy success for transaction "c092df4098775057a7b712db402e45f3c8420d98fc022dfc331accb580448d4a"

  ...

  ```

  Similarly, let's do the `CashTrade` transaction between resident and bank.

  ```bash
  node cash-trade.js
  ```

  You should see the following in the terminal followed by updated state of the resident and the bank:
  
  ```bash
  2019-02-27T06:38:29.252Z - info: [TransactionEventHandler]: _strategySuccess: strategy success for transaction "c092df4098775057a7b712db402e45f3c8420d98fc022dfc331accb580448d4a"

  ...

  ```

<br>
<p align="center">
  <img src="https://user-images.githubusercontent.com/8854447/72288761-c24a0500-3617-11ea-8fcc-101a78941c82.gif">
</p>
<br>


## Troubleshooting

* If you receive the following error on submitting transaction:
`error: [Client.js]: Channel not found for name mychannel`

  It is safe to ignore this error because the ibp2.0 beta has service discovery enabled. (In order to use service discovery to find other peers please define anchor peers for your channel in the ui). If you really want the message to go away you can add the channels section to the connection profile, but it is a warning rather than a true error telling the user the channel is found but not in the connection profile

  As an example you can manually add the following json and updated the IP address and ports manually:

  ```
  "channels": {
          "mychannel": {
              "orderers": [
                  "169.46.208.151:32078"
              ],
              "peers": {
                  "169.46.208.151:31017": {}
              }
          }
      },
  ```


## Links
* [Hyperledger Fabric Docs](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [IBM Code Patterns for Blockchain](https://developer.ibm.com/patterns/category/blockchain/)


## License
This code pattern is licensed under the Apache Software License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1 (DCO)](https://developercertificate.org/) and the [Apache Software License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache Software License (ASL) FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)
