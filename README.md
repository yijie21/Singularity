# Singularity Tutorial

## Installation

Follow the steps in [link](https://docs.sylabs.io/guides/latest/user-guide/quick_start.html).



## Load datasets into A Singularity

**Using the Directory Overlay introduced in [link](https://docs.sylabs.io/guides/latest/user-guide/persistent_overlays.html)**

1. Create a directory:

   ```bash
   $ mkdir my_overlay
   ```

2. Create two SIFs and let them access to the same overlay

   ```bash
   $ sudo singularity build testOverlay1.sif testOverlay.def
   $ sudo singularity build testOverlay2.sif testOverlay.def
   ```

   where the def is defined below:

   ```bash
   Bootstrap: docker
   From: Ubuntu
   
   %post
   ```

3. Create a file in the overlay to let two SIFs read it (This is a simple example for storing a dataset in the overlay and let two SIFs access the dataset.)

   ```bash
   $ echo "This is a text file." > my_overlay/data.txt
   
   # test for testOverlay1.sif
   $ sudo singularity shell --overlay my_overlay/ testOverlay1.sif
   $ Singularity> cat my_overlay/data.txt
   $ This is some data.
   
   # test for testOverlay2.sif
   $ sudo singularity shell --overlay my_overlay/ testOverlay2.sif
   $ Singularity> cat my_overlay/data.txt
   $ This is some data.
   ```
   
   

​	

