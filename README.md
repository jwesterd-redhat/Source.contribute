# Source.contribute
This is meant as a vector to share with the global Redhat audience via SOURCE

Here is something I learned today.

To scale effectively, In place upgrades (AKA IPU) need to encapsulate OS upgrades inside methods that delive customers objectives.

The following must be met: 
 * Systems need to be prepared for the upgrade method (redhat-upgrade-tool for RHEL6 or leapp for RHEL7, RHEL8 and RHEL9 and beyond)
 * Services need to be quiesced to avoid data being served or collected during the in place upgrade
 * Services that compete for system resources (CPU, Memory or disk) need to be stopped and disabled during multiple reboot cycles
  
optionally:
 * File systems not on the root volume group can be unmounted

During an initial Proof of concept (POC) phase, representative systems provided by customer should reveal common technical challenges to IPU.
It will be during the first round of IPU that real world challenges will be found.

Snapshots of file systems need to provide rollback if IPU needs to be reverted to near-original state.

  * Physical servers
    - Physical Servers will need to be snapshotted with LVM (if used) or other snapshot method ( storage vendor based for example).
    - Physical servers may need to be trimmed down to only OS releated file systems in some cases

 * Virtual servers
    - Virtual servers may be snapshotted by passing snapshot requests to the hosting server via API

Snapshot functionality needs to include create, delete, revert, and status at a minimum so the managing IPU service can support a customers needs
