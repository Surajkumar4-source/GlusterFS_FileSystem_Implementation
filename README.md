# Introduction to GlusterFS

**GlusterFS is a highly scalable and distributed file system that allows you to aggregate storage resources from multiple machines into a single, unified storage pool. This means it can combine storage across multiple servers, offering a seamless storage solution for large-scale environments. GlusterFS is designed to scale horizontally, meaning you can add more nodes (servers) as needed to accommodate increasing data storage needs. This makes it an excellent choice for cloud environments, big data processing, and applications requiring high availability and redundancy.**

## Key Features of GlusterFS

- **Scalability:** One of the main features of GlusterFS is its ability to scale out. As data storage requirements grow, administrators can simply add more servers to the system. GlusterFS distributes data across multiple servers, allowing it to scale efficiently while maintaining high availability.

- **High Availability and Fault Tolerance:** GlusterFS ensures data availability even in the event of hardware or network failures. This is achieved through replication and redundancy, ensuring that data remains accessible at all times.

- **Elasticity:** GlusterFS adapts to changing demands. It can grow and shrink as necessary, making it a dynamic solution for storage management.

- **Data Integrity and Consistency:** GlusterFS uses strong consistency models and data integrity mechanisms to ensure that data is not corrupted and remains consistent across the distributed system.


## Use Cases

- **Cloud Storage Solutions:** GlusterFS is often used in cloud storage systems, where scalability and high availability are critical.

- **Big Data Applications:** It is ideal for storing and managing large datasets, often found in big data analytics, machine learning, and scientific computing.

- **Disaster Recovery:** With geo-replication features, GlusterFS provides a means to ensure data is backed up across geographically distributed locations.

- **Content Delivery:** As a distributed file system, GlusterFS can be used for high-performance content delivery systems, ensuring rapid access to large volumes of data.


<br>


## Core Concepts of GlusterFS

**Before delving into the installation and configuration of GlusterFS, it's crucial to understand its core components and concepts.**

## 1. Volumes
   
*In GlusterFS, a volume is a logical storage unit that is made up of one or more bricks (directories on different machines). Volumes are the key abstraction in GlusterFS and represent the shared storage that users or clients access. A volume can span multiple nodes, and it is essentially how data is organized and managed across the distributed system.*

## Types of Volumes:

- **Distributed Volume: This volume type distributes data across multiple servers, increasing storage capacity without redundancy. While this type allows for efficient scaling, it does not provide fault tolerance or redundancy.**
  
- **Replicated Volume:** Data is replicated across two or more servers to ensure redundancy and high availability. This type is ideal for scenarios where uptime and data availability are critical.
  
- **Striped Volume:** In this type of volume, data is divided into fixed-size blocks and distributed across multiple servers. This increases performance, especially for read/write-intensive applications.

- **Distributed-Replicated Volume:** A combination of distributed and replicated volumes, this type offers both scalability and redundancy. Data is distributed across multiple servers, and each piece of data is replicated for fault tolerance.

- **Geo-replication:** This advanced feature allows you to replicate volumes across geographically separated locations, ensuring disaster recovery capabilities and improved data availability in different regions.


## 2. Bricks

*A brick is the fundamental unit of storage in GlusterFS. A brick is simply a directory on a specific server that GlusterFS uses to store data. A volume in GlusterFS is made up of one or more bricks, and each brick is hosted on a different server (or node) in the system. Each brick is managed independently, but collectively, they form the storage pool of the system.*

## 3. Cluster

*A GlusterFS cluster is a collection of nodes that participate in managing storage. Each node in a GlusterFS cluster serves one of two roles:*

- **Server (Storage Node):** This is the node that hosts the physical or virtual storage, where the data is actually written and read. The server manages the bricks and their respective volumes.
  
- **Client (Access Node):** This is the node that accesses the shared storage, usually to perform read/write operations. Clients interact with the GlusterFS volumes to access the data.

  *A cluster can scale by adding more servers, which automatically extends the available storage and increases redundancy.*







  

# Advanced Concepts in GlusterFS

### 1. Consistency Models

*GlusterFS offers a consistency model for data across its distributed environment. It ensures that all clients see the same data when they access it. GlusterFS uses the replication feature to maintain data consistency across multiple nodes. There are two types of consistency models that GlusterFS supports:*

   - Strong Consistency: Data is consistent and up-to-date across all replicas. This means that every client always sees the most recent write to the system.

   - Eventual Consistency: This model allows for slight delays in data replication, but over time, all replicas will converge to the same state.

