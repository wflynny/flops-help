# FLOPS

In this context I take FLOPS to mean **FL**oating point **O**perations **P**er
**S**econd.  I am having difficulty computing and reconciling the FLOPS for
various types of computing infrastructure, including clusters, BOINC grids, and
personal PCs.  I think my problem is twofold:

1.  I am not sufficiently differentiating "real-world" from "theoretical" FLOPS
    and may be making some apples-to-oranges comparisons.

2.  I have trouble reconciling the ratios of "real-world" FLOPS and my perceived
    ratios of "real-world" throughput when comparing two machines.  Either my
    perception of throughput is way off (too high) or I am not taking into
    account the actual programs I intend to compare.

The machines I want to compare are the following:

1.  CB2RR:  HPC cluster

    -   Redhat Linux
    -   120 x Intel Xeon E5-2660v3
    -   20 x Intel Xeon E5-2640v3
    -   40 x NVIDIA GeForce GTX Titan X

2.  Temple University Grid (TUGRID):  BOINC Grid

    -   ~450 x Intel Core i7-4770
    -   ~90  x Intel Core i7-4770S
    -   ~70  x Intel Core i7-6700
    -   ~120 x Intel Core i7-2600
    -   ~110 x Intel Core i5-3570
    -   ~90  x Intel Core i5-2400
    -   ~20  x Intel Core i5-2500

3.  IBM's World Community Grid (WCG):  BOINC Grid

    -   ~57,000 active memebers
    -   ~570,000 active devices
    -   Reported 1,100 TFLOPS actual as of [here][sekerob]

4.  Owl's Nest (OWLSNEST):  HPC Cluster

    -   144 x Intel Xeon x5660
    -   16 x Intel Xeon E5630
    -   32 x NVIDIA Tesla C2050

## Theoretical FLOPS

To compute theoretical FLOPS, the [formula][formula] is:

    FLOPS / CPU = (clock speed) x cores x (floating point operations)/cycle

I found most of the FLOPs/cycle numbers for each architecture
[here][flops-per-arch].

This is also complicated by the fact that computations for single floating point
(SP) and double floating point (DP) will naturally give different results (SP >
DP for CPUs and SP >> DP for GPUs), so I will need to be extra careful to state
SP or DP for my calculations.

### Double floating point Precision
1.  CB2RR
    -   [Xeon E5-2660v3][e5-2600v3]

            2.6(3.3)GHz, 10(20) cores
            Microarchitecture: Haswell-EP
            DP FLOPS = 2.6GHz * 10 cores * (16 OP/cycle) = 416.0 GLOPS / CPU
            DP FLOPS = 3.3GHz * 10 cores * (16 OP/cycle) = 528.0 GLOPS / CPU

    -   [Xeon E5-2640v3][e5-2600v3]

            2.6(3.4)GHz, 8(16) cores
            Microarchitecture: Haswell-EP
            DP FLOPS = 2.6GHz * 8 cores * (16 OP/cycle) = 332.8 GLOPS / CPU
            DP FLOPS = 3.4GHz * 8 cores * (16 OP/cycle) = 435.2 GLOPS / CPU

    Total CPU:

        120 x 416 + 20 x 332.8 = 56576 GFLOPs = 56.6 TFLOPS
        120 x 528 + 20 x 435.2 = 72064 GFLOPs = 72.1 TFLOPS

2.  OWLSNEST

    -   [Xeon x5660][x5660]

            2.8(3.2)GHz, 6(12) cores
            Microarchitecture: Westmere-EP (Gulftown)
            DP FLOPS = 2.8GHz * 6 cores * (4 OP/cycle) = 67.2 GLOPS / CPU
            DP FLOPS = 3.2GHz * 6 cores * (4 OP/cycle) = 76.8 GLOPS / CPU

    -   [Xeon E5-5630][e5630]

            2.53(2.8)GHz, 4(8) cores
            Microarchitecture: Westmere-EP (Gulftown)
            DP FLOPS = 2.53 * 4 * (4 OP/cycle) = 40.5 GFLOPS / CPU
            DP FLOPS = 2.8 * 4 * (4 OP/cycle) =  44.8 GFLOPS / CPU

    Total CPU:

        144 x 67.2 + 16 * 40.5 = 10325 GFLOPs = 10.3 TFLOPS
        144 x 76.8 + 16 * 44.8 = 11776 GFLOPs = 11.8 TFLOPS

