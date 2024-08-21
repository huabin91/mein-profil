# 1 Git Principles and Practice
## 1.1 About Version Control System (VCS)
### 1.1.1 Centralized Version Control System (CVCS)
<img src="https://github.com/huabin91/mein-profil/blob/main/1-Programmierkenntnisse/4-Ressource/centralized_vcs.png">

Such as Subversion, have a **single server** that contains all the versioned files, and a number of clients that check out files from that central place.

This setup offers many **advantages**. **Administrators** have **fine-grained control** over who can do what; and it's far easier to administer a CVCS than it is to deal with local databases on every client.

However, this setup also has some serious **downsides**. The most **obvious** is **the single point of failure** that the centralized server represents. If that server **goes down** for an hour, then during that hour nobody can collaborate at all or save versioned changes to anything they're working on. If the hard the central database is on becomes **corrupted**, and proper backups haven't been kept, you lose absolutely erverthing (the **entire** history of the project), except whatever **single snapshots** people happen to have on their **local machines**.

### 1.1.2 Distributed Version Control System (DVCS)
<img src="https://github.com/huabin91/mein-profil/blob/main/1-Programmierkenntnisse/4-Ressource/distributed_vcs.png">

Such as Git, clients don't just check out the latest snapshot of the files, they **fully mirror the repository**. Every checkout is really a **full backup** of all the data.

Deal pretty well with having **several remote repositories** they can **work with**. This allows you to **set up several types of workflows** that aren't possible in centralized systems.