### 2. Self-Healing

*GlusterFS has a built-in self-healing mechanism that automatically repairs corrupted or missing data from replicas. This is crucial in environments where fault tolerance and uptime are essential. If a server fails or a brick becomes inaccessible, GlusterFS ensures that the data from the affected brick is reconstructed from its replica, making the system resilient to hardware or network failures.*

### 3. Geo-replication and Disaster Recovery

*For organizations with multiple data centers or geographically dispersed systems, geo-replication is a key feature of GlusterFS. It enables replication of data across different geographic regions to ensure data durability and provide disaster recovery capabilities. This is particularly beneficial for businesses operating across different regions or for cloud services that require high availability.*

### 4. Data Access Methods

*GlusterFS supports a range of data access methods, including:*

   - POSIX File System Interface: Clients access data through standard file system protocols (e.g., NFS, SMB), making GlusterFS compatible with many existing applications.

   - GlusterFS Native Protocol: GlusterFS also provides its own client-side protocol for more optimized access to storage.*

### 5. Performance Optimization

*GlusterFS includes several features to optimize performance in distributed environments:      

   - Load Balancing: The system automatically balances data across bricks, helping to ensure that no single node becomes overwhelmed.*

   - Caching: GlusterFS can cache frequently accessed data to improve read performance.

   - Tuning and Performance Metrics: Administrators can monitor and tune performance parameters, such as I/O threads, read/write sizes, and more, to match the system’s usage patterns.

### 6. Advanced Security Features

*GlusterFS provides several security measures to ensure safe and secure data access:*

   - Encryption: Data can be encrypted both in transit and at rest to prevent unauthorized access.

   - Access Control Lists (ACLs): ACLs allow granular control over which users or systems can access specific volumes or bricks.

## Key Point

*GlusterFS is a powerful, scalable, and highly available distributed file system that meets the needs of large-scale environments, including cloud storage, big data analytics, and disaster recovery. With its advanced features such as geo-replication, self-healing, and strong consistency models, GlusterFS is a critical tool for businesses and organizations that require reliable and efficient storage solutions. By understanding its core components and advanced capabilities, users can make the most of GlusterFS in their environments and optimize their storage infrastructure to meet evolving demands.*


<br>
<br>


**After implementing Both GlusterFS and NFS (Network File System) in my environment ,both allow files to be created on one node and made visible across all other nodes, making them both useful for sharing files in a distributed environment. However, while they serve a similar purpose of file sharing, GlusterFS and NFS are fundamentally different in terms of architecture, features, scalability, and use cases. I have implemented both GlusterFS and NFS, and here are the key differences between them:**


## 1. Architecture:

- NFS (Network File System):
    - **Centralized Server-Based Architecture:** NFS operates on a client-server model, where one server (the NFS server) provides file access to multiple clients. Clients access files on the server over a network.
    - **Single Server Focus:** The NFS server holds the file system, and clients mount the NFS share from this central server.

    - **Scale:** NFS typically scales by adding more NFS servers, but managing many servers can become complex and the performance might degrade as the number of clients increases.


- GlusterFS:

    - **Distributed Clustered File System:** GlusterFS uses a distributed architecture with multiple storage nodes (also called "bricks") that are pooled together to create a single logical volume.

    - **Decentralized & Fault-Tolerant:** GlusterFS is designed to be fault-tolerant. It spreads data across multiple nodes (distributed volume), and if one node goes down, the data remains accessible from other nodes (replicated volume).
    - **Scale:** GlusterFS is built to scale horizontally by simply adding more nodes to the cluster. As you add nodes, the system can handle more clients and data more efficiently.

### 2. Data Availability & Redundancy:

- NFS:

    - **Single Point of Failure:** If the NFS server goes down, the entire file system becomes inaccessible. You would need to set up complex failover solutions (like NFS replication, HA clusters) to achieve high availability, which isn’t inherent in NFS itself.

- GlusterFS:
    - **High Availability & Redundancy Built-In**: GlusterFS provides built-in data redundancy with features like replication (data is replicated across multiple servers) and distributed volume (data is spread across multiple servers). Even if a server goes down, GlusterFS can continue to serve the data from other replicas, ensuring higher availability and fault tolerance.

    - **Self-Healing:** If a file is deleted or corrupted on one brick, GlusterFS will automatically replicate and heal the file across other bricks to maintain consistency.

### 3. Performance:

