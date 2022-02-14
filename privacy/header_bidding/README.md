# Header Bidding

## Inferring Tracker-Advertiser Relationships in the Online Advertising Ecosystem using Header Bidding
- Challenge
	- Different entities in online advertising and tracking ecosystems are incentivized to share information with each other through client-side or server-side mechanisms. 
	- Inferring data sharing between  entities on the server-side is hard.
- KASHF: infer data sharing relationships between advertisers and trackers by studying how an advertiser's bidding behavior changes as we manipulate the presence of trackers.
	- Relies on: advertisers with knowledge of a user's browsing history will bid differently (potentially higher) than an advertiser having no knowledge of a user's browsing history. 
- Contributions
	- Measuring bidding behavior of advertisers
	- Uncovering tracker-advertiser relationships
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