CONCLUSION:   
   
SHORT:   
The performance related advantage of large page usage for randomly accessed data   
in a big address range is significant, and i think it would be generally worth a    
better implementation at operating system level.   
   
DETAILED:      
On current windows operating systems, the availability of unfragmented    
continous large page blocks decreases over time.   

There is a relation between, type and ammount of processes running on a system   
and fragmentation progress.   
   
This fragmentation, is generally irreversible and windows doesn't directly support   
any defragmentation mechanism for physical RAM, currently.   
   
To ensure a 100% availabilty of unfragmented physical RAM, the most effective approach would be    
to allocate this RAM at system start, with the consequence, that this memory is no longer
available for other applications.   
   
If enough memory is available, a good implementation could be a preallocation via creation    
of a big large page section object and later mappings in process address space.   
    
   
This little research project is closet for now, maybe i will continue it later,    
if i find the time and new motivation.    
   
   
Thanks for your attention,
Fred41 :)   
   
   

=======================================================================================================


... this is an **experimental** replacement for armas default **custom memory allocator** ...

This custom memory allocator is based on **intel tbb malloc 4.2, updt. 2** and should work with arma server and client.

You can find the source code of intels tbb 4.2, updt. 2 here:

[https://www.threadingbuildingblocks.org/sites/default/files/software_releases/source/tbb42_20131118oss_src.tgz](https://www.threadingbuildingblocks.org/sites/default/files/software_releases/source/tbb42_20131118oss_src.tgz)

and some general infos about custom memory allocator for arma and the BIS interface description can be found here:

[http://community.bistudio.com/wiki/ArmA_2:_Custom_Memory_Allocator](http://community.bistudio.com/wiki/ArmA_2:_Custom_Memory_Allocator)

This project is covered by the same license as provided with the source code from intel (GPL 2.0).

Some small optimizations in the interface, a little workaround, adaption of some internal parameters and the fact,    
that this allocator allocates memory regions in **large pages** (2048kB), instead of **small pages** (4kB) results in better performance,
compared with the default allocator tbb4malloc_bi.dll.   
    
This allocator works best/only on 64 bit OS, with at least 8GB RAM.    
    
    
HOW TO USE:    
    
Copy **tbbmalloc.dll** in your arma3/dll directory.    
append **-malloc=tbbmalloc** to your arma 3 start line.    
    
**tbbmalloc** prefers to use RAM in **large pages** (2048kB instead of 4kB).    
    
The use of large pages requires the **lock pages in memory privilege** for the arma user.    
    
Make sure your arma user account has this privilege set in your **local security policies** settings (secpol.msc, restart required).     
If your useraccount, which you use to start arma, is member of the **administrator group**, you have to start arma **as administrator**!   
    
On client, i measured between 6-9% higher framerates with "Helos A3-bench". 
I noticed significant smoother gameplay (higher and more stable framerates).
On server i have no benchmark, but it will accelerate here too, dependend on mission and server load.   

This allocator logs some timing data to **malloc_PIDX.log**.
The tbbmalloc logfile looks like in this example:

	WindowsVersion: 6.1  ServicePack: 1.0  Typ: Desktop

	process virt. address available:  3840
	system physical RAM total:       16351
	system physical RAM available:   12746
	system committed limit:          40875
	system committed peak:            6720
	system committed current:         3612
	system cache current:             2907
	system handles:                   9592
	system processes:                   43
	system threads:                    503

	system uptime minutes:              50

	SeLockMemoryPrivilege: granted, huge pages enabled

	   0.015s:   0.18ms     2048k at:0xffc00000 Alloc LP (   2M)
	   0.015s:   0.00ms      128k at:0x00230000 Alloc SP (   2M)
	   0.031s:   0.43ms     8192k at:0xff400000 Alloc LP (  10M)
	   0.686s:   0.25ms     4096k at:0xff000000 Alloc LP (  14M)
	   0.686s:   0.22ms     4096k at:0xfec00000 Alloc LP (  18M)
	   0.686s:   0.21ms     4096k at:0xfe800000 Alloc LP (  22M)
	   0.686s:   0.25ms     4096k at:0xfe400000 Alloc LP (  26M)
	   0.967s:   0.32ms     4096k at:0xfe000000 Alloc LP (  30M)
	   0.967s:   0.30ms     4096k at:0xfdc00000 Alloc LP (  34M)
	   0.967s:   0.26ms     4096k at:0xfd800000 Alloc LP (  38M)
	   .....


The line with **SeLockMemoryPrivilege** for example tells you, that the required privileg is set correctly.     
(Alloc LP means large pages are allocated, SP means small pages)



IMPORTANT:   
The goal of this little research project, is to verify the performance gain by using large pages for memory allocations and some other optimizations.
   
So this project will not provide a permanent replacement for the default memory allocator. 
Instead the results will be provided to BIS and hopefully help to improve the default memory allocator as part of the arma distribution.



Greets,
Fred41