- NFS:

    - **Limited Scalability:** NFS performance can degrade with a high number of clients or very large amounts of data. NFS is designed to work best in smaller to moderate-sized environments, and scaling it effectively requires additional infrastructure (like load balancing or clustered NFS servers).

    - **Single Server Bottleneck:** The NFS server can become a bottleneck when handling a high volume of file requests.

- GlusterFS:

    - **Horizontal Scalability:** GlusterFS allows for easy horizontal scaling. By adding more servers (bricks), you increase both the storage capacity and the performance, distributing the load across the cluster.

    - **Better Performance in Large Scale**: Due to its distributed nature, GlusterFS can handle large volumes of data and a large number of clients more efficiently than NFS.


### 4. Flexibility & Features:

- NFS:

    - **Simple & Mature Protocol:** NFS is simple to set up and has been in use for a long time. It’s well-supported in almost all environments.

    - **Single Protocol for File Sharing:** NFS primarily provides a network file-sharing protocol, but it lacks some advanced features for managing distributed data.

- GlusterFS:

    - **Advanced Features:** GlusterFS offers advanced features such as:
          - **Data Replication:** Ensures multiple copies of data exist across different servers.
          - **Distributed Volumes:** Spreads data across multiple nodes to increase performance and storage capacity.

        - **Striped Volumes:** Distributes files across multiple servers for faster read/write operations.

         - **Geo-Replication:** Provides data replication across geographically distributed sites.

         - **Arbiter Volumes:** A special volume type to handle quorum-based decisions in a replicated setup, which can prevent data corruption during network partitions.

### 5. Use Cases:

- NFS:
    **Best suited for:**

     - Simple network file sharing in smaller to mid-sized environments.

     - Situations where you need a central server and clients need to mount shared directories.

     - Environments where fault tolerance is not a high priority, and failover mechanisms are implemented externally.

- GlusterFS:

   **Best suited for:**

     - Large-scale environments requiring high availability, fault tolerance, and easy horizontal scaling.
         
     - Scenarios where the need for distributed data storage, redundancy, and performance across multiple nodes is a priority.
       
     - Applications that need a flexible, fault-tolerant storage system with features like replication, geo-replication, and self-healing.

### 6. Data Access:

- NFS:
        - **File-Level Access:** NFS provides file-level access to data. Clients can read and write files over the network. Each client directly accesses files stored on the NFS server.
        - **Access Control:** NFS uses UID/GID (User/Group IDs) for access control, which can be limiting in complex setups.

- GlusterFS:

    - **File-Level and Block-Level Access:** GlusterFS can provide both file-level and block-level access, offering more flexibility depending on the application.

        - **Access Control:** GlusterFS allows for more advanced access control mechanisms and can be tightly integrated with other systems for authentication and authorization.

### 7. Ease of Setup:

- NFS:
        - **Easier to Set Up:** NFS is easier to set up for simple use cases, especially when there’s only one server involved and basic file sharing is needed.
        - **Less Complex:** NFS does not require as much configuration as GlusterFS for basic file-sharing needs.

- GlusterFS:
      - **More Complex Setup:** GlusterFS can be more complex to set up, especially if you are configuring distributed or replicated volumes.

     - **Requires More Resources: Because it involves multiple nodes and complex configurations, setting up a GlusterFS cluster requires more planning and resources.


<br>


### Summary of Differences:

# NFS vs. GlusterFS: Feature Comparison

| **Feature**          | **NFS**                                      | **GlusterFS**                                        |
|-----------------------|----------------------------------------------|-----------------------------------------------------|
| **Architecture**      | Centralized (client-server)                 | Distributed (cluster of nodes)                     |
| **Data Redundancy**   | Not built-in (needs extra setup for HA)      | Built-in (data replication, fault tolerance)       |
| **Scalability**       | Limited scalability with more clients        | Horizontal scalability with more nodes             |
| **Performance**       | Can be a bottleneck at scale                 | High performance in large, distributed environments|
| **Fault Tolerance**   | Limited (requires external solutions)        | Built-in fault tolerance and self-healing          |
| **Use Case**          | Small to medium file sharing                | Large-scale, distributed storage, high availability|
| **Advanced Features** | Basic file sharing                          | Advanced features like geo-replication, striping, self-healing |






## Key Points:

- **NFS** is great for simple, centralized file sharing where high availability and scalability aren't critical.

- **GlusterFS** is a more powerful, scalable solution for large environments where high availability, fault tolerance, and redundancy are crucial.

