# PolkaAirdrops

- **Team Name:** AI Agents Lab  
- **Payment Address:** 14atBfY6PexLsYLsCUxvEv2Ra5naHWpf6SN2KkFJdMydU47o
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):** 2


## Project Overview :page_facing_up:

### Overview

PolkaAirdrops is an AI-powered airdrop automation platform tailored for crypto projects on the Polkadot network.
Its standout feature is the integration of generative AI technology to create unique NFTs and automate their distribution using the power of AI sentiment analysis to active project ambassadors on social media, particularly Twitter.

Airdrops have proven to be a highly effective method for the marketing and promotion of crypto projects, garnering extensive reach and impact. Notable examples include the Axie Infinity airdrop in 2021, which attracted more than 2 million participants. In 2023, the chainGPT airdrop also made a significant impact, drawing in close to 1 million participants.

Our team is passionate about creating the PolkaAirdrops project because we recognize the untapped potential 
within the Polkadot ecosystem and the critical need for enhanced visibility of its projects. 
We are driven by the opportunity to leverage cutting-edge generative AI technology to bridge this gap,
fostering community engagement and attracting potential investors and users to Polkadot's innovative ecosystem.

The immense potential we see in combining the power of airdrops with the expansive reach of social networks like Twitter provides an exceptional opportunity to amplify the visibility and appeal of Polkadot projects, reaching a diverse and extensive global audience in a way that is both innovative and highly effective.

In our pursuit to realize this vision with PolkaAirdrops, we are leveraging the cutting-edge capabilities of Generative Pre-trained Transformers (GPTs) for advanced natural language processing, sentiment analysis, and art creation. This technology enables us to intelligently and automatically identify and reward positive social media engagements with precision. Simultaneously, we are utilizing EVM-compatible Moonbeam smart contracts to ensure seamless, secure, and cross-chain airdrop distributions.
Moonbeam is a parachain on the Polkadot network. 
enabling cross-chain communication and interoperability among different parachains
in the Polkador ecosystems.
This harmonious integration of GPTs with  Moonbeam's cross-chain functionality is propelling us toward achieving our goal of elevating Polkadot projects' visibility on a global scale.

In addition, the use of AI-driven airdrops can be effectively utilized not only for general promotion in social media but also for specific purposes such as highlighting project upgrades, and events, and even rewarding attendance at conferences. 
In  the last case, by offering attendances unique NFTs for their participation not only increases event visibility but also adds an element of excitement and exclusivity around attending these events.

In summary, PolkaAirdrops represents a significant step forward in the intersection of AI and blockchain technology, particularly in the realm of cryptocurrency marketing and community engagement. 


### Key Features:

* Generative AI-Driven NFT Creation: PolkaAirdrops allows to design and minting of unique NFTs. These NFTs are not only visually distinctive but also embed certain characteristics or metadata that align with the crypto project's theme and ethos. This approach ensures that each NFT is exclusive and resonates with the project's branding.

* Automated Reward Distribution: The platform uses AI to analyze Twitter for posts displaying positive sentiment towards the crypto project. It identifies key active community members, categorizing them as project ambassadors. These ambassadors participating in the airdrop will be automatically rewarded with the unique NFTs created by the AI, fostering a sense of exclusivity and belonging. 

* SnowBall Effect Project Visibility: As more individuals share positive tweets, the number of participants in the airdrop escalates, creating a snowball effect on the social network. Each new ambassador joining the campaign and contributing positive content further amplifies this momentum. Subsequently, these participating ambassadors are automatically rewarded with distinctive NFTs generated by the AI, nurturing an environment of exclusivity and community belonging. This process not only incentivizes continued positive engagement but also significantly broadens the project's reach and impact on the platform.


 

### Project Details

The integration of generative AI for automatically creating and distributing NFTs adds a novel dimension to crypto project promotions. This approach not only enhances user engagement but also elevates the perceived value and uniqueness of the project, potentially leading to higher visibility and adoption rates.

