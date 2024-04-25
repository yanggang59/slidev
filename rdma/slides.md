---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# apply any unocss classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
transition: slide-left
title: RDMA Introduction
mdc: true
---

# RDMA Introduction

Thomas Young

2024/04/24

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Go <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: default
---

# Table of contents


<Toc maxDepth="1"></Toc>

---
transition: slide-up
level: 2
---



# Socket API

<div grid="~ cols-2 gap-4">
<div>

Description:
- 🛠 **Server starts first, wait for client connetcion**
- 🛠 **Client connect to server, then send and receive msg from each other**


<br>


</div>
<div>

<img src="imgs/socket_test.png"/>

</div>
</div>

---
class: px-20
---

# Socket-Arch

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **System Calls** - Data transfer has to use system call 
- 📤 **Protocol Stack** - CPU has to deal with protocol stack




</div>
<div>
<img src="imgs/socket_arch.png"/>

</div>
</div>

---
class: px-20
---

# Socket-Dataflow

<div grid="~ cols-2 gap-4">
<div>

Descrition:
- 📤 **System Calls** -  Latency shall be high
- 📤 **Memory Copy** - data has to be copied from user space to kernel space
- 📤 **Protocol Stack** - CPU has to cope with protocal stack


</div>
<div>

<img src="imgs/socket_dataflow.png"/>

</div>
</div>

---
class: px-20
---

# RDMA Arch

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **Control Path** - Initialize and build connection
- 📤 **Data Path** - Data transfer between two nodes




</div>
<div>
<img src="imgs/rdma_arch.png"/>

</div>
</div>

---
class: px-20
---

# RDMA-Dataflow

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **System Calls** - Data transfer don't have to use syscalls
- 📤 **Protocol Stack** - CPU doesn't deal with protocol stack
- 📤 **Memory Copy** - No memory copy between user space and kernel space

RDMA Driver must have the ability of 

(1) Accessing data in phsycal uncontiguous address of user space

(2) packing and unpacking data

</div>
<div>
<img src="imgs/rdma_dataflow.png"/>

</div>
</div>

---
class: px-20
---

# RDMA Software Architecture

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **rdma-core** - Data transfer don't have to use syscalls
- 📤 **rdma kernel driver** - CPU doesn't deal with protocol stack



</div>
<div>
<img src="imgs/rdma_soft_arch.png"/>

</div>
</div>

---
class: px-20
---

# RDMA Transfer Process
<div grid="~ rows-4">
<div>
<img src="imgs/rdma_trans_process.png"/>
</div>
<div>

Description:
- 📤 **cntrol-path** - Data transfer don't have to use syscalls
- 📤 **data-path** - CPU doesn't deal with protocol stack
</div>
</div>

---
class: px-20
---

# RDMA Elements - WQ & WQE

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **WQ** - Work Queue
- 📤 **WQE** - Work Queue Entry



</div>
<div>
<img src="imgs/rdma_wq.png"/>

</div>
</div>

---
class: px-20
---

# RDMA Elements - QP & QPN

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **QP** - Queue Pair: SQ + WQ
- 📤 **QPN** - Queue Pair Number 



</div>
<div>
<img src="imgs/rdma_qp.png"/>

</div>
</div>

---
class: px-20
---

# RDMA Elements - CQ & CQE

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **CQ** - Complete Queue
- 📤 **CQE** - Complete Queue Entry



</div>
<div>
<img src="imgs/rdma_cq.png"/>

</div>
</div>

---
class: px-20
---
# RDMA Write Process

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **Single Side Operation** - Only host side needs participate
- 📤 **RDMA Hardware** - Need to know how to transfer Virtual Address to Physical Address



</div>
<div>
<img src="imgs/rdma_write.png"/>

</div>
</div>

---
class: px-20
---

# RDMA Elements -MR - MTT
<div grid="~ rows-4">
<div>
<img src="imgs/rdma_mtt.png"/>
</div>
<div>

Description:
- 📤 **MR** - Memory Region
- 📤 **MTT** - Memory Transfer Table
</div>
</div>

---
class: px-20
---

# RDMA Elements -MR - Keys
<div grid="~ rows-4">
<div>
<img src="imgs/rdma_keys.png"/>
</div>
<div>

Description:
- 📤 **L_Key** - Local Key
- 📤 **R_Key** - Remote Key
</div>
</div>

---
class: px-20
---

# RDMA Elements - PD

<div grid="~ cols-2 gap-4">
<div>

Description:

(1) Node B access MR0 of Node A using QP5

(2) Node C access MR1 of Node A using QP5

(3) Node B can access MR1 when using R_Key of MR1

</div>
<div>
<img src="imgs/rdma_pd1.png"/>

</div>
</div>

---
class: px-20
---

# RDMA Elements - PD

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **PD** - Protection Domain



</div>
<div>
<img src="imgs/rdma_pd2.png"/>

</div>
</div>

---
class: px-20
---

# Our Design --- Soft Architecture

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **Compatibility** - Using rdma-core lib to be compatible with ibverbs sematics
- 📤 **User Space** - Specified implementation for our own products
- 📤 **Kernel Space** - RDMA driver to work with user libs


</div>
<div>
<img src="imgs/rdma_clussys_soft_arch.png"/>

</div>
</div>

---
class: px-20
---


# Our Design --- Logic Definition

<div grid="~ cols-2 gap-4">
<div>

Description:
- 📤 **Host RAM** - WQ Buffer, CQ Buffer, MTT

- 📤 **FPGA RAM** - QP Contex, CQ Contex, MR Contex

</div>
<div>
<img src="imgs/rdma_clussys_logic_def.png"/>

</div>
</div>

---
class: px-20
---

# Thanks for watching

<div grid="~ rows-1 gap-4">
<div>

## Reference

RDMA_Aware_Programming_usermanual_V1.7.pdf
《Advanced Programming in the UNIX Environment》
《Understanding Linux Network Internals》
https://www.kernel.org/doc/html/latest/networking/index.html



<br>
<br>
<br>


</div>

</div>