*If you need more advanced features like data replication, fault tolerance, scalability, and geo-replication, GlusterFS is the better choice. For simpler file sharing with less overhead, NFS is often sufficient.*





<br>

<br>



#  ********************* Implemenytation *********************



<br>



*Before you begin the GlusterFS setup on your Ubuntu nodes (controller, compute1, compute2), ensure the following prerequisites are met. These prerequisites will ensure smooth installation and configuration:*

### 1. Virtual Machines or Physical Machines (Nodes)

- **Three nodes:** You need at least three nodes (VMs or physical machines) for this setup:
      - **Controller:** This node will manage the cluster.
      - **Compute1 and Compute2:** These nodes will participate in the GlusterFS cluster as data storage nodes.

*The nodes should have access to each other over the network (i.e., they should be able to ping each other).*

### 2. Ubuntu Installation

   - Each node should have a clean installation of Ubuntu 20.04 LTS or Ubuntu 22.04 LTS (or any similar version).
   - Ensure that you have a non-root user with sudo privileges on each node for running commands.

### 3. Network Configuration

- **Static IP addresses:** Each node must have a static IP address so that the GlusterFS cluster can reliably connect between nodes.
  
  *Example:*

```yml
  
Controller: 192.168.82.244
Compute1: 192.168.82.63
Compute2: 192.168.82.50

```
   - Ensure that these IPs are correctly mapped to hostnames in the /etc/hosts file for easy identification.
   - The nodes must be able to ping each other. Run ping between the nodes to ensure network connectivity is working.






### 4. Firewall Configuration

**Firewall (ufw):** If you have the Uncomplicated Firewall (ufw) enabled on any of the nodes, it should be disabled temporarily during setup:

```yml
sudo ufw disable
```


   - Ports for GlusterFS: Later, you will need to open specific ports in the firewall for GlusterFS. These ports include:

      - TCP ports 24007, 24008, and 24009 for GlusterFS communication.
      - TCP/UDP ports in the range 49152-49251 for GlusterFS brick communication.

### 5. Additional Disk for GlusterFS Storage (Optional)

*If you are using GlusterFS as a distributed storage solution, you will need at least one additional disk per node for the GlusterFS volume storage. This disk should be unformatted (or you can use an existing disk) and should be mounted to a directory where the GlusterFS volume will be created.*

   - For example, you may have /dev/sdb attached to each node, and you will format it and mount it to /mnt/disk1.

   - You can check for available disks on each node by running:

```yml
lsblk
```

### 6. Sufficient Resources
- Ensure that each node has enough resources (CPU, RAM, disk space) to handle GlusterFS:
      - Minimum RAM: 2GB per node.
      - Minimum CPU: 1 CPU core per node.
      - Disk Space: At least 10GB available for GlusterFS data.

- GlusterFS performance depends on hardware and disk configuration, so adequate resources will ensure smoother operation.

### 7. Root or Sudo Privileges

- Sudo or root access on all the nodes is required to perform administrative tasks such as installing packages, configuring system files, and managing services.

### 8. Internet Access

- Each node will need internet access to download the necessary packages and updates (e.g., apt for installing GlusterFS).

### 9. GlusterFS Version Compatibility

- Make sure the GlusterFS version is compatible across all nodes. In the steps provided, we are installing GlusterFS 10, but if you are using a different version, the commands may differ slightly.
      - To ensure compatibility, use the same GlusterFS version across all nodes.




<br>

<br>



#  ************  Step-by-Step Inmplementation  ****************


<br>











### Step 1: Modify /etc/hosts on All Nodes

- Modify the /etc/hosts file to include the IPs and hostnames of the nodes. Run this on each node (controller, compute1, compute2).

- On controller, compute1, and compute2, open the /etc/hosts file and add the following lines:

```yml
sudo nano /etc/hosts
```

   - Add these entries, adjusting for the respective IPs and hostnames:

```yml

192.168.82.244   controller

192.168.82.63    compute1
                                       # In my case change IP  acc. to your machine
192.168.82.50    compute2

```


### Step 2: Disable the Firewall (ufw) on All Nodes

- Ubuntu uses ufw for firewall management. Disable it on all nodes for now (you can configure it later, once the setup is confirmed to work).

```yml
sudo ufw disable
```



### Step 3: Install GlusterFS on All Nodes
   - Run these commands on all nodes (controller, compute1, and compute2):

