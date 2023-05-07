Download Link: https://assignmentchef.com/product/solved-eth263-2210-hw-5-parallelism-mutiprocessors-bottleneck-acceleration-prefetching
<br>
<h1>1.      Parallel Speedup</h1>

You are a programmer at a large corporation, and you have been asked to parallelize an old program so that it runs faster on modern multicore processors.

<ul>

 <li>You parallelize the program and discover that its speedup over the single-threaded version of the same program is significantly less than the number of processors. You find that many cache invalidations are occuring in each core’s data cache. What program behavior could be causing these invalidations (in 20 words or less)?</li>

 <li>You modify the program to fix this first performance issue. However, now you find that the program is slowed down by a global state update that must happen in only a single thread after every parallel computation. In particular, your program performs 90% of its work (measured as processor-seconds) in the parallel portion and 10% of its work in this serial portion. The parallel portion is perfectly parallelizable. What is the maximum speedup of the program if the multicore processor had an infinite number of cores?</li>

 <li>In order to execute your program with parallel and serial portions more efficiently, your corporation decides to design a custom heterogeneous processor.

  <ul>

   <li>This processor will have one large core (which executes code more quickly but also takes greater die area on-chip) and multiple small cores (which execute code more slowly but also consume less area), all sharing one processor die.</li>

   <li>When your program is in its parallel portion, all of its threads execute only on small cores.</li>

   <li>When your program is in its serial portion, the one active thread executes on the large core.</li>

   <li>Performance (execution speed) of a core is proportional to the square root of its area.</li>

   <li>Assume that there are 16 units of die area available. A small core must take 1 unit of die area. The large core may take any number of units of die area <em>n</em><sup>2</sup>, where <em>n </em>is a positive integer.</li>

   <li>Assume that any area not used by the large core will be filled with small cores.</li>

  </ul></li>

 <li>How large would you make the large core for the fastest possible execution of your program?</li>

 <li>What would the same program’s speedup be if all 16 units of die area were used to build ahomogeneous system with 16 small cores, the serial portion ran on one of the small cores, and the parallel portion ran on all 16 small cores?</li>

 <li>Does it make sense to use a heterogeneous system for this program which has 10% of its work inserial sections?</li>

</ul>

<ul>

 <li>Now you optimize the serial portion of your program and it becomes only 4% of total work (the parallel portion is the remaining 96%).

  <ul>

   <li>What is the best choice for the size of the large core in this case?</li>

   <li>What would the same program’s speedup be for this 4%/96% serial/parallel split if all 16 units ofdie area were used to build a homogeneous system with 16 small cores, the serial portion ran on one of the small cores, and the parallel portion ran on all 16 small cores?</li>

   <li>Does it make sense to use a heterogeneous system for this program which has 4% of its work inserial sections?</li>

  </ul></li>

</ul>

Why or why not?

<h1>2.      Asymmetric Multicore</h1>

A microprocessor manufacturer asks you to design an asymmetric multicore processor for modern workloads. You should optimize it assuming a workload with 80% of its work in the parallel portion. Your design contains one large core and several small cores, which share the same die. Assume the total die area is 32 units.

<ul>

 <li><em>Large core</em>: For a large core that is <em>n </em>times faster than a single small core, you will need <em>n</em><sup>3 </sup>units of die area (<em>n </em>is a positive integer). The dynamic power of this core is 6×<em>n </em>Watts and the static power is <em>n </em></li>

 <li><em>Small cores</em>: You will fit as many small cores as possible, after placing the large core. A small core occupies 1 unit of die area. Its dynamic power is 1 Watt and its static power is 0.5 Watts. The parallel portion executes <em>only </em>on the small cores, while the serial portion executes <em>only </em>on the large core.</li>

</ul>

Please answer the following questions. Show your work. Express your equations and solve them. You can approximate some computations, and get partial or full credit.

