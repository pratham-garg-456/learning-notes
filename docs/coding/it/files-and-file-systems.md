---
title: Files and File Systems
---

# Files and File Systems

## What is a file system?

When you save a file, the operating system needs to answer several questions:

- Where exactly on the disk should this data go?
- How will I find it again later?
- Who is allowed to access it?
- What type of file is it?

The **file system** is the organizational system that answers all these questions. Without it, your disk would be a massive sea of 0s and 1s with no way to find anything, like a library with books thrown on the floor instead of organized on labeled shelves.

Different operating systems developed their own file systems:

- **NTFS (New Technology File System)**: used by Windows.
    - Supports very large files and drives
    - Built-in file permissions: control exactly who can read, write, or execute each file
    - Journaling: keeps a log of changes so that if the system crashes mid-write, it can recover without corrupting data
    - Built-in encryption support
    - File compression
- **EXT4 (Fourth Extended File System)**: used by Linux.
    - Also has journaling for crash recovery
    - Very efficient with large numbers of files
    - Supports large drives and files
    - Fast and reliable for server environments
- **APFS (Apple File System)**: used by modern Macs. Optimized specifically for SSDs.
- **FAT32 / exFAT**: older, simpler file systems. Still widely used for USB drives and memory cards because virtually every operating system can read them. FAT32 has a 4GB file size limit, which is why large video files sometimes won't copy to certain USB drives.

**Compatibility matters.** This is why a drive formatted for Mac may not be readable on Windows: they speak different file system languages. IT professionals often deal with this when moving data between systems.

## How data is actually stored: blocks

When you save a file, the file system doesn't necessarily store it as one continuous chunk. It breaks the file into fixed-size pieces called **blocks** (sometimes called clusters) and scatters them across available spaces on the disk.

Think of parking in a busy city. Instead of needing one giant empty lot for all your vehicles, you park each car in whatever individual space is available, and you keep a map of where each car is parked.

The file system keeps a similar map: a table that records which blocks belong to which file and in what order. When you open a file, the OS consults this map, collects all the blocks from wherever they're scattered, and reassembles the complete file.

**Why scatter blocks instead of keeping files together?** Imagine files A, B, and C stored consecutively. You delete B, leaving a gap. If a new file D is larger than that gap, it can't fit in one piece, so it gets split across the gap and whatever other free space exists. This happens constantly as files are created, modified, and deleted. Storing in blocks embraces this reality:

- no space is wasted waiting for a perfectly sized gap,
- disk space is used much more efficiently,
- files can grow without needing to move entirely.

## Fragmentation

Scattering blocks has a downside on HDDs called **fragmentation**. When a file's blocks are spread far apart on a spinning platter, the read arm has to physically travel to many locations to collect them, slowing access.

This is why older Windows computers had **Disk Defragmenter**, which reorganized blocks so each file's pieces were stored consecutively, reducing the read arm's travel time.

SSDs don't have this problem: with no physical movement, it doesn't matter where blocks are located. Accessing block 1 and block 1,000,000 takes exactly the same time. Defragmenting an SSD is unnecessary and actually harmful, because it causes unnecessary write cycles that wear the drive out faster.

## File metadata

Every file has two parts:

- the actual data (the content: the pixels of a photo, the text of a document),
- the metadata (information about the file).

Metadata is stored separately from the file's content and includes:

- **Creation date**: when the file was first made.
- **Modification date**: when the file was last changed. This is what Windows shows in File Explorer by default. Important when figuring out what changed and when.
- **Access date**: when the file was last opened, even if not changed.
- **File size**: how many bytes the content takes up.
- **Access permissions**: who is allowed to do what with this file. In NTFS, for example:
    - Read only: can open but not change
    - Read/write: can open and modify
    - Execute: can run as a program
    - No access: completely blocked

  This is fundamental to IT security: controlling who can access what files on a system.
- **File owner**: which user account created or owns the file.

**Analogy:** think of a book in a library. The content is the text inside the book. The metadata is the library catalog card: the title, author, date acquired, which shelf it's on, whether it's checked out, and who's allowed to borrow it. The catalog card isn't the book; it's information about the book.

## File extensions