```yml
# Update the package list
sudo apt update

# Install required dependencies
sudo apt install -y software-properties-common

# Add GlusterFS repository
sudo add-apt-repository ppa:gluster/glusterfs-10

# Update the package list again
sudo apt update

# Install GlusterFS server and client
sudo apt install -y glusterfs-server glusterfs-client

```





### Step 4: Start and Enable GlusterFS Service on All Nodes
   - Run the following commands on all nodes to start the GlusterFS service and enable it to start on boot:

```yml

sudo systemctl start glusterd

sudo systemctl enable glusterd

```

### Step 5: Check Network Connectivity Between Nodes

   - Make sure all nodes can communicate with each other.


```yml

# From controller, run:

ping compute1
ping compute2

# From compute1, run:


ping controller
ping compute2

# From compute2, run:


ping controller
ping compute1

```




   *If there are any connectivity issues, verify the network configuration and ensure the nodes are in the same subnet and can reach each other.*



### Step 6: Add Peers to the GlusterFS Cluster

   - Now, let's add the nodes as peers to the GlusterFS cluster. Run these commands on the controller node.

```yml

# Add compute1 and compute2 to the cluster

sudo gluster peer probe compute1
sudo gluster peer probe compute2

```

 - **Check the peer status to ensure all nodes are connected:**

```yml
sudo gluster peer status
```


### Step 7: Prepare the Disks for GlusterFS Volume


*On each node, you'll need to create a directory for storing the GlusterFS volume and format the disk (/dev/sdb) if it isn't already formatted. Run these commands on controller, compute1, and compute2.*

- **Create a Partition on /dev/sdb:** You need to partition the disk /dev/sdb before creating a filesystem on it. You can use fdisk or parted to create a partition.

   **Using fdisk:**

```yml
sudo fdisk /dev/sdb
```

   - Type n to create a new partition.
   - Choose the partition number (usually 1 for the first partition).
   - Accept the default first and last sectors (or define the size if necessary).
   - Type w to write the partition table and exit.

- **Verify the Partition:** After partitioning, check that /dev/sdb1 exists:

```yml
lsblk
```
   *You should see /dev/sdb1 listed as a partition under /dev/sdb.*
   
- **Format the Partition with XFS:** Once /dev/sdb1 is created, you can format it with XFS:

```yml
sudo mkfs.xfs /dev/sdb1
```

- **Mount the Partition:** After formatting, you can mount the partition:

```yml

sudo mkdir /mnt/disk1
sudo mount /dev/sdb1 /mnt/disk1

```


- **Check the Mounted Filesystem:** To confirm that the filesystem is mounted correctly:

```yml
df -h
```

   **Summary:**
- Partition /dev/sdb using fdisk to create /dev/sdb1.
- Format /dev/sdb1 with mkfs.xfs.
- Mount the formatted partition to a directory, e.g., /mnt/disk1.
   *By following these steps, you should be able to partition and format the disk correctly.*





### Step 8: Create the GlusterFS Volume

- *You will create the GlusterFS volume on any node (for example, the controller node). This volume will be replicated across the three nodes.*

   - Run this command on the controller node to create the volume:

```yml

sudo gluster volume create gdisk1 replica 3 \
compute1:/mnt/disk1/gdisk1 \
compute2:/mnt/disk1/gdisk1 \
controller:/mnt/disk1/gdisk1

```

### Step 9: Start the GlusterFS Volume
   - Once the volume is created, start it with the following command on the controller node:

```yml
sudo gluster volume start gdisk1
```

### Step 10: Verify the GlusterFS Volume

   - You can check the volume status and details with:

```yml
sudo gluster volume info gdisk1
```



### Step 11: Mount the GlusterFS Volume on the Client Node
  - *Now, let's mount the GlusterFS volume on the controller node (this can also be done on compute1 or compute2, if you prefer).*

      - Install the GlusterFS client on the controller node (if it’s not already installed):

```yml
sudo apt install -y glusterfs-client
```

   - Create a mount point directory:

```yml
sudo mkdir /mnt/gdrive
```

   - Mount the GlusterFS volume:

```yml
sudo mount -t glusterfs controller:/gdisk1 /mnt/gdrive
```





### Step 12: Test the Volume
   *To ensure everything is working correctly, test the volume by creating a test file:*


```yml

# Create a test file in the mounted volume
sudo touch /mnt/gdrive/suraj.txt

# List the files to verify
sudo ls -l /mnt/gdrive

```

   *If you see testfile in the output, then the GlusterFS volume is mounted and functioning correctly.*





## Step 13: (Optional) Configure Firewall Rules