<ul>

 <li>What configuration (i.e., number of small cores and size of the large core) results in the best performance?</li>

 <li>The energy consumption should also be a metric of reference in your design. Compute the energy consumption for the best configuration in part (a).</li>

 <li>For the best configuration obtained in part (a), you are considering to use the large core to collaborate with the small cores on the execution of the parallel portion.

  <ul>

   <li>What is the overall performance improvement, compared to the performance obtained in part (a), if the large core collaborates on the parallel portion?</li>

   <li>What is the overall energy change, compared to the energy obtained in part (b), if the large core collaborates on the parallel portion?</li>

   <li>Discuss whether it is worth using the large core to collaborate with the small cores on the execution of the parallel portion.</li>

  </ul></li>

 <li>Now assume that the serial portion can be optimized, i.e., the serial portion becomes smaller. This gives you the possibility of reducing the size of the large core, and still improving performance. For a large core with an area of (<em>n</em>−1)<sup>3</sup>, where <em>n </em>is the value obtained in part (a), what should be the fraction of serial portion that would lead to better performance than in part (a)?</li>

 <li>Your design is so successful for desktop processors that the company wants to produce a similar design for mobile devices. The power budget becomes a constraint. For a maximum of total power of 20W, how much would you need to reduce the dynamic power consumption of the large core, if at all, for the best configuration obtained in part (a)? Assume again that the parallel fraction is 80% of the workload. (Hint: Express the dynamic power of the large core as <em>D</em>×<em>n </em>Watts, where <em>D </em>is a constant).</li>

</ul>

<h1>3.      Runahead Execution</h1>

Assume an in-order processor that employs Runahead execution, with the following specifications:

<ul>

 <li>The processor enters Runahead mode when there is a cache miss. There is no penalty for entering and leaving the Runahead mode.</li>

 <li>There is a 64KB data cache. The cache block size is 64 bytes.</li>

 <li>Assume that the instructions are fetched from a separate dedicated memory that has zero access latency, so an instruction fetch never stalls the pipeline.</li>

 <li>The cache is 4-way set associative and uses the LRU replacement policy.</li>

 <li>A memory request that hits in the cache is serviced instantaneously.</li>

 <li>A cache miss is serviced from the main memory after <em>X </em></li>

 <li>A cache block for the corresponding fetch is allocated <em>immediately </em>when a cache miss happens.</li>

 <li>The cache replacement policy does <em>not </em>evict the cache block that triggered entry into Runahead mode until after the Runahead mode is exited.</li>

 <li>The victim for cache eviction is picked at the same time a cache miss occurs, i.e., during cache block allocation.</li>

 <li>ALU instructions and Branch instructions take one cycle.</li>

 <li>Assume that the pipeline <em>never stalls </em>for reasons <em>other than data cache misses</em>. Assume that the conditional branches are always correctly predicted and the data dependencies do not cause stalls (except for data cache misses).</li>

</ul>

Consider the following program. Each element of Array A is one byte.

for (i = 0; i &lt; 100; i++) { \ 2 ALU instructions and 1 branch instruction

int m = A[i*16*1024] + 1; \ 1 memory instruction followed by 1 ALU instruction

…                                                                \ 26 ALU instructions

}

<ul>

 <li>After running this program using the processor specified above, you find that there are 66 data cache hits. What are all the possible values of the cache miss latency X? You can specify all possible values of X as an inequality. Show your work.</li>

 <li>Is it possible that <em>every </em>memory access in the program misses in the cache? If so, what are all possible values of X that will make all memory accesses in the program miss in the cache? If not, why? Show your work.</li>

 <li>What is the <em>minimum </em>number of cache misses that the processor can achieve by executing the above program? Show your work.</li>

</ul>

<h1>4.      Prefetching</h1>

An architect is designing the prefetch engine for his machine. He first runs two applications A and B on the machine, with a stride prefetcher. Application A:

uint8_t a[1000]; sum = 0; for (i = 0; i &lt; 1000; i += 4) { sum += a[i];

}

Application B:

uint8_t a[1000]; sum = 0; for (i = 1; i &lt; 1000; i *= 4) { sum += a[i];

}

