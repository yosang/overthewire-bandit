# Step 1
We got a `data.txt` file in our home directory, with is a hexdump that has been repeatedly compressed with different toools.

In order for us to get started with decompressing, we actual need to convert this file from a `hexdump` to a binary file. For this we will be using `xxd`

https://tldr.inbrowser.app/pages/common/xxd

The flag to revert a hexdump to a binary is `-r`

```bash
xxd -r data.txt newfile.txt
```

We run the code to create a new file, and use `file` to inspect it

```bash
bandit12@bandit:/tmp/myarch$ xxd -r data.txt newdata.txt
bandit12@bandit:/tmp/myarch$ ls -l
total 8
-rw-r----- 1 bandit12 bandit12 2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12  611 Jul 29 14:36 newdata.txt
bandit12@bandit:/tmp/myarch$ file newdata.txt 
newdata.txt: gzip compressed data, was "data2.bin", last modified: Mon Jul 28 19:03:32 2025, max compression, from Unix, original size modulo 2^32 578
```

# Step 2
We see that this file is a `gzip` compressed file, previously named data2.bin, which means we need to decompress it in order to get the content.

OBS: We cant decompress a txt file, so we need to rename it with the right extension in order to use `gunzip`

```bash
bandit12@bandit:/tmp/myarch$ gunzip newdata.txt
gzip: newdata.txt: unknown suffix -- ignored
bandit12@bandit:/tmp/myarch$ file newdata.txt 
newdata.txt: gzip compressed data, was "data2.bin", last modified: Mon Jul 28 19:03:32 2025, max compression, from Unix, original size modulo 2^32 578
bandit12@bandit:/tmp/myarch$ mv newdata.txt newdata.gz
bandit12@bandit:/tmp/myarch$ ls -l
total 8
-rw-r----- 1 bandit12 bandit12 2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12  611 Jul 29 14:36 newdata.gz
bandit12@bandit:/tmp/myarch$ gunzip newdata.gz 
bandit12@bandit:/tmp/myarch$ ls -l
total 8
-rw-r----- 1 bandit12 bandit12 2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12  578 Jul 29 14:36 newdata
bandit12@bandit:/tmp/myarch$ file newdata 
newdata: bzip2 compressed data, block size = 900k
```

We used the `mv` command to change it from `.txt` to `gz` and then ran `gunzip`.

After a successful decompresion we now have a new file with new extention, we run `file` on it and see that its a `bzip2` compressed file.

# Step 3
Ive never worked with `bzip2` before so we read up on https://tldr.inbrowser.app/pages/common/bzip2

It was as easy as running a `-d` flag on bzip2, and now we got a new file named `newdata.out`

```bash
bandit12@bandit:/tmp/myarch$ bzip2 -d newdata
bzip2: Can't guess original name for newdata -- using newdata.out
```
```bash
bandit12@bandit:/tmp/myarch$ file newdata.out 
newdata.out: gzip compressed data, was "data4.bin", last modified: Mon Jul 28 19:03:32 2025, max compression, from Unix, original size modulo 2^32 20480
```

From what we can see its another gzip, so we repeat `step 2` here.

```bash
bandit12@bandit:/tmp/myarch$ mv newdata.out newdata.gz
bandit12@bandit:/tmp/myarch$ ls -l
total 8
-rw-r----- 1 bandit12 bandit12 2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12  434 Jul 29 14:36 newdata.gz
bandit12@bandit:/tmp/myarch$ gunzip newdata.gz 
bandit12@bandit:/tmp/myarch$ ls -l
total 24
-rw-r----- 1 bandit12 bandit12  2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12 20480 Jul 29 14:36 newdata
bandit12@bandit:/tmp/myarch$ file newdata 
newdata: POSIX tar archive (GNU)
```

# Step 4
This time we got a POSIX tar archive, wich is just a tar

We unarhcive it with `tar` and the flag `-xf`, x stands for extranct and f stands for file

```bash
bandit12@bandit:/tmp/myarch$ tar -xf newdata
bandit12@bandit:/tmp/myarch$ ls -l
total 36
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data5.bin
-rw-r----- 1 bandit12 bandit12  2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12 20480 Jul 29 14:36 newdata
bandit12@bandit:/tmp/myarch$ file data5.bin 
data5.bin: POSIX tar archive (GNU)
```

We now have a new file `data5.bin`, which by the looks of it is another tar file.

```bash
bandit12@bandit:/tmp/myarch$ tar -xf data5.bin
bandit12@bandit:/tmp/myarch$ ls -l
total 40
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data5.bin
-rw-r--r-- 1 bandit12 bandit12   221 Jul 28 19:03 data6.bin
-rw-r----- 1 bandit12 bandit12  2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12 20480 Jul 29 14:36 newdata
bandit12@bandit:/tmp/myarch$ file data6.bin 
data6.bin: bzip2 compressed data, block size = 900k
```

Another file, its named `data6.bin` this time, we inspect it and its another `bzip2` file.

We decompress it wiht `bzip2 -d` and get a new `.out`

```bash
bandit12@bandit:/tmp/myarch$ ls -l
total 48
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data5.bin
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data6.bin.out
-rw-r----- 1 bandit12 bandit12  2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12 20480 Jul 29 14:36 newdata
bandit12@bandit:/tmp/myarch$ file data6.bin.out
data6.bin.out: POSIX tar archive (GNU)
```

At this point got a bunch of files, so we clear it up a bit before moving on

```bash
bandit12@bandit:/tmp/myarch$ ls -l
total 48
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data5.bin
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data6.bin.out
-rw-r----- 1 bandit12 bandit12  2639 Jul 29 14:30 data.txt
-rw-rw-r-- 1 bandit12 bandit12 20480 Jul 29 14:36 newdata
bandit12@bandit:/tmp/myarch$ rm -rf data5.bin newdata data.txt 
bandit12@bandit:/tmp/myarch$ ls -l
total 12
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data6.bin.out
```

# Step 5
After a new clean, we extract `data6.bin.out`, which was a tar archive file, and now have `data8.bin`, which by the looks of it is another gzip file...


```bash
bandit12@bandit:/tmp/myarch$ ls -l
total 16
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data6.bin.out
-rw-r--r-- 1 bandit12 bandit12    79 Jul 28 19:03 data8.bin
bandit12@bandit:/tmp/myarch$ file data8.bin 
data8.bin: gzip compressed data, was "data9.bin", last modified: Mon Jul 28 19:03:32 2025, max compression, from Unix, original size modulo 2^32 49
```

# Step 6
We keep moving here repeating our previous steps and finally get to the ASCII text file


```bash
bandit12@bandit:/tmp/myarch$ mv data8.bin data8.gz
bandit12@bandit:/tmp/myarch$ ls -l
total 16
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data6.bin.out
-rw-r--r-- 1 bandit12 bandit12    79 Jul 28 19:03 data8.gz
bandit12@bandit:/tmp/myarch$ gunzip data8.gz 
bandit12@bandit:/tmp/myarch$ ls -l
total 16
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data6.bin.out
-rw-r--r-- 1 bandit12 bandit12    49 Jul 28 19:03 data8
bandit12@bandit:/tmp/myarch$ file data8
data8: ASCII text
```

# Final step
We wrap up with a `cat` command to get the password

```bash
bandit12@bandit:/tmp/myarch$ ls -l
total 16
-rw-r--r-- 1 bandit12 bandit12 10240 Jul 28 19:03 data6.bin.out
-rw-r--r-- 1 bandit12 bandit12    49 Jul 28 19:03 data8
bandit12@bandit:/tmp/myarch$ cat data8 
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

- And we got the password
    - FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn