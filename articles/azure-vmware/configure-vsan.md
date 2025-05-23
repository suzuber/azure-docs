---
title: Configure VMware vSAN
description:  Learn how to configure VMware vSAN
ms.topic: how-to
ms.service: azure-vmware
ms.date: 12/07/2023
ms.custom: engagement-fy23

#Customer intent: As an Azure service administrator, I want to configure VMware vSAN.

---

# Configure VMware vSAN (OSA)

VMware vSAN has more capabilities that are set with every Azure VMware Solution deployment.  Each cluster has their own VMware vSAN Datastore.
Azure VMware Solution defaults with the following configurations per cluster:

   | **Field** | **Value** |
   | --- | --- |
   | **TRIM/UNMAP** | Disabled |
   | **Space Efficiency** | Deduplication and Compression |

> [!NOTE]
> Run commands are executed one at a time in the order submitted.

In this article, learn how to:

> [!div class="checklist"]
> - Enable or Disable vSAN TRIM/UNMAP
> - Enable vSAN Compression Only
> - Disable vSAN Deduplication and Compression
> - Enable or Disable vSAN Data-In-Transit Encryption

## Set VMware vSAN TRIM/UNMAP
Run the `Set-AVSVSANClusterUNMAPTRIM` cmdlet to enable or disable TRIM/UNMAP.

1. Sign in to the [Azure portal](https://portal.azure.com).

   > [!NOTE]
   > Enabling TRIM/UNMAP on your vSAN Datastore may have a negative performance impact.
   
1. Select **Run command** > **Packages** > **Set-AVSVSANClusterUNMAPTRIM**.

1. Provide the required values or change the default values, and then select **Run**.

   | **Field** | **Value** |
   | --- | --- |
   | **Name**  | Cluster name as defined in vCenter Server. Comma delimit to target only certain clusters. (Blank targets all clusters) |
   | **Enable**  | True or False. |
   | **Retain up to**  | Retention period of the cmdlet output. The default value is 60.  |
   | **Specify name for execution**  | Alphanumeric name, for example, **Disable vSAN TRIMUNMAP**.  |
   | **Timeout**  |  The period after which a cmdlet exits if taking too long to finish.  |
   
1. Check **Notifications** to see the progress.
   > [!NOTE]
   > After vSAN TRIM/UNMAP is Enabled, the following lists additional requirements for it to function as intended. Once enabled, there are several prerequisites that must be met for TRIM/UNMAP to successfully reclaim no longer used capacity.
   > - Prerequisites - VM Level
   > - A minimum of virtual machine hardware version 11 for Windows
   > - A minimum of virtual machine hardware version 13 for Linux.
   > - disk.scsiUnmapAllowed flag is not set to false. The default is implied true. This setting can be used as a "stop switch" at the virtual machine level should you wish to disable this behavior on a per VM basis and do not want to use in-guest configuration to disable this behavior. VMX file changes require a reboot to take effect.
   > - The guest operating system must be able to identify the virtual disk as thin.
   > - After enabling at a cluster level, the VM must be powered off and back on (a reboot is insufficient).
   
   > [!TIP]
   > Articles on reclaiming space for Windows and Linux systems for TRIM/UNMAP to execute.
   > -https://knowledge.broadcom.com/external/article/340005/reclaiming-disk-space-from-thin-provisio.html
   > -https://knowledge.broadcom.com/external/article/326595/procedure-to-enable-trimunmap.html
   
## Set VMware vSAN Space Efficiency

Run the `Set-vSANCompressDedupe` cmdlet to set preferred space efficiency model.
> [!NOTE]
> Changing this setting will cause a vSAN resync and performance degradation while disks are reformatted.
> Assure enough space is available when changing to a new configuration. 25% free space or greater is recommended in general.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Select **Run command** > **Packages** > **Set-vSANCompressDedupe**.

1. Provide the required values or change the default values, and then select **Run**.

   | **Field** | **Value** |
   | --- | --- |
   | **Compression**  | True or False.|
   | **Deduplication**  | True or False. (Enabling deduplication, enables both dedupe and compression).|
   | **ClustersToChange**  | Cluster name as defined in vCenter Server. Comma delimit to target multiple clusters.|
   | **Retain up to**  | Retention period of the cmdlet output. The default value is 60.|
   | **Specify name for execution**  | Alphanumeric name, for example, **set cluster-1 to compress only**.|
   | **Timeout**  | The period after which a cmdlet exits if taking too long to finish.|
   
   > [!NOTE]
   > Setting Compression to False and Deduplication to True sets vSAN to Dedupe and Compression.
   > Setting Compression to False and Dedupe to False disables all space efficiency.
   > Azure VMware Solution default is Dedupe and Compression.
   > Compression only provides slightly better performance.
   > Disabling both compression and deduplication offers the greatest performance gains, however at the cost of space utilization.
   
1. Check **Notifications** to see the progress.


## Set VMware vSAN Data-In-Transit Encryption

Run the `Set-vSANDataInTransitEncryption` cmdlet to enable or disable data-in-transit encryption for all clusters or specified clusters of an SDDC.

> [!NOTE]
> Changing this setting will cause a performance impact. See [VMware KB](https://blogs.vmware.com/virtualblocks/2021/08/12/storageminute-vsan-data-encryption-performance/).

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Select **Run command** > **Packages** > **Set-vSANDataInTransitEncryption**.

1. Provide the required values or change the default values, and then select **Run**.

   | **Field** | **Value** |
   | --- | --- |
   | **ClusterName**  | Name of the cluster. Leave blank if required to enable for whole SDDC else enter comma separated list of names. |
   | **Enable**  | Specify True/False to Enable/Disable the feature.|
   
1. Check **Notifications** to see the progress.

>[!NOTE]
>You can also use the `Get-vSANDataInTransitEncryptionStatus` command to check for the current status or status after performing the `Set-vSANDataInTransitEncryptionStatus` operation and verify the cluster's current encryption state.

## Next steps

Now that you learned how to configure VMware vSAN, learn more about:

- [How to configure storage policies](configure-storage-policy.md) - Create and configure storage policies for your Azure VMware Solution virtual machines.

- [How to configure external identity for vCenter Server](configure-identity-source-vcenter.md) - vCenter Server has a built-in local user called cloudadmin and assigned to the CloudAdmin role. The local cloudadmin user is used to set up users in Active Directory (AD). With the Run command feature, you can configure Active Directory over LDAP or LDAPS for vCenter Server as an external identity source.