i and sum are in registers, while the array a is in memory. A cache block is 4 bytes in size.

(a) What is the prefetch accuracy and coverage for applications A and B using a stride prefetcher. This stride prefetcher detects the stride between two consecutive memory accesses and prefetches the cache block at this stride distance from the currently accessed block.

<h1>5.      Cache Coherence</h1>

We have a system with 4 byte-addressable processors. Each processor has a private 256-byte, directmapped, write-back L1 cache with a block size of 64 bytes. Coherence is maintained using the Illinois Protocol (MESI), which sends an invalidation to other processors on writes, and the other processors invalidate the block in their caches if <em>the block is present </em>(NOTE: On a write hit in one cache, a cache block in Shared state becomes Modified in that cache).

Accessible memory addresses range from 0x50000000 − 0x5FFFFFFF. Assume that the offset within a cache block is 0 for all memory requests. We use a snoopy protocol with a shared bus.

Cosmic rays strike the MESI state storage in your coherence modules, causing the state of a <em>single </em>cache line to instantaneously change to another state. This change causes an inconsistent state in the system. We show below the initial tag store state of the four caches, <em>after </em>the inconsistent state is induced. Inital State

<table width="457">

 <tbody>

  <tr>

   <td colspan="3" width="206">Cache 0</td>

   <td rowspan="6" width="44"> </td>

   <td colspan="5" width="206">Cache 1</td>

  </tr>

  <tr>

   <td width="45"> </td>

   <td width="80"><em>Tag</em></td>

   <td width="81"><em>MESI state</em></td>

   <td width="45"> </td>

   <td colspan="2" width="80"><em>Tag</em></td>

   <td colspan="2" width="81"><em>MESI state</em></td>

  </tr>

  <tr>

   <td width="45"><em>Set 0</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">M</td>

   <td width="45"><em>Set 0</em></td>

   <td colspan="2" width="80">0x522222</td>

   <td colspan="2" width="81">I</td>

  </tr>

  <tr>

   <td width="45"><em>Set 1</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">E</td>

   <td width="45"><em>Set 1</em></td>

   <td colspan="2" width="80">0x510000</td>

   <td colspan="2" width="81">S</td>

  </tr>

  <tr>

   <td width="45"><em>Set 2</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">S</td>

   <td width="45"><em>Set 2</em></td>

   <td colspan="2" width="80">0x5FFFFF</td>

   <td colspan="2" width="81">S</td>

  </tr>

  <tr>

   <td width="45"><em>Set 3</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">I</td>

   <td width="45"><em>Set 3</em></td>

   <td colspan="2" width="80">0x533333</td>

   <td colspan="2" width="81">S</td>

  </tr>

  <tr>

   <td colspan="3" width="206">Cache 2</td>

   <td rowspan="6" width="44"> </td>

   <td colspan="4" width="204">Cache 3</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"> </td>

   <td width="80"><em>Tag</em></td>

   <td width="81"><em>MESI state</em></td>

   <td width="45"> </td>

   <td width="78"><em>Tag</em></td>

   <td colspan="2" width="81"><em>MESI state</em></td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"><em>Set 0</em></td>

   <td width="80">0x5F111F</td>

   <td width="81">M</td>

   <td width="45"><em>Set 0</em></td>

   <td width="78">0x5FF000</td>

   <td colspan="2" width="81">E</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"><em>Set 1</em></td>

   <td width="80">0x511100</td>

   <td width="81">E</td>

   <td width="45"><em>Set 1</em></td>

   <td width="78">0x511100</td>

   <td colspan="2" width="81">S</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"><em>Set 2</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">S</td>

   <td width="45"><em>Set 2</em></td>

   <td width="78">0x5FFFF0</td>

   <td colspan="2" width="81">I</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"><em>Set 3</em></td>

   <td width="80">0x533333</td>

   <td width="81">S</td>

   <td width="45"><em>Set 3</em></td>

   <td width="78">0x533333</td>

   <td colspan="2" width="81">I</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"></td>

   <td width="80"></td>

   <td width="81"></td>

   <td width="44"></td>

   <td width="45"></td>

   <td width="78"></td>

   <td width="2"></td>

   <td width="79"></td>

   <td width="2"></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>What is the inconsistency in the above initial state? Explain with reasoning.</li>

 <li>Consider that, after the initial state, there are several paths that the program can follow that access different memory instructions. In b.1 and b.2, we will examine whether the followed path can potentially lead to incorrect execution, i.e., an incorrect result.

  <ul>

   <li>Could the following path potentially lead to incorrect execution? Explain.</li>

  </ul></li>

