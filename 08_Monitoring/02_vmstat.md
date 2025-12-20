## **vmstat command :**

**vmstat 1**
```
vmstat 1
```

What it shows

- Updates every 1 second

- First line = since boot (ignore it)

- Following lines = real-time behavior

When to use

- System feels slow

- CPU vs memory vs I/O diagnosis

This is what admins use most

##

**vmstat 1 10**
```
vmstat 1 10
```

What it shows

- 10 samples

- 1-second interval

- Then exits



<img width="1082" height="75" alt="image" src="https://github.com/user-attachments/assets/aab540b2-3f80-46fd-bd57-9a512fc3e2b8" />

<img width="719" height="470" alt="image" src="https://github.com/user-attachments/assets/cbbd4b73-9f7f-4ba7-9ae0-e0b4fcd7845c" />

##

## **1) Processes (run queue) :**

```r  b```

r → runnable processes (waiting for CPU)

b → blocked processes (usually waiting for I/O)

**If r > number of CPU cores → CPU pressure**

---

## **2) Memory :**
```
swpd  free  buff  cache
```

swpd = swap used (should ideally be 0)

free = unused RAM

buff = filesystem metadata

cache = file cache (this is good, not bad)


**- Low free is normal**
**- Growing swpd is bad**

---

## **3) Swap activity :**

```si  so```

si → swap in (from disk → RAM)

so → swap out (from RAM → disk)

**Non-zero values over time = memory pressure**

##

**What is “swap” in the first place?**

- Swap is disk space used as an extension of RAM.

- When RAM is insufficient, the kernel can:

   - move memory pages from RAM → disk (swap out)

   - later bring them back from disk → RAM (swap in)

**So swap activity is memory movement, not process movement.**

##

**What exactly is being swapped?**

- Not bytes, not processes — memory pages ( A page is usually 4 KB Sometimes larger (e.g., 2 MB huge pages) )

- So when we say: “swap out happened” it mean: some memory pages were written to disk

```
Non-zero continuously
si so
12 18
15 20
14 17
```

This means:

- RAM is insufficient ( bez Swap activity means the kernel is moving memory pages between RAM and disk because RAM is under pressure. )
- Kernel is constantly moving pages
- Useful work is being replaced by disk I/O

**This is called thrashing. This is the bad case.**

##

**Higher swapping rate == high waiting of Cpu (wa)... but how ??**

When RAM is insufficient, memory pages are swapped to disk.
When a process needs those pages again, it blocks while the kernel reads them back from disk.
During this time the CPU waits on I/O, so wa increases and the system feels slow.”

---

## **4) Disk I/O :**

Disk I/O = reading data from disk or writing data to disk ..That’s it.

Whenever the system:
```
reads a file

writes logs

loads a binary

swaps memory

accesses a database

pulls container layers
```
…it performs disk input/output.

remember :
- Disk = slow
- CPU + RAM = fast

For a program to run, it needs:

- CPU time
- Its data/code in RAM (The CPU cannot use data that is still on disk.)

##

**What happens when data is NOT in RAM?**

If the program needs data that is on disk:

Program asks for the data

- Kernel says: “wait”
- Disk starts working (slow)
- CPU cannot do useful work for this program
- Program is blocked

This waiting = disk I/O wait


##

**What is an I/O bottleneck? (core idea)**

An I/O bottleneck means:  Many programs are ready to run, but all of them are waiting for disk.

So:

- CPU is free
- Programs are stuck
- Disk is overloaded

The system feels slow even though CPU looks idle.

##

**What bi and bo really mean**

In vmstat:

bi → blocks read from disk (disk → RAM) per second
bo → blocks written to disk (RAM → disk) per second

```
so if bi / bo is high then disk is doing a lot of reads/writes and 
if Disk is slow → requests take time

Processes that need disk data must wait
→ they enter blocked state

CPU has nothing useful to do for them
→ CPU shows I/O wait (wa)
```

**but if disk is fast and we have enough RAM then processes need not wait and cpu is not idle so no bottleneck.**

bottleneck simple means :
```
bi high
bo high
b high
wa high
```

---

## **5) CPU**
```
us  sy  id  wa  st
```

us → user CPU (% of CPU time spent running user-space code)

sy → kernel CPU

id → idle

wa → waiting on I/O (very important)

st → stolen time (VMs only)

- High wa = disk/network is slow
- High id = CPU is NOT your problem
