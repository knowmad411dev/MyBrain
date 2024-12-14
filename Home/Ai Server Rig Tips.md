---
tags:
- - home
video-url: https://www.youtube.com/watch?v=_xL9r0ygISg&list=WL&index=2
---

## **Ai Server Rig Tips

-   [GPU Server for Ai](https://digitalspaceport.com/category/homelab-tutorials/gpu-server-for-ai/), [Homelab Tutorials](https://digitalspaceport.com/category/homelab-tutorials/), [Storage Server](https://digitalspaceport.com/category/homelab-tutorials/storage-server/)

_When you click on links to various merchants on this site and make a purchase, this can result in this site earning a commission. Affiliate programs and affiliations include, but are not limited to, the eBay Partner Network. As an Amazon Associate I earn from qualifying purchases. #ad #promotions_

![](https://digitalspaceport.com/wp-content/uploads/2024/11/ai-hardware-tips-tricks-takeaways-1024x576.png)

It has been around three months since I built a dedicated Ai server and I have learned a lot in this time. This rig houses a quad 3090 GPU setup on an AMD Epyc Rome motherboard and CPU. We have conducted while isolating to 1 variable several tests over a variety of base motherboard and CPU, ram speed, gpu, pcie width and generation, and models fitting to certain workloads and use cases. Here are the current findings based off my stacks of notes broken down into hardware categories. I hope these tips and tricks and lessons learned can be of assistance to you. Classes of Ai Rigs (I consider a rig a dedicated, likely always on, ai focused or supporting system)    

#### Super Budget AI Rig

###### OEM Tower, 2x K2200s, 8GB VRAM, 1 NVMe, 16GB RAM. Idle ~25w

Run a 7b, multiple 1/3/7

**Under $150**

Dell Optiplex 7050 MT [https://geni.us/OptiPlex7050MT](https://geni.us/OptiPlex7050MT) 

Quadro K2200 GPU [https://geni.us/K2200\_GPU](https://geni.us/K2200_GPU)

\*\*\*\*\*\*\*\*\*\*\*\*\*\*

#### Budget AI Rig 

###### OEM WS or tower, 3060 12 GB VRAM, 1 NVMe + 1 SSD, 32GB RAM. Idle ~30w

Run an 11b Vision, multiple 1/3/7/8

**Under $350**

Dell Precision 3620 Tower [https://geni.us/Precision\_3620](https://geni.us/Precision_3620) 

3060 12GB GPU [https://geni.us/3060\_GPU\_12GB](https://geni.us/3060_GPU_12GB) 

GPU 6 to 8 pin Power Adapter [https://geni.us/GPUPowerAdapt6pin-8pin](https://geni.us/GPUPowerAdapt6pin-8pin)

\*\*\*\*\*\*\*\*\*\*\*\*\*\*

#### Mid AI Rig 

###### WS or DIY Desktop, 3090 24GB or 3x 3060 12GB, 2x SSDs or NVMEs, 32-64GB RAM, Idle ~40w

Runs some 32b at q4, multiple 1/3/7/8/11

**Under $1000**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*

#### High End AI Rig 

###### High end consumer, EPYC or TRpro, RACK, 2x 3090 24GB GPUs + 3060 12GB, Mirror NVMe drives for boot and for storage, 64-128GB RAM, Idle ~ 65w

Runs 72b + 1/3/7b at q4, multiple 1/3/7/8/22/32s. Training +

**Under $2500**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

#### Insane AI Rig

###### Quad 3090 96, EPYC or TRpro, RACK, 4x 3090 24GB GPUs, U.2 storage, Mirror boot nvme, 256GB RAM, Idle ~ 90w

Runs 123 at q4, multiple 1/3/7/8/22/32/72/90s. Training +

**Under $5000**

GPU Rack Frame [https://geni.us/GPU\_Rack\_Frame](https://geni.us/GPU_Rack_Frame)

Gigabyte MZ32-AR0 Motherboard [https://geni.us/mz32-ar0\_motherboard](https://geni.us/mz32-ar0_motherboard)

RTX 3090 24GB GPU (x4) [https://geni.us/GPU3090](https://geni.us/GPU3090)

Kritical Thermal GPU Pads [https://geni.us/Kritical-Thermal-Pads](https://geni.us/Kritical-Thermal-Pads)

256GB (8x32GB) DDR4 2400 RAM [https://geni.us/256GB\_DDR4\_RAM](https://geni.us/256GB_DDR4_RAM)

PCIe4 Risers (x4) [https://geni.us/PCIe4\_Riser\_Cable](https://geni.us/PCIe4_Riser_Cable)

AMD EPYC 7702p [https://geni.us/EPYC\_7702p](https://geni.us/EPYC_7702p)

iCUE H170i ELITE CAPELLIX [https://geni.us/iCUE\_H170i\_Capellix](https://geni.us/iCUE_H170i_Capellix) (sTRX4 fits SP3 and retention kit comes with the CAPELLIX)

ARCTIC MX4 Thermal Paste [https://geni.us/Arctic\_ThermalPaste](https://geni.us/Arctic_ThermalPaste)

CORSAIR HX1500i PSU [https://geni.us/Corsair\_HX1500iPSU](https://geni.us/Corsair_HX1500iPSU)

4i SFF-8654 to 4i SFF-8654 (x4) [https://geni.us/SFF8654\_to\_SFF8654](https://geni.us/SFF8654_to_SFF8654)

HDD Rack Screws for Fans [https://geni.us/HDD\_RackScrews](https://geni.us/HDD_RackScrews)

#### \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Really Insane AI Rig 

###### 8x GPUs, EPYC or TRpro, RACK, 8x 3090 24GB GPUs, Mirror NVMe drives for boot U.2, 256GB RAM, Idle ~ 180w (30 AMP)

Runs FP16s, 123 at q4, multiple 1/3/7/8/22/32/72/90s. Training +

**Under $10000**

#### GPUs

-   VRAM is everything! Get as much as possible into your system.
-   GPUs directly impact tokens/s and ability to run large models.
-   GPUs running Ollama use llama.cpp under the hood. 
-   CUDA 11 will not be supported by drivers and possibly SW developers for a lot longer. Pascal + to stay CUDA 12 compatible.
-   I still like the perf/$ for the 3090 for inference workloads.
-   You may NOT need to repaste/pad used GPUs. Even higher end ones.
-   P40s are something many folks like to get higher perf, but will drop tps. Be sure to get 3D printed air shroud. Cheap.
-   Maxwells do work currently. [K2200 is a Maxwell chip. Uber cheap.](https://geni.us/K2200_GPU)
-   Avoid 8GB GPUs, unless you have them already.
-   96GB VRAM Run 123B and smaller. 2 mains. Hoards of smaller accy LLMs.
-   High electric rate? Beware insane class machines do not idle as low as you would want. 
-   24GB VRAM supports a lot. 1 main and a 1-2 accy LLM.
-   48GB – 60GB VRAM Start running at higher precision. Fits 32Bs. 1/2 main class models and 1-2 accy. 1 main and many accy.
-   Training Workloads? You will benefit from ADA GPUs. 2x ish
-   Inference Workloads? You are unlikely to see a big difference per our testing. Not 2x ish.
-   On eBay you should check a seller’s history and reputation pretty well and know how they will handle returns based on reviews imho. Check return policy to see if they allow returns.

#### Rack, Frame and Case

-   Rackmount GPU specific servers are fairly expensive and loud. Deep racks, dedicated power, house modifications likely.
-   [Open GPU rack frame rigs](https://geni.us/GPU_Rack_Frame) are nice as they are easy to adjust and cool, you will need to provide a fans. 
-   You will HAVE TO modify the frame I can say so you should have a drill and some metal bits on hand.
-   Pay attention to MOBO size. Tapping new holes in the frame is hard, threading issues.
-   You DO NOT need to have water cooling. You can use deeper GPUs like 4090s easier this way.
-   No water cooler also means you have an extra support bracket to use for the GPUs.
-   [H12SSL-i](https://geni.us/MBD_H12SSL-I-O) no standoff tapping needed.
-   [MZ32-AR0](https://geni.us/mz32-ar0_motherboard) is deeper, you will have to tap 3 stands.
-   Need airflow over RAM sticks to keep them from throttling.
-   Open Frames are somewhat dangerous to kids/pets and the hardware itself is in danger. Locate accordingly.
-   In my setup, I need to fab a FH bracket support for my NIC.
-   Single PSU mounted, easy. Dual PSU mounted, little space.
-   GPU mounting screw spots by default are wide apart. Could modify to fit more cards if you have a box fan or vornado on it.

#### Motherboards/RAM

-   My [MZ32-AR0 BIOS v1](https://geni.us/mz32-ar0_motherboard) was able to be updated to V3. Just choose the oldest V3 after you max the V1 updates. Works with ROME CPUs.
-   [Threadripper Pro 5955WX](https://geni.us/ThreadripperPRO_5955wx) can be pretty cheap and I think the 3XXX may also support PCIe 4 gen slots. [WRX80 motherboards](https://geni.us/ASRock_wrx80_creator) can be cheap.
-   BMC / iKVM is a major quality of life need on workstation and server boards.
-   Avoid boards that support only up to 7001. Some can be flashed but should come flashed already.
-   RAM SPEED/GEN DOES NOT SEEM TO MATTER FOR INFERENCE

#### CPUs

-   Fast single thread DOES make a measured difference.
-   Intel idles better vs AMD.
-   Core count at or above 4 for a dedicated only Ai computer.
-   Core count above 16 for a multiuse home server setup, which makes more sense imo.
-   Really high core counts can run small models fairly decently at low b sizes.
-   You can run a 405b on a CPU/RAM of 256GB but it’s slow. Even on a [7995WX](https://geni.us/AMD_TR_PRO_7995WX).

<iframe frameborder="0" allowfullscreen="" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" title="Ai Server Hardware Tips, Tricks and Takeaways - Watch before you SHOP BF/CM" width="640" height="360" src="https://www.youtube.com/embed/_xL9r0ygISg?controls=1&amp;rel=0&amp;playsinline=0&amp;modestbranding=0&amp;autoplay=0&amp;enablejsapi=1&amp;origin=https%3A%2F%2Fdigitalspaceport.com&amp;widgetid=1" id="widget2"></iframe>

[![Picture of DSP](https://digitalspaceport.com/wp-content/uploads/2021/12/headshot-no-bg.png)](https://digitalspaceport.com/author/dsp/)

#### Table of Contents

<iframe title="Latest Videos" src="https://www.youtube.com/embed/videoseries?list=PLarJAzZsWRGBK1s6OgXgT2bI3wMhXSRqF" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen=""></iframe>

When you click on links to various merchants on this site and make a purchase, this can result in this site earning a commission. Affiliate programs and affiliations include, but are not limited to, the eBay Partner Network.

As an Amazon Associate I earn from qualifying purchases.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut elit tellus, luctus nec ullamcorper mattis, pulvinar dapibus leo.

[[ML Hardware]]