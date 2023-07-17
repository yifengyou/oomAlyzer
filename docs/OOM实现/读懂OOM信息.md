<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [读懂OOM信息](#读懂oom信息)   
   - [最简单的OOM](#最简单的oom)   
   - [信息解读](#信息解读)   

<!-- /MDTOC -->
# 读懂OOM信息

## 最简单的OOM

```
Jul 15 23:44:32 rocky8 kernel: oom invoked oom-killer: gfp_mask=0x6280ca(GFP_HIGHUSER_MOVABLE|__GFP_ZERO), order=0, oom_score_adj=0
Jul 15 23:44:32 rocky8 kernel: CPU: 1 PID: 2074 Comm: oom Kdump: loaded Not tainted 4.18.0-477.13.1.el8_8.x86_64 #1
Jul 15 23:44:32 rocky8 kernel: Hardware name: QEMU Standard PC (i440FX + PIIX, 1996), BIOS 1.14.0-2 04/01/2014
Jul 15 23:44:32 rocky8 kernel: Call Trace:
Jul 15 23:44:32 rocky8 kernel: dump_stack+0x41/0x60
Jul 15 23:44:32 rocky8 kernel: dump_header+0x4a/0x1df
Jul 15 23:44:32 rocky8 kernel: oom_kill_process.cold.33+0xb/0x10
Jul 15 23:44:32 rocky8 kernel: out_of_memory+0x1bd/0x4e0
Jul 15 23:44:32 rocky8 kernel: __alloc_pages_slowpath+0xbe7/0xcd0
Jul 15 23:44:32 rocky8 kernel: __alloc_pages_nodemask+0x2e2/0x330
Jul 15 23:44:32 rocky8 kernel: alloc_pages_vma+0x74/0x1d0
Jul 15 23:44:32 rocky8 kernel: handle_pte_fault+0x354/0x880
Jul 15 23:44:32 rocky8 kernel: ? do_huge_pmd_anonymous_page+0x15a/0x870
Jul 15 23:44:32 rocky8 kernel: __handle_mm_fault+0x453/0x6c0
Jul 15 23:44:32 rocky8 kernel: ? apic_timer_interrupt+0xa/0x20
Jul 15 23:44:32 rocky8 kernel: handle_mm_fault+0xca/0x2a0
Jul 15 23:44:32 rocky8 kernel: __do_page_fault+0x1f0/0x450
Jul 15 23:44:32 rocky8 kernel: ? __do_page_fault+0x21e/0x450
Jul 15 23:44:32 rocky8 kernel: do_page_fault+0x37/0x130
Jul 15 23:44:32 rocky8 kernel: ? page_fault+0x8/0x30
Jul 15 23:44:32 rocky8 kernel: page_fault+0x1e/0x30
Jul 15 23:44:32 rocky8 kernel: RIP: 0033:0x7ff9f838c291
Jul 15 23:44:32 rocky8 kernel: Code: 01 00 00 48 83 fa 40 77 77 c5 fe 7f 44 17 e0 c5 fe 7f 07 c5 f8 77 c3 66 90 f3 0f 1e fa c5 f8 77 48 89 d1 40 0f b6 c6 48 89 fa <f3> aa 48 89 d0 c3 66 0f 1f 84 00 00 00 00 00 f3 0f 1e fa 48 39 d1
Jul 15 23:44:32 rocky8 kernel: RSP: 002b:00007ffee7631168 EFLAGS: 00010206
Jul 15 23:44:32 rocky8 kernel: RAX: 0000000000000009 RBX: 0000000000000000 RCX: 000000001526f010
Jul 15 23:44:32 rocky8 kernel: RDX: 00007ff8782b7010 RSI: 0000000000000009 RDI: 00007ff8a3048000
Jul 15 23:44:32 rocky8 kernel: RBP: 00007ffee7631180 R08: 00000000ffffffff R09: 0000000000000000
Jul 15 23:44:32 rocky8 kernel: R10: 0000000000000022 R11: 0000000000000246 R12: 0000000000400580
Jul 15 23:44:32 rocky8 kernel: R13: 00007ffee7631260 R14: 0000000000000000 R15: 0000000000000000
Jul 15 23:44:32 rocky8 kernel: Mem-Info:
Jul 15 23:44:32 rocky8 kernel: active_anon:4558 inactive_anon:469552 isolated_anon:0#012 active_file:6371 inactive_file:4910 isolated_file:0#012 unevictable:0 dirty:0 writeback:0#012 slab_reclaimable:9955 slab_unreclaimable:17169#012 mapped:5675 shmem:613 pagetables:4454 bounce:0#012 free:1378257 free_pcp:0 free_cma:0
Jul 15 23:44:32 rocky8 kernel: Node 3 active_anon:14424kB inactive_anon:1863636kB active_file:24kB inactive_file:4kB unevictable:0kB isolated(anon):0kB isolated(file):0kB mapped:84kB dirty:0kB writeback:0kB shmem:16kB shmem_thp: 0kB shmem_pmdmapped: 0kB anon_thp: 2048kB writeback_tmp:0kB kernel_stack:948kB pagetables:13140kB all_unreclaimable? yes
Jul 15 23:44:32 rocky8 kernel: Node 3 Normal free:36376kB min:34644kB low:43304kB high:51964kB active_anon:14424kB inactive_anon:1863228kB active_file:24kB inactive_file:4kB unevictable:0kB writepending:0kB present:2048000kB managed:1968380kB mlocked:0kB bounce:0kB free_pcp:0kB local_pcp:0kB free_cma:0kB
Jul 15 23:44:32 rocky8 kernel: lowmem_reserve[]: 0 0 0 0 0
Jul 15 23:44:32 rocky8 kernel: Node 3 Normal: 73*4kB (UME) 13*8kB (UEH) 2*16kB (UH) 27*32kB (UMEH) 11*64kB (UME) 3*128kB (EH) 3*256kB (UMH) 7*512kB (UME) 29*1024kB (UM) 0*2048kB 0*4096kB = 36428kB
Jul 15 23:44:32 rocky8 kernel: Node 0 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=1048576kB
Jul 15 23:44:32 rocky8 kernel: Node 0 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
Jul 15 23:44:32 rocky8 kernel: Node 1 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=1048576kB
Jul 15 23:44:32 rocky8 kernel: Node 1 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
Jul 15 23:44:32 rocky8 kernel: Node 2 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=1048576kB
Jul 15 23:44:32 rocky8 kernel: Node 2 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
Jul 15 23:44:32 rocky8 kernel: Node 3 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=1048576kB
Jul 15 23:44:32 rocky8 kernel: Node 3 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
Jul 15 23:44:32 rocky8 kernel: 13503 total pagecache pages
Jul 15 23:44:32 rocky8 kernel: 1609 pages in swap cache
Jul 15 23:44:32 rocky8 kernel: Swap cache stats: add 5512946, delete 5510992, find 2145/4494
Jul 15 23:44:32 rocky8 kernel: Free swap  = 12kB
Jul 15 23:44:32 rocky8 kernel: Total swap = 4149244kB
Jul 15 23:44:32 rocky8 kernel: 2047866 pages RAM
Jul 15 23:44:32 rocky8 kernel: 0 pages HighMem/MovableOnly
Jul 15 23:44:32 rocky8 kernel: 126938 pages reserved
Jul 15 23:44:32 rocky8 kernel: 0 pages hwpoisoned
Jul 15 23:44:32 rocky8 kernel: Tasks state (memory values in pages):
Jul 15 23:44:32 rocky8 kernel: [  pid  ]   uid  tgid total_vm      rss pgtables_bytes swapents oom_score_adj name
Jul 15 23:44:32 rocky8 kernel: [    774]     0   774    22394     1057   225280      197             0 systemd-journal
Jul 15 23:44:32 rocky8 kernel: [    809]     0   809    24731      396   204800      591         -1000 systemd-udevd
Jul 15 23:44:32 rocky8 kernel: [    921]     0   921    32727      187   135168      149         -1000 auditd
Jul 15 23:44:32 rocky8 kernel: [    923]     0   923    12163        0   135168       93             0 sedispatch
Jul 15 23:44:32 rocky8 kernel: [    956]    81   956    16207      415   159744      129          -900 dbus-daemon
Jul 15 23:44:32 rocky8 kernel: [    957]   997   957     2154        5    61440       36             0 lsmd
Jul 15 23:44:32 rocky8 kernel: [    958]     0   958    31266      288   131072       21             0 irqbalance
Jul 15 23:44:32 rocky8 kernel: [    959]     0   959     1664       69    61440       33             0 mcelog
Jul 15 23:44:32 rocky8 kernel: [    960]     0   960    20819      437   192512      500             0 systemd-logind
Jul 15 23:44:32 rocky8 kernel: [    964]     0   964    12574      384   135168       44             0 smartd
Jul 15 23:44:32 rocky8 kernel: [    966]     0   966   125943      508   479232     6011             0 firewalld
Jul 15 23:44:32 rocky8 kernel: [    971]   993   971    35019      186   167936       76             0 chronyd
Jul 15 23:44:32 rocky8 kernel: [    999]     0   999   147654      944   389120      491             0 NetworkManager
Jul 15 23:44:32 rocky8 kernel: [   1013]     0  1013   175317     1424   446464     3068             0 tuned
Jul 15 23:44:32 rocky8 kernel: [   1015]     0  1015    19163      100   192512      230         -1000 sshd
Jul 15 23:44:32 rocky8 kernel: [   1023]     0  1023    54813       38    73728       30             0 agetty
Jul 15 23:44:32 rocky8 kernel: [   1025]     0  1025     6533       82    98304       44             0 atd
Jul 15 23:44:32 rocky8 kernel: [   1029]     0  1029    54903       27    61440        1             0 agetty
Jul 15 23:44:32 rocky8 kernel: [   1031]     0  1031    58907      175   106496      188             0 crond
Jul 15 23:44:32 rocky8 kernel: [   1242]   998  1242   504147      588   393216     2031             0 polkitd
Jul 15 23:44:32 rocky8 kernel: [   1743]     0  1743    32818      480   299008      293             0 sshd
Jul 15 23:44:32 rocky8 kernel: [   1747]     0  1747    32819      547   303104      225             0 sshd
Jul 15 23:44:32 rocky8 kernel: [   1752]     0  1752    22395      828   212992      304             0 systemd
Jul 15 23:44:32 rocky8 kernel: [   1754]     0  1754    34949      175   278528     1098             0 (sd-pam)
Jul 15 23:44:32 rocky8 kernel: [   1761]     0  1761    32900      415   290816      262             0 sshd
Jul 15 23:44:32 rocky8 kernel: [   1762]     0  1762    56683      175    86016      592             0 bash
Jul 15 23:44:32 rocky8 kernel: [   1776]     0  1776    32819      124   299008      227             0 sshd
Jul 15 23:44:32 rocky8 kernel: [   1793]     0  1793     7342      255   102400        0             0 sftp-server
Jul 15 23:44:32 rocky8 kernel: [   1876]     0  1876    59513      118   118784      107             0 tmux: client
Jul 15 23:44:32 rocky8 kernel: [   1878]     0  1878    60428      791   118784      187             0 tmux: server
Jul 15 23:44:32 rocky8 kernel: [   1879]     0  1879    56687      741    81920      306             0 bash
Jul 15 23:44:32 rocky8 kernel: [   1918]     0  1918    56658      556    86016      581             0 bash
Jul 15 23:44:32 rocky8 kernel: [   2068]     0  2068    54653      977   188416      133             0 rsyslogd
Jul 15 23:44:32 rocky8 kernel: [   2073]     0  2073    54876      537    69632        0             0 make
Jul 15 23:44:32 rocky8 kernel: [   2074]     0  2074  1573962   468395 11972608  1018086             0 oom
Jul 15 23:44:32 rocky8 kernel: oom-kill:constraint=CONSTRAINT_MEMORY_POLICY,nodemask=3,cpuset=/,mems_allowed=0-3,global_oom,task_memcg=/user.slice/user-0.slice/session-1.scope,task=oom,pid=2074,uid=0
Jul 15 23:44:32 rocky8 kernel: Out of memory: Killed process 2074 (oom) total-vm:6295848kB, anon-rss:1872532kB, file-rss:1048kB, shmem-rss:0kB, UID:0 pgtables:11692kB oom_score_adj:0
```




## 信息解读

```
Jul 15 23:44:32 rocky8 kernel: oom invoked oom-killer: gfp_mask=0x6280ca(GFP_HIGHUSER_MOVABLE|__GFP_ZERO), order=0, oom_score_adj=0
```
解析：
表示oom这个进程在请求内存时触发了oom-killer
- gfp_mask是一个**标志位**，用来表示内存分配的条件和要求。例如，GFP_HIGHUSER表示分配高端内存，__GFP_ZERO表示分配的内存要清零
  - gfp_mask中的gfp是get free page的缩写，表示获取空闲页的意思
  - gfp_mask是一个**标志位**，用来表示内存分配的条件和要求
  - gfp_mask中的**低4位**用来表示应该从哪个物理内存区域zone中获取内存页page，例如：
      - ___GFP_DMA表示从DMA区域分配内存
      - ___GFP_HIGHMEM表示从高端内存区域分配内存
  - gfp_mask中除了区域修饰符之外，还有其他的分配标志，例如：
      - __GFP_WAIT表示内存分配过程中可以被打断
      - __GFP_ZERO表示分配的内存要清零
  - gfp_mask中的分配标志可以混合组合使用，例如GFP_KERNEL表示可以睡眠，可以有IO和VFS操作的内核空间分配
- order是一个整数，用来表示分配的内存页的数量
  - order=0表示分配1个页，order=1表示分配2个页，order=2表示分配4个页，依此类推
- oom_adj是一个整数，用来调整进程的oom_score
  - adj是adjustment的缩写，表示调整的意思。
  - oom_score是一个**指标**，用来表示进程在内存不足时被杀死的可能性。
  - oom_adj越大，进程的oom_score越高，越有可能被杀死
  - oom_adj可以在**-17到15**之间取值，-17表示永远不被杀死，15表示最容易被杀死
- oom_score_adj是一个新的接口，用来替代oom_adj
  - 它的取值范围是**-1000到1000**，-1000表示永远不被杀死，1000表示最容易被杀死

```
Jul 15 23:44:32 rocky8 kernel: CPU: 1 PID: 2074 Comm: oom Kdump: loaded Not tainted 4.18.0-477.13.1.el8_8.x86_64 #1
```
解析：
- CPU: 1 表示记录日志的CPU编号是1。
- PID: 2074 表示记录日志的进程编号是2074。
- Comm: oom 表示记录日志的进程名称是oom，即oom-killer。
- Kdump: loaded 表示记录日志时已经加载了Kdump模块，用于在内核崩溃时生成内存转储文件。
- Not tainted 表示记录日志时内核没有被污染，即没有加载非开源的模块或驱动。
- 4.18.0-477.13.1.el8_8.x86_64 表示记录日志时内核的版本号。
- #1 表示记录日志时内核的编译次数
  - 与```uname -v```的输出```#1 SMP Tue May 30 22:15:39 UTC 2023``` 一致
  - 一般都是 #1 ，底层来看，它是Linux源代码中EXTRAVERSION选项默认值


```
Jul 15 23:44:32 rocky8 kernel: Hardware name: QEMU Standard PC (i440FX + PIIX, 1996), BIOS 1.14.0-2 04/01/2014
```
解析：
这表示系统的硬件名称，QEMU是一种虚拟机软件，i440FX和PIIX是Intel芯片组，BIOS是基本输入输出系统
- Hardware name: QEMU Standard PC (i440FX + PIIX, 1996) 表示记录日志的硬件名称是QEMU标准PC，使用了i440FX芯片组和PIIX南桥，这是一种模拟1996年的PC架构的虚拟机
- BIOS 1.14.0-2 04/01/2014 表示记录日志时BIOS的版本号和日期。BIOS是Basic Input/Output System的缩写，它是一种固件，用于管理硬件和启动操作系统

```
Jul 15 23:44:32 rocky8 kernel: Call Trace:
Jul 15 23:44:32 rocky8 kernel: dump_stack+0x41/0x60
Jul 15 23:44:32 rocky8 kernel: dump_header+0x4a/0x1df
Jul 15 23:44:32 rocky8 kernel: oom_kill_process.cold.33+0xb/0x10
Jul 15 23:44:32 rocky8 kernel: out_of_memory+0x1bd/0x4e0
Jul 15 23:44:32 rocky8 kernel: __alloc_pages_slowpath+0xbe7/0xcd0
Jul 15 23:44:32 rocky8 kernel: __alloc_pages_nodemask+0x2e2/0x330
Jul 15 23:44:32 rocky8 kernel: alloc_pages_vma+0x74/0x1d0
Jul 15 23:44:32 rocky8 kernel: handle_pte_fault+0x354/0x880
Jul 15 23:44:32 rocky8 kernel: ? do_huge_pmd_anonymous_page+0x15a/0x870
Jul 15 23:44:32 rocky8 kernel: __handle_mm_fault+0x453/0x6c0
Jul 15 23:44:32 rocky8 kernel: ? apic_timer_interrupt+0xa/0x20
Jul 15 23:44:32 rocky8 kernel: handle_mm_fault+0xca/0x2a0
Jul 15 23:44:32 rocky8 kernel: __do_page_fault+0x1f0/0x450
Jul 15 23:44:32 rocky8 kernel: ? __do_page_fault+0x21e/0x450
Jul 15 23:44:32 rocky8 kernel: do_page_fault+0x37/0x130
Jul 15 23:44:32 rocky8 kernel: ? page_fault+0x8/0x30
Jul 15 23:44:32 rocky8 kernel: page_fault+0x1e/0x30
Jul 15 23:44:32 rocky8 kernel: RIP: 0033:0x7ff9f838c291
Jul 15 23:44:32 rocky8 kernel: Code: 01 00 00 48 83 fa 40 77 77 c5 fe 7f 44 17 e0 c5 fe 7f 07 c5 f8 77 c3 66 90 f3 0f 1e fa c5 f8 77 48 89 d1 40 0f b6 c6 48 89 fa <f3> aa 48 89 d0 c3 66 0f 1f 84 00 00 00 00 00 f3 0f 1e fa 48 39 d1
Jul 15 23:44:32 rocky8 kernel: RSP: 002b:00007ffee7631168 EFLAGS: 00010206
Jul 15 23:44:32 rocky8 kernel: RAX: 0000000000000009 RBX: 0000000000000000 RCX: 000000001526f010
Jul 15 23:44:32 rocky8 kernel: RDX: 00007ff8782b7010 RSI: 0000000000000009 RDI: 00007ff8a3048000
Jul 15 23:44:32 rocky8 kernel: RBP: 00007ffee7631180 R08: 00000000ffffffff R09: 0000000000000000
Jul 15 23:44:32 rocky8 kernel: R10: 0000000000000022 R11: 0000000000000246 R12: 0000000000400580
Jul 15 23:44:32 rocky8 kernel: R13: 00007ffee7631260 R14: 0000000000000000 R15: 0000000000000000
```
解析：
这表示内核在触发OOM时的函数调用栈，可以用于调试和定位问题
- Code
- RAX-R15：寄存器值

```
Jul 15 23:44:32 rocky8 kernel: Mem-Info:
Jul 15 23:44:32 rocky8 kernel: active_anon:4558 inactive_anon:469552 isolated_anon:0#012 active_file:6371 inactive_file:4910 isolated_file:0#012 unevictable:0 dirty:0 writeback:0#012 slab_reclaimable:9955 slab_unreclaimable:17169#012 mapped:5675 shmem:613 pagetables:4454 bounce:0#012 free:1378257 free_pcp:0 free_cma:0
Jul 15 23:44:32 rocky8 kernel: Node 3 active_anon:14424kB inactive_anon:1863636kB active_file:24kB inactive_file:4kB unevictable:0kB isolated(anon):0kB isolated(file):0kB mapped:84kB dirty:0kB writeback:0kB shmem:16kB shmem_thp: 0kB shmem_pmdmapped: 0kB anon_thp: 2048kB writeback_tmp:0kB kernel_stack:948kB pagetables:13140kB all_unreclaimable? yes
Jul 15 23:44:32 rocky8 kernel: Node 3 Normal free:36376kB min:34644kB low:43304kB high:51964kB active_anon:14424kB inactive_anon:1863228kB active_file:24kB inactive_file:4kB unevictable:0kB writepending:0kB present:2048000kB managed:1968380kB mlocked:0kB bounce:0kB free_pcp:0kB local_pcp:0kB free_cma:0kB
Jul 15 23:44:32 rocky8 kernel: lowmem_reserve[]: 0 0 0 0 0
Jul 15 23:44:32 rocky8 kernel: Node 3 Normal: 73*4kB (UME) 13*8kB (UEH) 2*16kB (UH) 27*32kB (UMEH) 11*64kB (UME) 3*128kB (EH) 3*256kB (UMH) 7*512kB (UME) 29*1024kB (UM) 0*2048kB 0*4096kB = 36428kB
Jul 15 23:44:32 rocky8 kernel: Node 0 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=1048576kB
Jul 15 23:44:32 rocky8 kernel: Node 0 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
Jul 15 23:44:32 rocky8 kernel: Node 1 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=1048576kB
Jul 15 23:44:32 rocky8 kernel: Node 1 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
Jul 15 23:44:32 rocky8 kernel: Node 2 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=1048576kB
Jul 15 23:44:32 rocky8 kernel: Node 2 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
Jul 15 23:44:32 rocky8 kernel: Node 3 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=1048576kB
Jul 15 23:44:32 rocky8 kernel: Node 3 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
Jul 15 23:44:32 rocky8 kernel: 13503 total pagecache pages
Jul 15 23:44:32 rocky8 kernel: 1609 pages in swap cache
Jul 15 23:44:32 rocky8 kernel: Swap cache stats: add 5512946, delete 5510992, find 2145/4494
Jul 15 23:44:32 rocky8 kernel: Free swap  = 12kB
Jul 15 23:44:32 rocky8 kernel: Total swap = 4149244kB
Jul 15 23:44:32 rocky8 kernel: 2047866 pages RAM
Jul 15 23:44:32 rocky8 kernel: 0 pages HighMem/MovableOnly
Jul 15 23:44:32 rocky8 kernel: 126938 pages reserved
Jul 15 23:44:32 rocky8 kernel: 0 pages hwpoisoned
```
解析：
- Mem-Info: 表示这是一条内存信息的日志。系统内存和交换空间的使用情况，包括总量、使用量、空闲量、缓存量、锁定量、脏量、回写量等
- active_anon: 表示活跃的匿名内存页的数量，即没有映射到文件的内存页，通常是**进程的堆或栈空间**
  - inactive_anon: 表示不活跃的匿名内存页的数量，即可能被换出到交换空间的内存页。
  - isolated_anon: 表示被隔离的匿名内存页的数量，即正在被回收或迁移的内存页。
  - active_file: 表示活跃的文件映射内存页的数量，即被频繁访问的文件缓存。
  - inactive_file: 表示不活跃的文件映射内存页的数量，即可能被回收或换出的文件缓存。
  - unevictable: 表示不可回收或换出的内存页的数量，即被锁定或保留在内存中的内存页。
  - dirty: 表示脏页的数量，即被修改过但还没有写回到磁盘的文件缓存。
  - writeback: 表示正在写回到磁盘的脏页的数量。
  - slab_reclaimable: 表示可回收的slab对象的数量，即用于缓存内核数据结构的内存对象，如inode、dentry等。
  - slab_unreclaimable: 表示不可回收的slab对象的数量，即用于缓存一些重要或频繁使用的内核数据结构的内存对象。
  - mapped: 表示映射到用户空间进程地址空间的文件缓存页或匿名页的数量。
  - shmem: 表示共享内存对象或tmpfs文件系统使用的内存页的数量。
  - pagetables: 表示用于管理虚拟地址到物理地址映射关系的页表占用的内存页的数量。
  - bounce: 表示用于处理高端内存和低端内存之间数据传输问题而创建的临时缓冲区占用的内存页的数量。
  - free: 表示空闲且可用于分配给任何进程或用途的内存页的数量。
  - free_pcp: 表示每个CPU上维护的本地空闲页面列表中包含的页面数。这些页面可以快速分配给本地CPU上运行的进程，也可以在需要时释放给全局空闲页面池。
  - free_cma: 表示连续内存分配器（CMA）管理并保留以便在需要时分配给DMA设备使用的空闲页面数。
- Node n: 表示节点n上各种类型和状态下占用和空闲内存大小情况。节点是一个物理上相邻并共享一定范围总线访问能力和速度特征（如本地和远程） 的一组CPU和RAM。节点之间可以通过互连总线进行通信。节点是NUMA（非统一访问）架构下管理和优化内存性能和访问效率 的基本单元。
- present: 表示节点上存在并可被操作系统使用（已被BIOS识别并初始化） 的物理RAM大小。
- managed: 表示节点上实际可供操作系统管理和分配使用 的物理RAM大小。managed = present - reserved，其中reserved表示被保留给内核或设备使用的内存大小。
- mlocked: 表示被mlock系统调用锁定在内存中不可换出的内存大小。
- bounce: 表示用于处理高端内存和低端内存之间数据传输问题而创建的临时缓冲区占用的内存大小。
- free_pcp: 表示每个CPU上维护的本地空闲页面列表中包含的页面大小。
- local_pcp: 表示每个CPU上维护的本地已分配页面列表中包含的页面大小。这些页面可以快速释放给本地CPU上运行的进程，也可以在需要时归还给全局已分配页面池。
- free_cma: 表示连续内存分配器（CMA）管理并保留以便在需要时分配给DMA设备使用的空闲内存大小。

- lowmem_reserve[]: 表示各个节点和区域之间预留的最低内存大小，用于防止某个节点或区域耗尽内存而影响其他节点或区域的正常运行。

- Node n Zone z: 表示节点n上区域z中各种类型和状态下占用和空闲内存大小情况。区域是一个逻辑上划分的内存范围，用于管理不同类型或属性的内存。Linux内核通常将物理内存划分为三个区域：DMA、Normal和HighMem。
  - min: 表示区域中保证给每个进程使用的最小空闲内存大小
      - min表示该zone中最低的可用内存量，如果低于这个值，说明内存非常紧张，需要同步回收内存，即在分配内存之前先尝试释放一些内存，这会导致分配延迟和性能下降。只有一些紧急的或者带有GFP_ATOMIC标志的分配请求才能在低于min时分配内存，但是会放宽对watermark的检查
  - low: 表示区域中保证给当前进程使用的最小空闲内存大小
    - low表示该zone中警戒的可用内存量，如果低于这个值，说明内存有一定压力，需要异步回收内存，即在分配内存之后唤醒kswapd线程去后台释放一些内存，这不会阻塞分配过程。
  - high: 表示区域中开始回收进程使用的内存页的最小空闲内存大小
    - high表示该zone中安全的可用内存量，如果高于这个值，说明内存充足，不需要回收内存，kswapd线程会处于睡眠状态
  - 一般来说，high, low, min的比例关系是6:5:42。它们的具体值可以通过/proc/zoneinfo文件查看。它们也可以通过/proc/sys/vm/min_free_kbytes和/proc/sys/vm/watermark_scale_factor进行调节

- Node n Zone z: x*ykB (flags) = zkB 表示节点n上区域z中按照不同页面大小划分的空闲页面数量和标志位，以及总共的空闲内存大小。
  - x表示空闲页面的数量，y表示空闲页面的大小，flags表示空闲页面的标志位，zkB表示总共的空闲内存大小。
  - 标志位有以下含义：
  - M表示可移动（Movable），表示这些页面可以被迁移或回收，通常用于缓存用户空间进程数据或文件数据。
  - A表示可回收（Reclaimable），表示这些页面可以被回收或换出，通常用于缓存一些可再生的内核数据结构。
  - U表示不可回收（Unreclaimable），表示这些页面不能被回收或换出，通常用于缓存一些重要或频繁使用的内核数据结构。
  - E表示可交换（Exchangeable），表示这些页面可以被换出到交换空间，通常是匿名页面。
  - H表示高端（High），表示这些页面属于高端内存区域，需要特殊处理才能映射到内核地址空间或用户地址空间。
- Node n hugepages_total=x hugepages_free=y hugepages_surp=z hugepages_size=wkB
  - 这种消息表示系统中每个NUMA节点（Node n）的大页（hugepages）的使用情况。大页是一种特殊的内存分配方式，可以减少页表项的数量，提高内存访问效率。
  - 每个节点上有两种大小的大页（hugepages_size），分别是1048576kB和2048kB
  - hugepages_total: 表示节点上配置并保留给大页使用的大页数量。大页是一种特殊的内存页，它比普通的4KB页面要大得多，例如2MB或1GB。大页可以减少页表项的数量，提高地址转换和缓存命中率，从而提高性能。
  - hugepages_free: 表示节点上未使用且可供分配给进程使用的大页数量。
  - hugepages_surp: 表示节点上超过配置数量而额外分配给大页使用的大页数量。
    - 超额数是指系统在启动时没有预留但是后来动态分配的大页数
  - hugepages_size：表示该大小的大页占用的物理内存量，单位是kB。
- total pagecache pages 这个消息表示系统中总共有多少个页面缓存（pagecache）。页面缓存是一种用来加速文件访问的机制，它将文件系统中常用的数据缓存在物理内存中，避免了频繁地从磁盘读取数据。
- pages in swap cache 这个消息表示系统中有多少个页面在交换缓存（swap cache）中。交换缓存是一种用来加速交换（swap）操作的机制，它将被换出到磁盘上的页面保留在物理内存中，以便在需要时快速地换回来。
- Swap cache stats: add x, delete y, find z/w 这个消息表示系统中交换缓存（swap cache）的统计信息。它包含以下几个字段：
- add：表示有多少个页面被添加到交换缓存中。
- delete：表示有多少个页面被从交换缓存中删除。
- find：表示有多少次查找交换缓存成功（z）和失败（w）。
- Free swap = xkB 这个消息表示系统中剩余的可用交换空间（swap space）量，单位是kB。交换空间是一种用来扩展物理内存容量的机制，它将不常用的内存页面换出到磁盘上，以便为其他更需要内存的进程腾出空间。
- Total swap = xkB 这个消息表示系统中总共有多少交换空间（swap space），单位是kB。交换空间可以由一个或多个交换分区（swap partition）或者交换文件（swap file）组成。
- x pages RAM 这个消息表示系统中总共有多少物理内存页面（RAM page），单位是页面数。物理内存页面是一种用来管理物理内存空间的数据结构，它将物理内存划分为固定大小的块，每个块对应一个页面号和一个状态位。
- x pages HighMem/MovableOnly 这个消息表示系统中有多少高端内存（HighMem）或者可移动内存（MovableOnly）页面，单位是页面数。高端内存是指在32位系统中超过4GB的物理内存空间，它不能被直接映射到内核地址空间，需要通过特殊的机制来访问。可移动内存是指可以被迁移或者释放的物理内存页面，它可以用来分配大页（hugepages）或者连续的物理内存块。
- x pages reserved 这个消息表示系统中有多少保留的物理内存页面（reserved page），单位是页面数。保留的物理内存页面是指不能被分配给用户空间或者交换出去的页面，它们通常用于内核代码、数据、设备驱动等特殊用途。
- x pages hwpoisoned 这个消息表示系统中有多少被硬件损坏的物理内存页面（hwpoisoned page），单位是页面数。被硬件损坏的物理内存页面是指由于硬件故障导致无法正常访问的页面，它们会被标记为不可用，并且尝试回收或者隔离。






















```
Jul 15 23:44:32 rocky8 kernel: Tasks state (memory values in pages):
Jul 15 23:44:32 rocky8 kernel: [  pid  ]   uid  tgid total_vm      rss pgtables_bytes swapents oom_score_adj name
Jul 15 23:44:32 rocky8 kernel: [    774]     0   774    22394     1057   225280      197             0 systemd-journal
Jul 15 23:44:32 rocky8 kernel: [    809]     0   809    24731      396   204800      591         -1000 systemd-udevd
Jul 15 23:44:32 rocky8 kernel: [    921]     0   921    32727      187   135168      149         -1000 auditd
Jul 15 23:44:32 rocky8 kernel: [    923]     0   923    12163        0   135168       93             0 sedispatch
Jul 15 23:44:32 rocky8 kernel: [    956]    81   956    16207      415   159744      129          -900 dbus-daemon
Jul 15 23:44:32 rocky8 kernel: [    957]   997   957     2154        5    61440       36             0 lsmd
Jul 15 23:44:32 rocky8 kernel: [    958]     0   958    31266      288   131072       21             0 irqbalance
Jul 15 23:44:32 rocky8 kernel: [    959]     0   959     1664       69    61440       33             0 mcelog
Jul 15 23:44:32 rocky8 kernel: [    960]     0   960    20819      437   192512      500             0 systemd-logind
Jul 15 23:44:32 rocky8 kernel: [    964]     0   964    12574      384   135168       44             0 smartd
Jul 15 23:44:32 rocky8 kernel: [    966]     0   966   125943      508   479232     6011             0 firewalld
Jul 15 23:44:32 rocky8 kernel: [    971]   993   971    35019      186   167936       76             0 chronyd
Jul 15 23:44:32 rocky8 kernel: [    999]     0   999   147654      944   389120      491             0 NetworkManager
Jul 15 23:44:32 rocky8 kernel: [   1013]     0  1013   175317     1424   446464     3068             0 tuned
Jul 15 23:44:32 rocky8 kernel: [   1015]     0  1015    19163      100   192512      230         -1000 sshd
Jul 15 23:44:32 rocky8 kernel: [   1023]     0  1023    54813       38    73728       30             0 agetty
Jul 15 23:44:32 rocky8 kernel: [   1025]     0  1025     6533       82    98304       44             0 atd
Jul 15 23:44:32 rocky8 kernel: [   1029]     0  1029    54903       27    61440        1             0 agetty
Jul 15 23:44:32 rocky8 kernel: [   1031]     0  1031    58907      175   106496      188             0 crond
Jul 15 23:44:32 rocky8 kernel: [   1242]   998  1242   504147      588   393216     2031             0 polkitd
Jul 15 23:44:32 rocky8 kernel: [   1743]     0  1743    32818      480   299008      293             0 sshd
Jul 15 23:44:32 rocky8 kernel: [   1747]     0  1747    32819      547   303104      225             0 sshd
Jul 15 23:44:32 rocky8 kernel: [   1752]     0  1752    22395      828   212992      304             0 systemd
Jul 15 23:44:32 rocky8 kernel: [   1754]     0  1754    34949      175   278528     1098             0 (sd-pam)
Jul 15 23:44:32 rocky8 kernel: [   1761]     0  1761    32900      415   290816      262             0 sshd
Jul 15 23:44:32 rocky8 kernel: [   1762]     0  1762    56683      175    86016      592             0 bash
Jul 15 23:44:32 rocky8 kernel: [   1776]     0  1776    32819      124   299008      227             0 sshd
Jul 15 23:44:32 rocky8 kernel: [   1793]     0  1793     7342      255   102400        0             0 sftp-server
Jul 15 23:44:32 rocky8 kernel: [   1876]     0  1876    59513      118   118784      107             0 tmux: client
Jul 15 23:44:32 rocky8 kernel: [   1878]     0  1878    60428      791   118784      187             0 tmux: server
Jul 15 23:44:32 rocky8 kernel: [   1879]     0  1879    56687      741    81920      306             0 bash
Jul 15 23:44:32 rocky8 kernel: [   1918]     0  1918    56658      556    86016      581             0 bash
Jul 15 23:44:32 rocky8 kernel: [   2068]     0  2068    54653      977   188416      133             0 rsyslogd
Jul 15 23:44:32 rocky8 kernel: [   2073]     0  2073    54876      537    69632        0             0 make
Jul 15 23:44:32 rocky8 kernel: [   2074]     0  2074  1573962   468395 11972608  1018086             0 oom
```
解析：
这表示可能被OOM killer杀死的进程或者线程的信息，包括PID、UID、TGID、total_vm、rss、cpu、oom_adj、oom_score_adj和name
- PID是进程或者线程的标识符
- UID是用户标识符
- TGID是线程组标识符
- total_vm是虚拟内存使用量（以4 kB为单位）
- cpu是运行在哪个CPU上
- rss(Resident Set Size)是常驻内存使用量（以4 kB为单位）
- oom_adj和oom_score_adj是进程或者线程的OOM调整值，用于影响进程或者线程被杀死的可能性
- name是进程或者线程的名称

```
Jul 15 23:44:32 rocky8 kernel: oom-kill:constraint=CONSTRAINT_MEMORY_POLICY,nodemask=3,cpuset=/,mems_allowed=0-3,global_oom,task_memcg=/user.slice/user-0.slice/session-1.scope,task=oom,pid=2074,uid=0
```
解析：
- constraint表示触发oom-kill的内存约束类型，可能有以下几种：
    - CONSTRAINT_NONE表示没有内存约束。
    - CONSTRAINT_CPUSET表示内存约束由cpuset子系统设置。
    - CONSTRAINT_MEMCG表示内存约束由memory cgroup子系统设置。
    - CONSTRAINT_MEMORY_POLICY表示内存约束由内存策略设置。
- nodemask表示触发oom-kill的节点掩码，即哪些节点上的内存不足。
- cpuset表示触发oom-kill的cpuset路径，即哪些CPU和内存节点被分配给了进程。
- mems_allowed表示触发oom-kill的内存节点掩码，即哪些内存节点被允许使用。
- global_oom表示是否是全局性的oom-kill，即是否影响整个系统的内存。
- task_memcg表示触发oom-kill的memory cgroup路径，即哪些进程组被限制了内存使用量。
- task表示触发oom-kill的进程名，即哪个进程导致了内存不足。
- pid表示触发oom-kill的进程ID，即哪个进程导致了内存不足。
- uid表示触发oom-kill的用户ID，即哪个用户拥有了导致内存不足的进程。

```
Jul 15 23:44:32 rocky8 kernel: Out of memory: Killed process 2074 (oom) total-vm:6295848kB, anon-rss:1872532kB, file-rss:1048kB, shmem-rss:0kB, UID:0 pgtables:11692kB oom_score_adj:0
```
解析：
- 进程ID是2074
- 进程名是oom
- 虚拟内存使用量是6295848kB
- 物理内存使用量是1872532kB
- 用户ID是0
- 页表使用量是11692kB
- oom_score_adj值是0








































































---