The main architecture of the project is depicted in the figure below

 ![Architecture of the PolkaAirdrops](https://github.com/AI-Agents-Lab/PolkaAirdrops/blob/main/PolkaAirdrops_Architecture.png)

The main components are described here:

* PolkaAirdrops GPT. This is the front-end component that implements the UI. It is leveraging the GPT solution of the OpenAI platform. OpenAI platform allows to design of GPTs to automate the interaction with users. Our users are defined as the projects or event managers who want to create a viral airdrop campaign on Twitter, and also ambassadors and individuals who are posting tweets to propel the project's visibility. The benefit of using the open UI OpenAI platform is threefold:
  * Leverages 1 billion monthly active users in OpenAI GPTs.
  * GPTs are supported on both mobile and desktop devices. 
  * OpenAI is the fastest-growing company on the internet today. 
  
  Our PolkaAirdops GPT allows you to interact with project managers to help launch their airdrop campaigns seamlessly. Our GPT will guide project managers to define the NFT prompt for the project branding and also define the required requirements for the Twitter post analysis.  

* PolkaAirdops Backend Server. This represents the core of the PolkaAirdrop platform. It is implemented entirely with Python. Its main functions are described below:
  * It exposes an API so the GPT can interact with the backend service to create the airdrop campaign. In this process, the airdrop project-specific prompt will be stored and encrypted in the public IPFS. 
  * It uses the Twitter public API to collect the ambassador tweets. 
  * It uses the proprietary OpenAI GPT4 to perform accurate sentiment analysis on the tweets and checks that are related to the airdrop project.   
  * It creates the unique NFT following the prompt instructions already set up by the airdrop project. For this sake, it will use the proprietary OpenAI DALLE-3 API. This unique NFT will be stored in the IPFS using the Python IPFS API where we upload the NFT and obtain back the IPFS URI to mint later the NFT using the project smart contract.
  Below is an example of the call to the DALLE-3 to generate an NFT:
      ```
        from openai import OpenAI
        client = OpenAI()

        response = client.images.generate(
          model="dall-e-3",
          prompt="project airdrop prompt",
          size="1024x1024",
          quality="standard",
          n=1,
        )
        image_url = response.data[0].url
      ```
  * It mints the particular NFT that will be rewarded to the ambassadors using the Web3 Python API. This API allows to minting of the NFT in the Polkadot Moonbeam network. The NFT will be available for project ambassadors in their Polkadot Talisman wallet. Moreover, the NFTs can also be traded in the Mintverse platform which is the world’s leading NFT aggregation marketplace, where users can easily collect and trade various types of NFT assets. Minting is performed using the new feature of dynamic NFT minting available in the project's airdrop smart contract defined below. 



* PolkaAirdops Smart Contract. This contract is a factory smart contract that creates a specific smart contract for the project airdrop allowing to minting and distribution of the NFTs to the rewarded ambassadors. The project manager of the airdrop must send enough GLMR coins to the factory smart contract for the creation of the project's NFT smart contract. 
Moonbeam is a perfect fit for our project because it allows for building cross-chain connected applications in the Polkadot ecosystem.  Moreover, Moonbeam leverages EVM-compatible smart contracts programming where our team has extensive expertise. 
Here is an excerpt of the connection of the backend server to the Moonbeam smart contract.

    ```
    from web3 import Web3

    provider_rpc = {
        "development": "http://localhost:9944",
        "moonbase": "https://rpc.api.moonbase.moonbeam.network",
    }
    web3 = Web3(Web3.HTTPProvider(provider_rpc["moonbase"]))  

    ```



### PolkaAirdrop UI Mockups 

Our team already developed a UI mockup in the OpenAI platform for our PolkaAirdrops GPT. 
This is shown in the figure below.

 ![Overview of GPTs in the OpenAI platform](https://github.com/AI-Agents-Lab/PolkaAirdrops/blob/main/OpenAI_GPTs.png)


As you can see in the figure, the users will see our PolkaAirdrops GPT where they can manage the airdrop campaign and also claim the NFT airdrops. 
The PolkaAirdrops GPT is a specific GPT that is viewed and directly accessible by billions of users worldwide who are using the OpenAI platform. Users can install it for free in their own OpenAI UI. 


Once users have installed the PolkaAirdrops GPT, they will see the PolkaAirdrop UI as seen in the figure below. 

![Overview of the PolkaAirdrop GPT](https://github.com/AI-Agents-Lab/PolkaAirdrops/blob/main/OpenAI_Polka.png)

The figure shows at the bottom the user's main actions that will trigger the interaction with the PolkaAirdrop GPT:  
* _How do I create an airdrop for my project?_. In this action the GPT will guide through the different steps to set up the airdrop such as defining the project manager address, the project prompt NFT, the requisites for ambassadors to get rewarded the NFT, duration of the airdrop, among other configurations. 

* _Can you guide me on participation in the airdrop?_. This action will inform the ambassadors of the actions that they have to perform to gain the NFT reward. 

* _How do I redeem the airdrop?_. This is after the ending of the airdrop campaign, ambassadors can come back here to redeem the NFT based on their posts performed on the Twitter social network. 

* _What are the current airdrops on the Polkadot network?_. This is informative of the current ongoing airdrop in that ambassadors can participate in promoting the Polkadot project. 

###  PolkaAirdrop's Limitations 

* We are not intending to trade NFTs. This is not a marketplace of NFTs where anyone can sell and buy NFTs. For this purpose, there are already platforms that are offering these services such as  Mintverse. 

* We are focused on NFT airdrops only. The project can be extended to support later token-based airdrops as well as using a similar architecture. However, NFT airdrops provide value benefits with respect to token-based airdrops: 
  * Early access and exclusive benefits: NFT airdrops may provide users with early access to new features, exclusive content, or other perks. This can give them a sense of privilege and make them feel more invested in the project.
  * Potential value: Users can receive valuable NFTs for free, which could potentially increase in value over time. This can be an attractive incentive for users to participate in airdrops.
  * Increased visibility and shareability. NFT airdrops are highly shareable in social networks due to the visual nature of the NFT. 


* Project promotion is limited to the Twitter social network. Although there are multiple social networks available such as YouTube, and Instagram. Twitter represents a social network as large as these platforms with a Monetizable Daily Active Users (mDAU) of 330 million.
Youtube and Instagram have 129 mDAU and 330 mDAU, respectively. 
Moreover, Twitter has been used as an excellent platform for building communities around crypto projects and 
Twitter is home to a large number of crypto influencers, who are individuals with a large following and a high level of credibility among the crypto community. 

* It is not a NFT wallet. Our project is not a crypto wallet to view your NFTs. For this purpose, you can use the Talisman wallet. PolkaAirdrop is only designed to automate the distribution of airdrops.


### Ecosystem Fit

*  Where and how does your project fit into the ecosystem?

  It will fit in the User Interface open-source Polkadot Tech Stack. 
  Our project will offer listing and managing of current airdrops on the Polkadot ecosystem.
  
  Up to now, there is no such solution already implemented in the Polkadot Tech Stack. 
  
  Our solution, designed to be completely open-source, directly benefits Polkadot projects
  by offering them access to our AI-driven automation software stack. 
  This innovative tool is specifically crafted to significantly boost their 
  visibility on social networks, enhancing their outreach and engagement within the digital community.



*  Who is your target audience (parachain/dapp/wallet/UI developers, designers, your own user base, some dapp's userbase, yourself)?

  Our target audience primarily consists of Polkadot projects aiming to extend their reach to a broader audience. Additionally, our project introduces an unparalleled solution for bridging the gap between social network influencers and ambassadors and the Polkadot project teams. This innovative merging is designed to create a mutually beneficial ecosystem where influencers and ambassadors can significantly amplify the visibility and appeal of Polkadot projects, driving engagement and adoption in the wider crypto community. Through this strategic alignment, PolkaAirdrops sets a new standard in digital marketing within the blockchain space, offering a unique and powerful tool for Polkadot projects to stand out in an increasingly competitive market.



*  What need(s) does your project meet?
  
  Our project, PolkaAirdrops, meets several critical needs in the Polkadot Tech Stack:

  * Enhanced Project Visibility: It addresses the fundamental need for increased visibility and recognition of Polkadot projects within the crowded and competitive cryptocurrency market. Currently, there is a lack of ambassadors and influencers embracing
  Polkadot projects. Our project solves this critical need by automating the crowdsourcing of project ambassadors on social media using 
  NFT airdrops.

  * Effective Community Engagement: The project provides an effective way for Polkadot projects to engage with and expand their community, particularly by connecting with influencers and ambassadors on social media platforms like Twitter. 

  * Rewarding User Participation: By integrating airdrops with social media engagement, our project fulfills the need to incentivize and reward active community participation, which is crucial for building a loyal and enthusiastic user base.


* Are there any other projects similar to yours in the Substrate / Polkadot / Kusama ecosystem?

  Our project is unique in the Polkadot ecosystem. However, recently it has been launched this year (2023) a similar project that uses AI to generate NFT automatically. This project is called ChainGPT, https://www.chaingpt.org.
  This project has been successfully launched in the Ethereum network standing today a market cap of $38 million.
  The main difference with this project is that we are automating the promotion and distribution of NFTs on social networks using AI sentiment analysis.
  In addition,  in our project, we are tapping into the vast and swiftly growing OpenAI ecosystem, leveraging its global influence and reach with the innovative Polkadot ecosystem.


## Team :busts_in_silhouette:

### Team members

- Jose Carlos Sancho, (founder, Ph.D. in Computer Science, AI, and smart contract developer) 
- Alexander Salas (Full-stack developer and AI developer)
- Mariana Matheus (social media marketing expert) 


### Contact

- **Contact Name:**  Jose Carlos Sancho
- **Contact Email:** jcsanchop@gmail.com
- **Website:**       https://aiagentslab.com

### Legal Structure

- **Registered Address:** 500 4th St NW, Suite 102, Albuquerque, NM 87102, USA.
- **Registered Legal Entity:** AI Agents Lab LLC

### Team's experience

Jose Carlos Sancho, the founder of AI Agents Lab, currently holds a Ph.D. in Computer Science. 
He has 10 years of experience in blockchain technology, and NFTs, and is currently in AI Generative Pre-trained Transformers (GPTs).
Alexander Salas, senior software developer currently contributing to many AI projects. 
Mariana Matheus graduated in Business administration with a special interest in marketing on social media. 

Overall, our team has extensive experience in developing different software stacks.
Our team developed an NFT project in the past. We have solid programming expertise in NFT smart contracts on the EVM Ethernet network.
In addition, we have expertise in developing the OpenAI software stack using the OpenAI API.
Recently, we have developed several trained GPTs that are publicly available:
* CryptoMastery: https://chat.openai.com/g/g-xVvJBeYik-crypto-mastery 
* Photorealistic: https://chat.openai.com/g/g-lp1vmS7nC-photorealistic
* BrainWave: https://chat.openai.com/g/g-o74FlvLep-brainwave



This is our first time applying to the Web3 Foundation Grants. 


### Team Code Repos

- https://github.com/AI-Agents-Lab/PolkaAirdrops


Please also provide the GitHub accounts of all team members. If they contain no activity, references to projects hosted elsewhere or live are also fine.

- https://github.com/jcsancho
- https://github.com/ajsb85

### Team LinkedIn Profiles (if available)

- https://www.linkedin.com/josecsancho/
- https://www.linkedin.com/ajsb85/
- https://www.linkedin.com/mariana-matheus-872a71262/


## Development Status :open_book:

We have started to design and configure the PolkaAirdrops GPT, as you can see in 
the screenshots shown above and the project GitHub page. 
In addition, ongoing work has been also performed
in defining the overall architecture of the PolkaAirdrop platform in detail,
as you can see in this proposal.

Furthermore, we have also been researching the Polkadot Forum.
We have found two exposed 
critical top priorities in the Polkadot ecosystem which
are (1) Marketing and (2) BizDev as you can see in the following recent post 
in the Polkadot Forum:
https://forum.polkadot.network/t/make-polkadot-great-again/4004


These top priorities align well with the direction of our project, 
PolkaAirdrops, which is addressing these critical areas through its innovative use of AI in marketing and community engagement within the Polkadot network. 
In addition,  PolkaAirdrops is well-aligned with  business development (BizDev).
PolkaAirdrops secures a sustainable revenue source by introducing a charge for every airdrop campaign. Through this strategy, PolkaAirdrops not only maintains a steady financial flow but also strengthens its position as an integral contributor to the business growth within the Polkadot ecosystem, leveraging advanced AI technologies.


## Development Roadmap :nut_and_bolt:

### Overview

- **Total Estimated Duration:** 3 months
- **Full-Time Equivalent (FTE):**  5 FTE
- **Total Costs:** 30,000 USD.

### Milestone 1 — GPT training 

- **Estimated duration:** 6 weeks
- **FTE:**  2.5
- **Costs:** 15,000 USD

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | License | Apache 2.0 |
| **0b.** | Documentation | We will provide technical documents and user guides |
| **0c.** | Testing and Testing Guide | Core functions will be fully covered by comprehensive unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests. |
| **0d.** | Docker | We will provide a Dockerfile that can be used to test all the functionality delivered with the GPT trained. |
| 1.      |  UI Design        | We will design the main actions for creation, managing, and in participating airdrops in the GPT UI. |
| 2.      |  GPT Training     | We will train the GPT to perform the different actions designed previously. |
| 3.      |  GPT API          | We will implement the GPT API calls that will interface with the backend server.  |
| 4.      |  NFT Creation     | We will implement the NFT creation functions in the backend server using the  openAI API to create NFTs.|
| 5.      |  IPFS Storage     | We will implement the IPFS functions to store  the NFTs and prompts in the backend server.  |
| 6.      |  Twitter          | We will implement the sentiment analysis  functionality  in the backend server using the Twitter API.  |
| 7.      |  Testing GPT      | Testing the implemented components above. Achieve a testing coverage of the functionalities above 90%  |


### Milestone 2  — NFT smart contract factory

- **Estimated duration:** 6 weeks
- **FTE:**  2.5
- **Costs:** 15,000 USD

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| **0a.** | License | Apache 2.0 |
| **0b.** | Documentation | We will provide technical documents and user guides |
| **0c.** | Testing and Testing Guide | Core functions will be fully covered by comprehensive unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests.|
| **0d.** | Docker | We will provide a Dockerfile that can be used to test all the functionality delivered with the NFT smart contract factory. |
| **0e.** | Article | We will publish an article video that explains the functionality of the project. First, from the project manager, we will show how to create an airdrop campaign. And lastly, from the ambassador side, we will show how to participate and redeem NFTs. |
| 1. | Factory Smart Contract  | We will deliver  the Moonbeam smart contract factory that will create the different project smart contracts. |
| 2. | NFT Dynamic Smart Contract | We will deliver the Moonbeam dynamic smart contract for projects that will mint the NFTs and distribute the NFTs. |
| 3. | Backend API  | We will develop the API in the backend server to interact with the smart contract factory.  |
| 4. | Monetization | We will develop the platform monetization mechanism to support future  developments.  |
| 5. | Testing Smart Contracts  | Testing the smart contract robustness and functionality as well as the monetization mechanism.  |





## Future Plans

* We will extend the PolkaAirdrop project to support token-based airdrops.
* We will extend the promotion of airdrops on other popular social media networks such as Instagram or WeChat.

The project will be maintained after the grant. We will use our funds, and the project 
is proposing a unique business model already being used in other similar platforms such as the ChainGPT project. 
In particular, this business model is based on collecting a fee for each NFT airdrop campaign launch in the platform.


## Additional Information :heavy_plus_sign:


**How did you hear about the Grants Program?** Web3 Foundation website
