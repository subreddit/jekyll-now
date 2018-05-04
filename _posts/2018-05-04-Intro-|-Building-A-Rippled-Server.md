---
published: true
---
Like many others who own XRP tokens I too am a fan of Ripple.  Using blockchain to send money globally in a fast and secure manner is not a new concept.  Ripple's use cases for xCurrent, xRapid, and xVia, have the potential to be the future of financial transactions.  What makes Ripple standout to me is their take on using blockchain in the enterprise and with the banking industry.  

How can I get involved, learn more, and look for an opportunity to add value?

My reasons for setting up rippled are: further expand decentralization, self-education through experience, to provide accessible walk-through documentation, and on behalf of the community at /r/Ripple.  

After following /r/Ripple for several months I noticed occasional interest in running rippled only to see disappointment after realizing the costs involved.

The largest cost barrier in a production node is the amount of storage required (6.8 TB as of 2018-03-01 **†** ) for the ledger history, combined with SSD storage to support the read/write IOPS (10k reads/7k writes **††** ).  In my tutorial I leverage SSD caching on the RAID controller to reduce the cost of storage while maintaining the required storage space and recommended read/write IOPS.  

This rippled guide consists of the following sections:

- [Intro](https://subreddit.github.io/Intro-Building-A-Rippled-Server/)
- Hardware
- Benchmarking
- OS Installation
- Installing MSM or MegaCLI
- Rippled Installation


### Next Section: Hardware


Sources: 
- † "At the time of writing (2018-03-01), a server with all XRP Ledger history requires 6.8TB."
- †† "The maximum reads and writes per second that Ripple engineers have observed are over 10,000 reads per second (in heavily-used public server clusters), and over 7,000 writes per second (in dedicated performance testing)." https://ripple.com/build/rippled-setup/#recommendation-1
