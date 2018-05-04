---
published: false
---
Before continuing the install I needed to benchmark the IOPS to ensure my server would meet the production level requirements and be an asset to the network and not a hindrance.  /u/pepperew directed me to this site to help use as a guide for benchmarking: [https://dzone.com/articles/iops-benchmarking-disk-io-aws-vs-digitalocean](https://dzone.com/articles/iops-benchmarking-disk-io-aws-vs-digitalocean)
**TLDR; The SSD caching will meet the recommended requirements.
**
These are the commands I used with results:

### Random 75%read/write
	$ sudo fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=/mnt/test --bs=4k --iodepth=64 --size=4G --readwrite=randrw --rwmixread=75

### Random Read
	$ sudo fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=/mnt/test --bs=4k --iodepth=64 --size=4G --readwrite=randread

### Random Write
	$ sudo fio --randrepeat=1 --ioengine=libaio --direct=1 --gtod_reduce=1 --name=test --filename=/mnt/test --bs=4k --iodepth=64 --size=4G --readwrite=randwrite

---------------------------------------

Optimum Fastpath Configuration

Virtual Drive Properties: 
Write Policy: Write Through
Read Policy: No Read Ahead
IO Policy: Direct IO
Disk Cache Policy: Disabled

Result: Random 75% read/write
Read IOPS: min=16768, max=22476, avg=20195.38
Write IOPS: min= 5734, max= 7448, avg=6748.40

Result: Random 80% read/write
Read IOPS: min=35534, max=40796, avg=38816.49
Write IOPS: min= 8844, max=10196, avg=9722.79

Results: Random Read
Read IOPS: min=64480, max=68952, avg=67638.30

Results: Random Write
Write IOPS: min=10616, max=41044, avg=26771.44

------------------------------------------------

Optimum CacheCade Configuration

Virtual Drive Properties: 
Write Policy: Write Back
Read Policy: No Read Ahead
IO Policy: Cached IO
Disk Cache Policy: Disabled

Result: Random 75% read/write
Read IOPS: min=25892, max=29168, avg=27434.96
Write IOPS: min= 8578, max= 9644, avg=9169.12

Results: Random Read
Read IOPS: min=65928, max=69678, avg=67413.52

Results: Random Write
Write IOPS: min= 7552, max=20945, avg=16563.93

--------------------------------

With the benchmarking showing the SSD caching will meet the recommended performance of a production node, it was time to install rippled.

### Next Section: OS Installation
### Previous Section: Hardware