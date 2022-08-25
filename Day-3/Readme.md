## Shared Disk with AKS
1. [Shared Disk](https://www.youtube.com/watch?v=BRNelyXLQ4o) introduction by Azure PM.
2. How [Shared Managed Disk](https://docs.microsoft.com/en-us/azure/virtual-machines/disks-shared#premium-ssd-ranges) works.
 ```
VMs in the cluster can read or write to their attached disk based on the reservation chosen by the clustered application using SCSI Persistent Reservations (SCSI PR). SCSI PR is an industry standard used by applications running on Storage Area Network (SAN) on-premises. Enabling SCSI PR on a managed disk allows you to migrate these applications to Azure as-is.

Shared managed disks offer shared block storage that can be accessed from multiple VMs, these are exposed as logical unit numbers (LUNs). LUNs are then presented to an initiator (VM) from a target (disk). These LUNs look like direct-attached-storage (DAS) or a local drive to the VM.

Shared managed disks don't natively offer a fully managed file system that can be accessed using SMB/NFS. You need to use a cluster manager, like Windows Server Failover Cluster (WSFC), or Pacemaker, that handles cluster node communication and write locking.
 ```
3. [Max Shares Limits](https://docs.microsoft.com/en-us/azure/virtual-machines/disks-shared#premium-ssd-ranges)
4. Summary of [Storage Redundancy Options ](https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy#summary-of-redundancy-options)

## Deployment detials.
1. Refer the yaml for static and dynamic provisioning of Volumes under SharedDisk. 
2. Please note, in deployment yaml, instead of mountPath, <b>devicePath</b> is used as the volumes are presented to VM as LUN
```
    spec:
      containers:
        - name: deployment-azuredisk
          image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine
          volumeDevices:
            - name: azuredisk
              devicePath: /dev/sdx
              
```