3.  TUGRID

    -   [Core i7-4770][haswell]

            3.4(3.9)GHz, 4(8) cores
            Microarchitecture: Haswell-DT
            DP FLOPS = 3.4GHz * 4 cores * ( 16 OP/cycle) = 217.6 GFLOPS / CPU
            DP FLOPS = 3.9GHz * 4 cores * ( 16 OP/cycle) = 249.6 GFLOPS / CPU

    -   [Core i7-4770S][haswell]

            3.1(3.9)GHz, 4(8) cores
            Microarchitecture: Haswell-DT
            DP FLOPS = 3.1GHz * 4 cores * ( 16 OP/cycle) = 198.4 GFLOPS / CPU
            DP FLOPS = 3.9GHz * 4 cores * ( 16 OP/cycle) = 249.6 GFLOPS / CPU

    -   [Core i7-6700][skylake]

            3.4(4.0)GHz, 4(8) cores
            Microarchitecture: Skylake
            DP FLOPS = 3.4GHz * 4 cores * ( 16 OP/cycle) = 217.6 GFLOPS / CPU
            DP FLOPS = 4.0GHz * 4 cores * ( 16 OP/cycle) = 256.0 GFLOPS / CPU

    -   [Core i7-2600][sandybridge]

            3.4(3.8)GHz, 4(8) cores
            Microarchitecture: Sandy Bridge
            DP FLOPS = 3.4GHz * 4 cores * ( 8 OP/cycle) = 108.8 GFLOPS / CPU
            DP FLOPS = 3.8GHz * 4 cores * ( 8 OP/cycle) = 121.6 GFLOPS / CPU

    -   [Core i5-3570][ivybridge]

            3.4(3.8)GHz, 4(4) cores
            Microarchitecture: Ivy Bridge
            DP FLOPS = 3.4GHz * 4 cores * ( 8 OP/cycle) = 108.8 GFLOPS / CPU
            DP FLOPS = 3.8GHz * 4 cores * ( 8 OP/cycle) = 121.6 GFLOPS / CPU

    -   [Core i5-2400][sandybridge]

            3.1(3.4)GHz, 4(4) cores
            Microarchitecture: Sandy Bridge
            DP FLOPS = 3.1GHz * 4 cores * ( 8 OP/cycle) =  99.2 GFLOPS / CPU
            DP FLOPS = 3.4GHz * 4 cores * ( 8 OP/cycle) = 108.8 GFLOPS / CPU

    -   [Core i5-2500][sandybridge]

            3.3(3.7)GHz, 4(4) cores
            Microarchitecture: Sandy Bridge
            DP FLOPS = 3.3GHz * 4 cores * ( 8 OP/cycle) = 105.6 GFLOPS / CPU
            DP FLOPS = 3.7GHz * 4 cores * ( 8 OP/cycle) = 118.4 GFLOPS / CPU

    Total CPU:

        450 x 217.6 +
        90  x 198.4 +
        70  x 217.6 +
        120 x 108.8 +
        110 x 108.8 +
        90  x  99.2 +
        20  x 105.6 = 167072 GFLOPS = 167.1 TFLOPS

        450 x 249.6 +
        90  x 249.6 +
        70  x 256.0 +
        120 x 121.6 +
        110 x 121.6 +
        90  x 108.8 +
        20  x 118.4 = 192832 GFLOPS = 192.8 TFLOPS

    Multiply these by 0.75 since we only ever use 3/4 or 6/8 cores per machine:

        125304 - 144624 GFLOPS = 125.3 - 144.6 TFLOPs

4.  WCG

    I'm honestly not sure how I can compute this.


### Single Precision
Single floating point FLOPS will double the DP FLOPS for all these
architectures (SandyBridge/IvyBridge/Westmere, Haswell/Broadwell/Skylake).

## Actual FLOPS

