<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Prerequisite: AWS Fundamentals for EC2 Storage](#prerequisite-aws-fundamentals-for-ec2-storage)
- [Overview of Elastic Block Store (EBS)](#overview-of-elastic-block-store-ebs)
- [EBS Snapshots](#ebs-snapshots)
- [Amazon Machine Images (AMI)](#amazon-machine-images-ami)
- [EC2 Instance Store](#ec2-instance-store)
- [EBS Volume Types](#ebs-volume-types)
- [EBS MultiAttach](#ebs-multiattach)
- [Elastic File System (EFS)](#elastic-file-system-efs)
- [Comparing EFS and EBS](#comparing-efs-and-ebs)
- [References](#references)

---

# Prerequisite: AWS Fundamentals for EC2 Storage
Before delving into EC2 storage options, review basic storage concepts, especially the distinction between file, block, and object storage.

- **File Storage**: Organizes data in a directory structure for easy access and sharing among instances, ideal for multiple applications that require access to the same data.
- **Block Storage**: Divides data into blocks, each accessible as an independent unit, suitable for applications requiring high-performance data access.
- **Object Storage**: Data is stored in discrete objects with metadata, suitable for unstructured data, such as media files and backups.

Understanding these types will help you determine which EC2 storage solution is best for specific workloads.

# Overview of Elastic Block Store (EBS)
- **Definition**: EBS is a high-performance block storage service that provides persistent data storage for EC2 instances.
- **Key Features**:
  - **Persistent Storage**: Data is retained after instance stops or restarts.
  - **Zonal Storage**: EBS volumes are AZ-specific, and data transfer is efficient within the AZ.
  - **EBS-Optimized Instances**: Boost performance by dedicating bandwidth for EBS, reducing network contention.
  - **Encryption**: Data can be encrypted with AWS Key Management Service (KMS) for security.
- **Storage Configuration**:
  - **Volume Size**: Ranges from 1 GB to 16 TB, with different volume types based on performance needs.
  - **Snapshots**: Backup mechanism for EBS volumes, stored in S3 for redundancy.
- **Use Cases**: Ideal for running databases, critical workloads, and root filesystems that require frequent and quick data access.

# EBS Snapshots
- **Purpose**: Snapshots capture incremental backups of EBS volumes, allowing for efficient storage and easy volume restoration.
- **Snapshot Types**:
  - **Standard Snapshots**: Incremental, with only modified data blocks stored since the last snapshot.
  - **Fast Snapshot Restore (FSR)**: Allows pre-warming of snapshots to achieve low-latency restores.
- **Key Features**:
  - **Cross-Region & Cross-Account Sharing**: Snapshots can be shared across regions and accounts for data replication and disaster recovery.
  - **Lifecycle Policies**: AWS Data Lifecycle Manager can automate snapshot creation and retention.
  - **Storage Efficiency**: Only incremental changes are stored, optimizing space and costs.
- **Use Cases**: Useful for backups, restoring volumes, and creating volume templates.

# Amazon Machine Images (AMI)
- **Purpose**: An AMI provides a pre-configured environment to quickly deploy EC2 instances with specific OS, applications, and configuration data.
- **Types of AMIs**:
  - **EBS-Backed AMI**: Boots from an EBS volume; data persists between stops and starts.
  - **Instance Store-Backed AMI**: Boots from instance store; data is ephemeral and lost on instance stop.
- **Components**:
  - **Root Volume**: Contains the OS and applications for the instance.
  - **Permissions**: AMIs can be shared across accounts or made public for community use.
- **Use Cases**: Frequently used for launching similar instances quickly, setting up test environments, or deploying instances with specific configurations.

# EC2 Instance Store
- **Overview**: Instance store provides temporary, ephemeral storage physically attached to an EC2 instance, with fast, high-throughput local storage.
- **Important Characteristics**:
  - **Data Volatility**: Data is lost when instances are stopped, rebooted, or terminated.
  - **Performance**: High I/O operations suitable for temporary data and cache.
  - **Ideal for Temporary Data**: Instance store is perfect for applications requiring fast data access without data persistence.
- **Example Use Cases**: Caching, scratch data, buffer storage, and stateless workloads that can regenerate lost data.

# EBS Volume Types
- **Types and Features**:
  - **General Purpose SSD (gp2/gp3)**: Balanced for common workloads, with consistent performance.
  - **Provisioned IOPS SSD (io1/io2)**: High IOPS, for latency-sensitive applications like high-performance databases.
  - **Throughput Optimized HDD (st1)**: Best for large sequential workloads, e.g., big data and log processing.
  - **Cold HDD (sc1)**: Lowest-cost storage for infrequently accessed data.
- **Performance Benchmarks**:
  - **gp3**: Provides cost-effective performance; allows provisioning of IOPS and throughput.
  - **io2**: Suitable for mission-critical applications with durability of 99.999%.
- **Use Cases**: Choose volume type based on workload needs – **gp3** for general apps, **io2** for high-performance databases, **st1** for large data processing, and **sc1** for infrequent access.

# EBS MultiAttach
- **Overview**: EBS MultiAttach allows a single io2 volume to be attached to multiple EC2 instances within the same AZ, enabling shared data access.
- **Key Points**:
  - **Read-Write Access**: Multiple instances can read/write to the volume, but applications need to handle concurrency.
  - **Limitations**: Only io2 volumes support MultiAttach, and instances must be in the same AZ.
  - **Use Cases**: Clustered applications, distributed data processing, or complex concurrent workflows.

# Elastic File System (EFS)
- **Purpose**: EFS provides scalable, managed file storage accessible from multiple EC2 instances, ideal for high concurrency.
- **Features**:
  - **Elastic Scaling**: Automatically scales to petabyte-scale capacity.
  - **Multi-AZ**: EFS data is available across multiple AZs within a region.
  - **Throughput Modes**: Burst mode for variable workloads and provisioned mode for consistent performance.
  - **Storage Classes**: Standard for frequently accessed data, Infrequent Access (IA) for cost efficiency with less-frequent access.
  - **Security**: Offers VPC integration, IAM policies, and encryption.
- **Use Cases**: Suitable for web servers, content management systems, and shared data repositories.

# Comparing EFS and EBS
| Feature                | Amazon EBS                         | Amazon EFS                            |
|------------------------|------------------------------------|---------------------------------------|
| **Storage Type**       | Block storage                     | NFS-based file storage                |
| **Accessibility**      | Single AZ (except MultiAttach)    | Region-wide, Multi-AZ                 |
| **Data Persistence**   | Data persists upon instance termination | Persistent across multiple instances within a region |
| **Use Cases**          | High-performance apps, databases, root volumes | High-concurrency needs, shared storage for content or web applications |
| **Backup**             | Supports EBS Snapshots            | Supports EFS backup with AWS Backup   |
| **Pricing**            | Based on volume type and size     | Usage-based, scales with data stored  |

---

# References
- [AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)