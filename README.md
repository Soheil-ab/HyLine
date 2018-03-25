# HyLine

Here you can find the ns-2 patch including HyLine, pFabric, and DCTCP. To use this patch, you need to first install ns2.34 using the provided instructions. Next, you can patch it and have mentioned schemes. There are also scripts (located in eval.tar.gz) for running the experiments.

## Install Ns-2.34

Download ns-2.34 from https://sourceforge.net/projects/nsnam/files/allinone/ns-allinone-2.34/ns-allinone-2.34.tar.gz/download
NS2 2.34 does not natively build on Ubuntu based systems. Use ns-allinone-2.34.ubuntu.patch (Provided by Qjump's authors) to make it work on Ubuntu.
Now build and install it.

	sudo apt-get update 
	sudo apt-get install build-essential autoconf automake libxmu-dev xorg-dev g++ xgraph 
	tar -xvf ns-allinone-2.34.tar.gz 
	cd ns-allinone-2.43 
	patch -p1 < ../ns-allinone-2.34.ubuntu.patch 
	./install 

When finished, follow the instructions and Setup your path variables. Test it by running this command: ns
If everything goes well, you should see `%`

## Apply DCTCP-Pfabric-HyLine

	cd ~/ns-allinone-2.43
	patch -p1 hyline.patch
	cd ns-2.34;
	./configure
	make clean
	make

## To Run Experiments: 
Download eval.tar.gz file and:

	cd ~;
	tar -xzf eval.tar.gz

## run the experiments

Here, it is important to extract files to the location above, scripts expect tcl files being in proper folders, If you want to change the location, you should simply modify scripts and point to the new location.

You can also have different instances of simulations, though you need enough amount of RAM and enough number of CPUs.
for 40000 # of flows, each experiment roughly utilizes 1.5GB of RAM and one CPU core.

Here are a few examples for load=0.5:

	cd ~/eval/hyline/;
	./hyline.sh 40000 1000000 1 50 1 0.5 Topology-mul-pland8-pfc.tcl &

	cd ~/eval/pfabric/;
	./pfabric.sh 40000 50 0.5 Topology-mul-pland8-pfc.tcl &

	cd ~/eval/dctcp/;
	./dctcp.sh 40000 0.5 Topology-mul-pland8-pfc.tcl &

	cd ~/eval/tcp/;
	./tcp.sh 40000 0.5 Topology-mul-pland8-pfc.tcl &

