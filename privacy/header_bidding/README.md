# Header Bidding

## Inferring Tracker-Advertiser Relationships in the Online Advertising Ecosystem using Header Bidding
- Challenge
	- Different entities in online advertising and tracking ecosystems are incentivized to share information with each other through client-side or server-side mechanisms. 
	- Inferring data sharing between  entities on the server-side is hard.
- KASHF: infer data sharing relationships between advertisers and trackers by studying how an advertiser's bidding behavior changes as we manipulate the presence of trackers.
	- Relies on: advertisers with knowledge of a user's browsing history will bid differently (potentially higher) than an advertiser having no knowledge of a user's browsing history. 
	- An advertiser’s assessment of the value of a user (i.e., bids) is highly dependent on the available information (i.e., browsing history)
	- Assumption: an advertiser's bids for a persona will change when it has an information flow originating from some tracker which has seen the persona before. 
	- Random Forest classifer:
		- Given edge 1 (from client to tracker) and edge 3 (from bidder to client), predict edge 2 (from tracker to bidder)
		- Assumption: trackers that have a high impact on our model for a particular advertiser are more likely to have a data sharing relationship with the advertiser than those having no impact on our model.
		- Data processing: bid values are discretized into 3 categories.
		- Explanability: obtain a list of trackers ranked by their influence on each advertiser: 1. External databases, 2. Client-side cookie syncing.
		- Results: 75%-83% accuracy shows the trained ML models can leverage tracker presence to accurately predict bids by different advertisers.
- Contributions
	- Measuring bidding behavior of advertisers
	- Uncovering tracker-advertiser relationships
		- Online ads and tracking ecosystems may be shifting from the client-side to the servert-side.
			- Motivations: 1. Advertisers and trackersare shifting to server-side data sharing to circumvent client-side blocking tools, 2. Browser extensions can block ads and trackers at the client-side.
- Background
	- Online advertising ecosystem includes middle-men. Protocols, e.g. real-time bidding (RTB), require publishers and advertisers to identify, offer, and respond to ad impression opportunities in near real-time. 
	- RTB: only exposes the winnign bid and the corresponding winner in the auction, and does not expose the highest bid due to its use of the second-price auction.
		- 3 phases: 1. Ad request, 2. Bid collection, 3. Ad placement.
		- Sequential process results in less competition for bids and subsequently reduces publisher yield from advertising.
	- HB: offers the ad inventory to multiple bidders simultaneousl, and essentially flattens the waterfull, forcing increased competition among different bidders for ad impressions and increasing the yield for publishers.
		- 2 phases: 1. Ad request, 2. Ad placement.
	- Supply-side platforms (SSPs) put up ad inventory of publishers for sale at ad exchanges (AdXes), which are marketplaces that run real-time auctions for individual ad slots.
	- Demand-side platforms (DSPs) use sophisticated models to determine how much to bid for eean ad slot based on the user information retrieved from data management platforms. 
	- Cookie sync allows two entities to map their cookies to each other and get a more complete view of a user's browsing history
	- It's important but hard to infer both client-side and server-side data sharing between different entities in the online advertising ecosystem.
	- Traditional RTB only exposes the winning bid at the client-side; HB exposes all bids made by differnt advertisers at the client-side. 
	- Entities: 1. publishers, 2. servers, 3. supply side platforms, 4. ad exchanges, 5. demand side platforms, 6. data management platforms
	- Online Tracking Ecosystem: 
		- Use cookies to deterministically identify users across the web as trackers assign unique identifiers to individual users.
		- Trackers use cookie syncing in order to map each other's identifiers of a user. To prevent cookie from being deleted by users, trackers reply on cookie respawning and other stateless techniques.
	- Synergy between online advertising and tracking
		- Contextual targeting: ads shown to a user are only dependent on the content of the page being viewed.
		- Behavioral targeting: ads shown are based on the interests and behavior demonstrated by the user.
	- Value of users
		- The winning price is the bid value of the second-highest bidder plus a predetermined amount because RTB uses the second-price auction.
	- Bidding results
		- Measurements on the client side
		- Cost-per-mille (CPM): price paid for 1000 ad impressions.
		- Conclusion: 1. A user's persona impacts bids placed by an advertiser, 2. Different bidders have preferences and aversions for different personas and only a few personas are universally preferred, 3. Bidders have to pay substantially higher prices than their average bids to win the auctions, 4. The averaging winning bid in HB is 3.4X th eaverage winning bid of RTB.