Real performance will never reach theoretical because that assume perfect
parallelization.  Excluding [unrealistic codes designed to hit peak
performance][perfect-parallel], we want a measure of how well each CPU will
perform across several scientific applications.  I took 5 sources
[1][asteroids],[2][seti],[3]lhc],[4][cosmology],[5][mindmodeling] for my CPUs and
took some averages.  Not that for the Xeons, I have only 2, 3, 4, 2 data points
for the 2660v3, 2640v3, x5660, 5630, respectively while the desktop CPUs have 5
data points each.

1.  CB2RR

    Total CPU:

        120 x 81 + 20 x 71 = 11140 GFLOPs = 11.1 TFLOPS

2.  OWLSNEST

    Total CPU:

        144 x 49.2 + 16 * 26.4 = 7507 GFLOPs = 7.5 TFLOPS

3.  TUGRID

        450 x 31.7 +
        90  x 32.8 +
        70  x 32.0 +
        120 x 31.1 +
        110 x 16.0 +
        90  x 15.4 +
        20  x 15.3 = 26641 GFLOPS = 26.6 TFLOPS

    Multiply this by 0.75 and we get:

        19981 GFLOPs = 20 TFLOPS

4.  WCG

    I think I have to take [their word][sekerob] for it:

        1100 TFLOPS

## GPUs

Recent commodity GPUs have managed to dramatically increase single floating
point FLOPS at the cost of double floating point FLOPS (with the recent GeForce
900 series and 10 series having DP FLOPS = 1/32 SP FLOPS).  Their Tesla
counterparts have also taken a similar path, with the Kepler series have DP =
1/4 SP but the newer Maxwell and Pascal series have DP = 1/32 SP.  Therefore,
for newer GPUs it only makes sense to compare SP FLOPS since that is what they
are designed for.

GPU FLOPS are [calculated as][gpuflops]:

    SP FLOPS = (clock speed) x (CUDA cores) x (2 OPS/core)

-   GeForce GTX Titan X

        3072 CUDA cores
        1000(1177)MHz clock speed
        6.1-7.2 TFLOPS

-   C2050

        448 CUDA cores
        1150MHz clock speed
        1 TFLOPS

-   K80

        4992 CUDA cores
        560(875)MHz clock speed
        5.6-8.7 TFLOPS

Therefore, the theoretical performances of the resources are:

-   CB2RR

        40 x 6.1 = 244 TFLOPS

-   OWLSNEST

        16 x 1 = 16 TFLOPS

-   CB2HPC (for fun)

        4 x 5.6 = 22.4 TFLOPS

while this seems like a lot, this is maximum theoretical single precision.
Compare with the double the maximum theoretical DP CPU precision from above
(CB2RR - 144 SP CPU TFLOPS and 244 SP GPU TFLOPS).


[formula]: https://en.wikipedia.org/wiki/FLOPS#Computing
[flops-per-arch]: http://stackoverflow.com/a/15657772/1634191
[sekerob]: http://s137.photobucket.com/user/Sekerob/media/Daily/WCGQuickLook.png.html?791
[x5660]: http://download.intel.com/support/processors/xeon/sb/xeon_5600.pdf
[e5630]: http://download.intel.com/support/processors/xeon/sb/xeon_5600.pdf
[e5-2600v3]: http://repnop.org/pd/slides/PD_Haswell_Architecture.pdf
[haswell]: https://en.wikipedia.org/wiki/Haswell_(microarchitecture)#List_of_Haswell_processors
[skylake]: https://en.wikipedia.org/wiki/Skylake_(microarchitecture)#Desktop_processors
[ivybridge]: https://en.wikipedia.org/wiki/Ivy_Bridge_(microarchitecture)#Desktop_processors
[sandybridge]: https://en.wikipedia.org/wiki/Sandy_Bridge#Desktop_platform
[perfect-parallel]: http://stackoverflow.com/questions/8389648/how-do-i-achieve-the-theoretical-maximum-of-4-flops-per-cycle
[asteroids]: http://asteroidsathome.net
[seti]: http://setiathome.berkeley.edu
[lhc]: http://lhcathomeclassic.cern.ch
[cosmology]: http://www.cosmologyathome.org
[mindmodeling]: http://mindmodeling.org
[gpuflops]: https://en.wikipedia.org/wiki/Pascal_(microarchitecture)#Performance
