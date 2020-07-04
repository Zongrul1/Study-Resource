# BBR算法

## 限制阶段 
![](https://user-gold-cdn.xitu.io/2020/2/16/1704be0e25d01fd9?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)  
**app limit应用限制阶段**  
在这个阶段是应用程序开始发送数据，目前网络通畅RTT基本保持固定且很小，发送速率与RTT成反比，因此发送速率也是线性增加的，可以简单认为这个阶段有效带宽并没有达到上限，RTT是几乎固定的没有明显增长。  
**band limit带宽限制阶段**  
随着发送速率提高，网络中的数据包越来越多开始占用链路Buffer，此时RTT开始增加发送速率不再上升，有效带宽开始出现瓶颈，但是此时链路中的缓存区并没有占满，因此数据还在增加，RTT也开始增加。  
**buffer limit缓冲区限制阶段**  
随着链路中的Buffer被占满，开始出现丢包，这也是探测到的最大带宽，这个节点BDP+BufferSize也是基于丢包的控制策略的作用点。  

## 算法流程
![](https://user-gold-cdn.xitu.io/2020/2/16/1704be0e290a5b20?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)  
**StartUp慢启动阶段**
BBR的慢启动阶段类似于CUBIC的慢启动，同样是进行探测式加速区别在于BBR的慢启动使用2ln2的增益加速，过程中即使发生丢包也不会引起速率的降低，而是依据返回的确认数据包来判断带宽增长，直到带宽不再增长时就停止慢启动而进入下一个阶段，需要注意的是在寻找最大带宽的过程中产生了多余的2BDP的数据量，关于这块可以看下英文原文的解释：To handle Internet link bandwidths spanning 12 orders of magnitude, Startup implements a binary search for BtlBw by using a gain of 2/ln2 to double the sending rate while delivery rate is increasing. This discovers BtlBw in log2BDP RTTs but creates up to 2BDP excess queue in the process.  
**Drain排空阶段**  
排空阶段是为了把慢启动结束时多余的2BDP的数据量清空，此阶段发送速率开始下降，也就是单位时间发送的数据包数量在下降，直到未确认的数据包数量<BDP时认为已经排空，也可以认为是RTT不再下降为止，排空阶段结束。
**ProbeBW带宽探测阶段**  
经过慢启动和排空之后，目前发送方进入稳定状态进行数据的发送，由于网络带宽的变化要比RTT更为频繁，因此ProbeBW阶段也是BBR的主要阶段，在探测期中增加发包速率如果数据包ACK并没有受影响那么就继续增加，探测到带宽降低时也进行发包速率下降。
**ProbeRTT延时探测阶段**
前面三个过程在运行时都可能进入ProbeRTT阶段，当某个设定时间内都没有更新最小延时状态下开始降低数据包发送量，试图探测到更小的MinRTT，探测完成之后再根据最新数据来确定进入慢启动还是ProbeBW阶段。