## Harpo: Learning to Subvert Online Behavioral Advertising
- Harpo: a principled learning-based approach to subvert online behavioral advertising through obfuscation.
	- Uses RL to adaptively interleave real page visits with fake pages to distort a tracker's view of a user's browsing profile.
	- Formulated the selection of obfuscation URLs as a MDP which selects URLs to maximize the distortion of the tracker's estimate of the user's interests.
	- Metric
		- Loss for the tracker, which represents the percentage of segments of the obfuscated persona which were not segments of the base persona: L1
		- Loss for the tracker, which aims to quantify the profile distortion: L2
		- Loss for bid price, which is the increase of the proportion of high bids in the obfuscated persona as compared to the corresponding base persona: L3
		- Loss for bid price, which is the average ratio of bid values of an obfuscated persona over its corresponding base persona: L4.
	- Workflow
		- 1. Parse content from visited URL pages, and featurize it using an embedding
		- 2. Train an RL agent that selects obfuscation URLs to optimize its reward based on the extracted featurtes.
		- 3. After training, RL agent is used by a URL agent that inserts obfuscation URLs, interleaving them with user URLs.
	- Modules
		- 1. A content feature extraction module to convert text to a document embedding
		- 2. An RL agent takes document embedding as input and output obfuscation URLs
		- 3. A surrogate model, trained to replicate real-world user profiling and ad targeting models
		- 4. A URL agent which inserts obfuscation URLs in the web browsing profile of personas.
	- Architecture
		- Implemented as a browser extension. Architecture inclues a passive monitoring component and an active obfuscation component.
		- The monitoring component uses a background script to access the webRequest API to inspect all HTTP requests and responses as well as a content script to parse the DOM and extract innerHTML. Then the monitoring component sens this info to the obfuscation component.
	- Stealthiness
		- Expect the tracker to try to detect the usage of Harpo using purpose-built ML models. 
		- The author built a binary ML classifier to simulate the tracker solely for benchmark purpose.

## Untangling Header Bidding Lore: Some myths, some truths, and some hope
- MyadPrice
	- Privacy 
		- The extension sends no data from the user's browser, and uses the browser's local storage to store data pertaining to ad slots in different pages and the bids received for each.
	- Duration
		- Focus on the page-load time (PLT), and measure the time it takes for the browser to fire the onLoad event after the user navigates to the web page. Longer ad auctions negatively affect both publishers and advertisers.
		- in-browser measures the difference between the timestamps that Prebid records when it has prepared the bid request to be sent through the browser, and when it has finished parsing the bid response.
		- on-the-wire: the duration between the bid request and response as provided by the WPT API.
		- Bid duration steps breakdown:	
			- 1. The bid request is waiting in the browser's queue (Stall)
			- 2. DNS
			- 3. TCP handshake
			- 4. TLS handshake
			- 5. Wait for the first byte of the resposne since start of request (TTFB)
			- 6. Receive the rest of the response
- Solutions and contributions
	- Developed a new brower extension MyadPrice for Chrome and Firefox to observe in-browser auction process from the user's perspective.

## YourAdvalue: Measuring Advertising Price Dynamics without Bankrupting User Privacy
- YourAdvalue: a privacy-perserving tool for displaying to end-users in a simple and intuitive manner their advertising value as seen through RTB.
	- Alows end-users to learn in the real-time whiel browsing, how much money the programmatic advertising ecosystem pays to capture their attention byu rendering ads on their display.
	- Data gets first anonymized, and then feature aggregation is applied, prior to their transmission towards the database, which allows YourAdvalue to retrain its classifiers, and improve its accuracy on estimating the most up-to-date encrypted prices.
	- System design
		- User-related: 1. Simple to understand, 2. Unhampered user experience, 3. Preserve user anonymity
		- System-related: 1. Transparency, 2. Scalability, 3. Fault tolerance, 4. Privacy-by-design
		- Ad-related: 1. Real-time operation, 2. Generality of RTB detection, 3. Untampered RTB ad-protocol, 4. RTB price detection
	- User de-anonymization threats
		- 1. De-anonymization using users' online behavior or demographics
		- 2. De-anonymization using advertising-related activity
		- 3. De-anonymization using grouped records into user sessions
	- Inherent tradeoff between aggregation of feature classes, and modeling of prices at the server using ML methods.
- Results & Data
	- Desktop and mobile prices both grow significantly.
	- User demographics/exchanging data between advertisers and data brokers increases displayed ads.

## Real Time Bidding (RTB) Project - OpenRTB API Specification Version 2.5
- Outline
	- Required, recommended, and optional APIs
	- Trasport, Security, Data Format, Data Encoding
	- Bid Request & Bid Response: Object Model 
	- Enumerated Lists for all categories
	- Bid Request & Bid Response: Samples

![Screen Shot 2022-02-24 at 22 03 12](https://user-images.githubusercontent.com/37657480/155799055-2ec4cc3b-400b-408f-882c-f8bf658eab35.png)

## Charting App Developers’ Journey Through Privacy Regulation Features in Ad Networks
- Contributions
	- Information about privacy regulation is scattered in several pages buried under multiple layers, and uses terms and language developers do not understand. Ad networks should be responsible for ensuring compliance with regulations, so we suggest dedicating a section to privacy, offering easily accessible configurations, building testing systems for privacy regulations, and creating multimedia materials to promote privacy values in the Ad networks' documentation.
- Research questions
	- 1. How do Ad networks present information about privacy regulations in their documentation?
	- 2. How do developers find ad networks' support for complying with privacy regulations?
	- 3. How can Ad networks improve their privacy regulations support for developers?
	