</ul>

<table width="458">

 <tbody>

  <tr>

   <td width="46">order</td>

   <td width="108">Processor 0</td>

   <td width="108">Processor 1</td>

   <td width="98">Processor 2</td>

   <td width="98">Processor 3</td>

  </tr>

  <tr>

   <td width="46">1<em>st</em></td>

   <td width="108"> </td>

   <td width="108"> </td>

   <td width="98">ld 0x51110040</td>

   <td width="98"> </td>

  </tr>

  <tr>

   <td width="46">2<em>nd</em></td>

   <td width="108">st 0x5FFFFF40</td>

   <td width="108"> </td>

   <td width="98"> </td>

   <td width="98"> </td>

  </tr>

  <tr>

   <td width="46">3<em>rd</em></td>

   <td width="108"> </td>

   <td width="108"> </td>

   <td width="98"> </td>

   <td width="98">st 0x51110040</td>

  </tr>

  <tr>

   <td width="46">4<em>th</em></td>

   <td width="108"> </td>

   <td width="108">ld 0x5FFFFF80</td>

   <td width="98"> </td>

   <td width="98"> </td>

  </tr>

  <tr>

   <td width="46">5<em>th</em></td>

   <td width="108"> </td>

   <td width="108">ld 0x51110040</td>

   <td width="98"> </td>

   <td width="98"> </td>

  </tr>

  <tr>

   <td width="46">6<em>th</em></td>

   <td width="108"> </td>

   <td width="108">ld 0x5FFFFF40</td>

   <td width="98"> </td>

   <td width="98"> </td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Could the following path potentially lead to incorrect execution? Explain.</li>

</ul>

<table width="444">

 <tbody>

  <tr>

   <td width="46">order</td>

   <td width="108">Processor 0</td>

   <td width="93">Processor 1</td>

   <td width="98">Processor 2</td>

   <td width="98">Processor 3</td>

  </tr>

  <tr>

   <td width="46">1<em>st</em></td>

   <td width="108"> </td>

   <td width="93"> </td>

   <td width="98"> </td>

   <td width="98">ld 0x51110040</td>

  </tr>

  <tr>

   <td width="46">2<em>nd</em></td>

   <td width="108">ld 0x5FFFFF00</td>

   <td width="93"> </td>

   <td width="98"> </td>

   <td width="98"> </td>

  </tr>

  <tr>

   <td width="46">3<em>rd</em></td>

   <td width="108"> </td>

   <td width="93"> </td>

   <td width="98">ld 0x51234540</td>

   <td width="98"> </td>

  </tr>

  <tr>

   <td width="46">4<em>th</em></td>

   <td width="108">st 0x5FFFFF40</td>

   <td width="93"> </td>

   <td width="98"> </td>

   <td width="98"> </td>

  </tr>

  <tr>

   <td width="46">5<em>th</em></td>

   <td width="108"> </td>

   <td width="93"> </td>

   <td width="98"> </td>

   <td width="98">ld 0x51234540</td>

  </tr>

  <tr>

   <td width="46">6<em>th</em></td>

   <td width="108">ld 0x5FFFFF00</td>

   <td width="93"> </td>

   <td width="98"> </td>

   <td width="98"> </td>

  </tr>

 </tbody>

</table>

After some time executing a particular path (which could be a path <em>different </em>from the paths in parts b.1 and b.2) and with no further state changes caused by cosmic rays, we find that the final state of the caches is as follows.

Final State