A file extension is the short suffix after a dot in a filename (`.jpg`, `.mp3`, `.pdf`, `.exe`). It tells both the OS and users what type of content the file contains and what program should open it.

- `.jpg` / `.png`: image files
- `.mp3` / `.wav`: audio files
- `.mp4` / `.mov`: video files
- `.pdf`: document
- `.exe`: executable program (Windows)
- `.txt`: plain text
- `.docx`: Microsoft Word document
- `.xlsx`: Microsoft Excel spreadsheet

**The extension is just a label, not a guarantee.** You could rename a `.jpg` to `.txt` and the file itself doesn't change; only the label does. Windows would try to open it in Notepad and show garbage, but the underlying image data is still there. This matters for IT because:

- Malware sometimes hides behind innocent-looking extensions (a virus named `invoice.pdf.exe`).
- File recovery tools look at the actual data structure inside the file, not the extension, to identify what type of file it really is.
- Sometimes a file won't open simply because the extension is wrong, and renaming it fixes it instantly.

**Windows hides extensions by default**, which is a security concern because you can't see whether a file is really `document.pdf` or `document.pdf.exe`. IT professionals always enable "show file extensions" in Windows settings.

## Why IT professionals need to understand file systems

- **Data recovery**: when files are deleted, the blocks aren't immediately erased, just marked as available. Recovery tools scan the disk for block patterns that match known file types.
- **Cross-platform work**: moving drives between Windows, Mac, and Linux requires knowing which file systems each can read and write. Sometimes you need to reformat or use specific tools.
- **Permissions troubleshooting**: a very common IT ticket is "I can't access this file or folder". Understanding metadata permissions lets you diagnose and fix access issues quickly.
- **Performance issues**: understanding fragmentation and block storage helps diagnose why a system might be running slowly.

## Summary table

| Concept | What it is | Why it matters |
| --- | --- | --- |
| File system | Organizational system for disk data | Without it data is unreadable chaos |
| NTFS | Windows file system | Permissions, journaling, encryption |
| EXT4 | Linux file system | Efficient, reliable, journaling |
| FAT32/exFAT | Universal simple file system | Compatible with all OS, used for USB drives |
| Blocks | Fixed-size data chunks | Efficient use of disk space |
| Fragmentation | Blocks spread far apart | Slows HDDs, irrelevant for SSDs |
| Metadata | Information about a file | Permissions, dates, ownership |
| File extension | Type label after the dot | Tells the OS what program opens the file |

## Practice Questions

??? question "1. What questions does a file system answer, and what would happen without one?"

    Where to put data on disk, how to find it again, who may access it, and what type of file it is. Without it the disk would be a sea of 0s and 1s with no way to find anything.

??? question "2. What are the main features of NTFS and EXT4?"

    NTFS (Windows): very large files and drives, permissions, journaling, encryption, and compression. EXT4 (Linux): journaling, efficiency with many files, large drives and files, reliable for servers.

??? question "3. Why do USB drives often use FAT32 or exFAT, and what is the FAT32 limitation?"

    Virtually every operating system can read them. FAT32 has a 4GB file size limit, so large video files sometimes won't copy.

??? question "4. What are blocks and why are they scattered?"

    Fixed-size pieces of a file. Files are scattered across whatever spaces are free, with a table mapping blocks to files, so no space is wasted waiting for a perfectly sized gap and files can grow without moving.

??? question "5. What is fragmentation, and why doesn't it matter on an SSD?"

    Blocks spread far apart on an HDD make the read arm travel more, slowing access. An SSD has no moving parts, so any block takes the same time to reach. Defragmenting an SSD is harmful because it adds needless write cycles.

??? question "6. What is file metadata?"

    Information about a file stored separately from its content: creation, modification, and access dates, size, access permissions, and owner.

??? question "7. Why is a file extension only a label, and why does that matter for security?"

    Renaming `.jpg` to `.txt` doesn't change the data, only the label. Malware can hide as `invoice.pdf.exe`, and Windows hides extensions by default, so IT professionals enable showing file extensions.

??? question "8. What happens to data when a file is deleted, and how does recovery work?"

    The blocks aren't erased immediately, just marked as available. Recovery tools scan the disk for block patterns that match known file types.