*After verifying the setup, you can re-enable the firewall (ufw) and configure appropriate rules.*
   - For example, allow GlusterFS traffic on the necessary ports:

```yml

sudo ufw allow from 192.168.82.0/24 to any port 24007
sudo ufw allow from 192.168.82.0/24 to any port 24008
sudo ufw allow from 192.168.82.0/24 to any port 49152:49251

```








<br>
<br>




## Summary of Commands:

### Controller node:

   - Modify /etc/hosts to include the IPs and hostnames of all nodes.
   - Install GlusterFS server and client.
   - Disable the firewall.
   - Probe compute1 and compute2 as peers.
   - Create and start the GlusterFS volume.
   - Mount the volume on /mnt/gdrive.

### Compute1 and Compute2 nodes:
   - Modify /etc/hosts to include the IPs and hostnames of all nodes.
   - Install GlusterFS server and client.
   - Disable the firewall.
   - Format and mount the new disk.
   - Probe the controller and other compute node as peers.
   - Install the GlusterFS client (if mounting the volume on these nodes).




<br>
<br>

*************** Implementation Screnshots ******************


<br>
<br>


![1  etc  file](https://github.com/user-attachments/assets/4e4a537c-918f-4bbd-b8b9-3145c0474dca)


<br>
<br>


![3 controller](https://github.com/user-attachments/assets/082773e8-4c78-4766-9e39-7434a6a6ea93)


<br>
<br>


![3 1 compute1](https://github.com/user-attachments/assets/851dce71-b18b-4377-baff-df1c8b31a5f6)


<br>
<br>

![3 2 compute2](https://github.com/user-attachments/assets/ba7a1b28-f5be-4e25-928f-f259de1f3c11)



<br>
<br>

![output   3 ](https://github.com/user-attachments/assets/416c082d-ca62-4972-bd14-952d019778d1)



<br>
<br>

![4  lsblk  controller](https://github.com/user-attachments/assets/6ffa60bf-3955-4155-a507-987a3417698e)



<br>
<br>

![4  lsblk  compute1](https://github.com/user-attachments/assets/7b895bd1-97a0-4e68-8614-575601374ba8)



<br>
<br>

![4  lsblk  compute2](https://github.com/user-attachments/assets/9e2a9042-4084-4f5d-86f1-57932a3b8d20)



<br>
<br>

![gluster status compute1](https://github.com/user-attachments/assets/9585d659-6b60-4f74-8465-ea356e2c404d)



<br>
<br>

![gluster status compute2](https://github.com/user-attachments/assets/fd6b507b-6adc-44d0-b99f-961f4fbe504e)



<br>
<br>


![5  df -h controller](https://github.com/user-attachments/assets/821db9fa-4020-43cf-a6d5-5fdebef53713)



<br>
<br>


![5 1  df -h compute1](https://github.com/user-attachments/assets/b6ef41c3-6083-4c01-bf61-573a93a34f7d)


<br>
<br>


![5 1  df -h compute2](https://github.com/user-attachments/assets/86b832ff-824f-4407-947f-96129ac24c43)


<br>
<br>



![5 3  pool status](https://github.com/user-attachments/assets/9768b8db-67a9-4cd4-ace9-bddfd5847f80)



<br>
<br>


![5 4 gluster volume  heal status status](https://github.com/user-attachments/assets/1a3acbea-cd77-4639-b1b7-1f5bc75a1b20)


<br>
<br>



![5 5 mount  status](https://github.com/user-attachments/assets/d3380c79-671b-413b-8135-1c7c11493537)

<br>
<br>

![5 3  pool status](https://github.com/user-attachments/assets/d194f4a1-2ead-43a4-bf8f-54a86754b8b7)#

<br>
<br>


![6 gluster volume](https://github.com/user-attachments/assets/81235987-4fdb-418e-a45d-4850a72d7057)



<br>
<br>



![7 gluster volume status](https://github.com/user-attachments/assets/2bc06dd2-1442-48c2-b807-0ba87f0a5b47)

<br>
<br>


![gluster status controller](https://github.com/user-attachments/assets/961151b0-db57-4079-b8fc-30771e8a898a)


<br>
<br>


![final output](https://github.com/user-attachments/assets/0be163c3-7512-4578-9fb4-b4b0ca202b18)


<br>
<br>


![final output 2 ](https://github.com/user-attachments/assets/2d462128-0586-4a82-9f32-ac0843ad8d90)


<br>
<br>
