<table width="457">

 <tbody>

  <tr>

   <td colspan="3" width="206">Cache 0</td>

   <td rowspan="6" width="44"> </td>

   <td colspan="5" width="206">Cache 1</td>

  </tr>

  <tr>

   <td width="45"> </td>

   <td width="80"><em>Tag</em></td>

   <td width="81"><em>MESI state</em></td>

   <td width="45"> </td>

   <td colspan="2" width="80"><em>Tag</em></td>

   <td colspan="2" width="81"><em>MESI state</em></td>

  </tr>

  <tr>

   <td width="45"><em>Set 0</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">M</td>

   <td width="45"><em>Set 0</em></td>

   <td colspan="2" width="80">0x5FF000</td>

   <td colspan="2" width="81">I</td>

  </tr>

  <tr>

   <td width="45"><em>Set 1</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">E</td>

   <td width="45"><em>Set 1</em></td>

   <td colspan="2" width="80">0x510000</td>

   <td colspan="2" width="81">S</td>

  </tr>

  <tr>

   <td width="45"><em>Set 2</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">S</td>

   <td width="45"><em>Set 2</em></td>

   <td colspan="2" width="80">0x5FFFFF</td>

   <td colspan="2" width="81">S</td>

  </tr>

  <tr>

   <td width="45"><em>Set 3</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">E</td>

   <td width="45"><em>Set 3</em></td>

   <td colspan="2" width="80">0x533333</td>

   <td colspan="2" width="81">I</td>

  </tr>

  <tr>

   <td colspan="3" width="206">Cache 2</td>

   <td rowspan="6" width="44"> </td>

   <td colspan="4" width="204">Cache 3</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"> </td>

   <td width="80"><em>Tag</em></td>

   <td width="81"><em>MESI state</em></td>

   <td width="45"> </td>

   <td width="78"><em>Tag</em></td>

   <td colspan="2" width="81"><em>MESI state</em></td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"><em>Set 0</em></td>

   <td width="80">0x5F111F</td>

   <td width="81">M</td>

   <td width="45"><em>Set 0</em></td>

   <td width="78">0x5FF000</td>

   <td colspan="2" width="81">M</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"><em>Set 1</em></td>

   <td width="80">0x511100</td>

   <td width="81">E</td>

   <td width="45"><em>Set 1</em></td>

   <td width="78">0x511100</td>

   <td colspan="2" width="81">S</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"><em>Set 2</em></td>

   <td width="80">0x5FFFFF</td>

   <td width="81">S</td>

   <td width="45"><em>Set 2</em></td>

   <td width="78">0x5FFFF0</td>

   <td colspan="2" width="81">I</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"><em>Set 3</em></td>

   <td width="80">0x533333</td>

   <td width="81">I</td>

   <td width="45"><em>Set 3</em></td>

   <td width="78">0x533333</td>

   <td colspan="2" width="81">I</td>

   <td width="2"> </td>

  </tr>

  <tr>

   <td width="45"></td>

   <td width="80"></td>

   <td width="81"></td>

   <td width="44"></td>

   <td width="45"></td>

   <td width="78"></td>

   <td width="2"></td>

   <td width="79"></td>

   <td width="2"></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>What is the <em>minimum </em>set of memory instructions that leads the system from the initial state to the final state? Indicate the set of instructions in order, and clearly specify the access type (ld/st), the address of each memory request, and the processor from which the request is generated.</li>

</ul>

<h1>6.      Memory Consistency</h1>

A programmer writes the following two C code segments. She wants to run them concurrently on a multicore processor, called SC, using two different threads, each of which will run on a different core. The processor implements <em>sequential consistency</em>, as we discussed in the lecture.

<table width="406">

 <tbody>

  <tr>

   <td width="88">Instr. T0.0Instr. T0.1Instr. T0.2Instr. T0.3</td>

   <td width="159">Thread T0a = X[0]; b = a + Y[0];while(*flag == 0);Y[0] += 1;</td>

   <td width="80">Instr. T1.0Instr. T1.1Instr. T1.2Instr. T1.3</td>

   <td width="80">Thread T1Y[0] = 1;*flag = 1;X[1] *= 2; a = 0;</td>

  </tr>

 </tbody>

</table>

X, Y, and flag have been allocated in main memory, while a and b are contained in processor registers. A read or write to any of these variables generates a single memory request. The initial values of all memory locations and variables are 0. Assume each line of the C code segment of a thread is a <em>single </em>instruction.

<ul>

 <li>What is the final value of Y[0] in the SC processor, after both threads finish execution? Explain your answer.</li>

 <li>What is the final value of b in the SC processor, after both threads finish execution? Explain your answer.</li>

</ul>

With the aim of achieving higher performance, the programmer tests her code on a new multicore processor, called RC, that implements <em>weak consistency</em>. As discussed in the lecture, the weak consistency model has no need to guarantee a strict order of memory operations. For this question, consider a very weak model where there is <em>no </em>guarantee on the ordering of instructions as seen by different cores.

<ul>

 <li>What is the final value of Y[0] in the RC processor, after both threads finish execution? Explain your answer.</li>

</ul>

After several months spent debugging her code, the programmer learns that the new processor includes a memory_fence() instruction in its ISA. The semantics of memory_fence() is as follows for a given thread that executes it:

<ol>

 <li>Wait (stall the processor) until <em>all </em>preceding memory operations from the thread complete in the memory system and become visible to other cores.</li>

 <li>Ensure <em>no </em>memory operation from any later instruction in the thread gets executed before the memory_fence() is retired.</li>

</ol>

<ul>

 <li>What <em>minimal </em>changes should the programmer make to the program above to ensure that the final value of Y[0] on RC is the same as that in part (a) on SC? Explain your answer.</li>

</ul>

<h1>7.      BONUS: Building Multicore Processors</h1>

You are hired by Amdahl’s Nano Devices (AND) to design their newest multicore processor.

Ggl, one of AND’s largest customers, has found that the following program can predict people’s happiness.

for (i = 12; i &lt; 2985984; i++) {

past = A[i-12]; current = A[i]; past *= 0.37; current *= 0.63;

A[i] = past + current;

}

A is a large array of 4-byte floating point numbers, gathered by Ggl over the years by harvesting people’s private messages. Your job is to create a processor that runs this program as fast as possible.

Assume the following:

<ul>

 <li>You have magically fast DRAM that allows infinitely many cores to access data in parallel. We will relax this strong assumption in parts (d), (e), (f).</li>

 <li>Each floating point instruction (addition and multiplication) takes 10 cycles.</li>

 <li>Each memory read and write takes 10 cycles.</li>

 <li>No caches are used.</li>

 <li>Integer operations and branches are fast enough that they can be ignored.</li>

</ul>

(a) Assuming infinitely many cores, what is the maximum steady state speedup you can achieve for this program? Please show all your computations.

It turns out magic DRAM does not exist except in Macondo<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>. As a result, you have to use cheap, slow, low-bandwidth DRAM. To compensate for this, you decide to use a private L1 cache for each processor. The new specifications for the DRAM and the L1 cache are:

<ul>

 <li>DRAM is shared by all processors. DRAM may only process one request (read or write) at a time.</li>

 <li>DRAM takes 100 cycles to process any request.</li>

 <li>DRAM prioritizes accesses of smaller addresses and write requests. (Assume no virtual memory)</li>

 <li>The cache is direct-mapped. Each cache block is 16 bytes.</li>

 <li>It takes 10 cycles to access the cache. Therefore, a cache hit is processed in 10 cycles and a cache miss is processed in 110 cycles.</li>

</ul>

All other latencies remain the same as specified earlier. Answer parts (d), (e), (f) assuming this new system.

(d) Can you still achieve the same steady state speedup as before? Circle one: YES                   NO

Please explain.

<a href="#_ftnref1" name="_ftn1">[1]</a> An imaginary town featured in <em>One Hundred Years of Solitude </em>by the late Colombian author Gabriel García Márquez

(1927-2014).