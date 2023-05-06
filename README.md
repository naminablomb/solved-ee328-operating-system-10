Download Link: https://assignmentchef.com/product/solved-ee328-operating-system-10
<br>
<h1>Design a File System</h1>

<h2>1 PROBLEM</h2>

<h3>1.1 DESCRIPTION</h3>

Write a program that implements the file system with the simulated disk. Several methods manipulating the file system are needed to be implemented such as <em>formatDisk(), shutdown(), create(), open(), inumber(), read(), write(), seek(), close(), delete()</em>. Some data structures like <em>Disk, SuperBlock, InodeBlock, IndirectBlock </em>can be found on www.os-book.com. You can see the detail in the end of chapter 11 of <em>OPERATING SYSTEM CONCEPTS WITH JAVA (Seventh Edition)</em>, from page 481 to 487.

<h2>2 ALGORITHM</h2>

<h3>2.1 PRINCIPLES</h3>

In computing, a file system (or filesystem) is a type of data store which can be used to store, retrieve and update a set of files. The term refers to either the abstract data structures used to define files, or the actual software or firmware components that implement the abstract ideas. Some file systems are used on local data storage devices; others provide file access via a network protocol (e.g. NFS, SMB, or 9P clients). Some file systems are “virtual”, in that the “files” supplied are computed on request (e.g. procfs) or are merely a mapping into a different file system used as a backing store. The file system manages access to both the content of files and the metadata about those files. It is responsible for arranging storage space; reliability, efficiency, and tuning with regard to the physical storage medium are important design considerations.

Unix-like operating systems create a virtual file system, which makes all the files on all the devices appear to exist in a single hierarchy. This means, in those systems, there is one root directory, and every file existing on the system is located under it somewhere. Unix-like systems can use a RAM disk or network shared resource as its root directory.

Unix-like systems assign a device name to each device, but this is not how the files on that device are accessed. Instead, to gain access to files on another device, the operating system

<h4>Figure 2.1: Open A File in Unix-like system</h4>

must first be informed where in the directory tree those files should appear. This process is called mounting a file system. For example, to access the files on a CD-ROM, one must tell the operating system “Take the file system from this CD-ROM and make it appear under suchand-such directory”. The directory given to the operating system is called the mount point it might, for example, be /media. The /media directory exists on many Unix systems (as specified in the Filesystem Hierarchy Standard) and is intended specifically for use as a mount point for removable media such as CDs, DVDs, USB drives or floppy disks. It may be empty, or it may contain subdirectories for mounting individual devices. Generally, only the administrator (i.e. root user) may authorize the mounting of file systems.

<h3>2.2 OPERATIONS</h3>

<h4>2.2.1 FORMATDISK()</h4>

Here I initial the instance <em>mySuperBlock </em>of the data structure <em>SuperBlock </em>with the number of disk blocks in the file system size, the number of inode blocks <em>iSize </em>and also <em>freeList </em>which is calculated with <em>iSize </em>representing the first block on the free list. Besides, I use the instance <em>freeBlockList </em>of data structure <em>ArrayList </em>to create the linked list of the free blocks.

<h4>2.2.2 SHUTDOWN()</h4>

After writing all the block data back to the disk, I clear all the states of the <em>bitmap </em>on the file table. Then use the method <em>stop() </em>in the data structure <em>Disk </em>to shut down the simulated disk.

<h5>2.2.3 CREATE()</h5>

With the allocated file descriptor number and the initial <em>Inode</em>, I create the new filea˛´rs file descriptor in the file table.

2.2.4 OPEN()

According to the given <em>inumbers</em>, get the file descriptor to find its location.

<h4>2.2.5 INUMBER()</h4>

Get the <em>inumbers </em>with its file descriptor number.

<h5>2.2.6 READ()</h5>

First find the filea˛´rs <em>Inode </em>according to its file descriptor in the file table. Using the pointers in the <em>Inode</em>, we can find the actually location of the file on the data blocks. That is to say, the content of the pointer is the number of the data block. The first 10 pointers are pointed to the blocks directly, which is called directly block, while the remaining 3 pointers are pointed to the blocks indirectly with multi-level structure. So if the corresponding pointer is not 0, that means this pointer has pointed to a data disk. Then I use the method <em>read() </em>in the data structure <em>Disk </em>to read it out to the buffer.

<h5>2.2.7 WRITE()</h5>

Similar to <em>read()</em>, I use the <em>Inode </em>to find where I can write the data and let the pointer have the value of <em>freeList</em>, then update the free list <em>freeBlockList</em>. Attention that the pointer has a same rule described in <em>read()</em>.

2.2.8 SEEK()

According to the offset and whence, update the <em>seekPointer </em>of the specific file descriptor.

2.2.9 CLOSE()

Write the its <em>Inode </em>back to disk and then clear its state in file table.

<h5>2.2.10 DELETE()</h5>

Clear its state in file table and also release the block it takes. The released blocks will be added to the free list.

<h2>3 RESULTS</h2>

<h3>3.1 ENVIRONMENT</h3>

<ul>

 <li>Ubuntu 14.04 LTS</li>

 <li>Java Development Kit 1.8.0_131</li>

 <li>Eclipse</li>

</ul>

3.2 SCREENSHOTS OF THE RESULT

We use Linux Terminal to compile and execute the program. The result is shown in Fig. 3.1.

<h3>3.3 THOUGHTS</h3>

File system is quite complicated to comprehend while more complicated to be realized as well.

Figure 3.1: Screenshot of a File System