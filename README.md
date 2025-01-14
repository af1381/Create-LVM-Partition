# Create-LVM-Partition

# Step 1: Prepare the disk
 <mark>First you need to identify the new disk you want to use for LVM. Use the following command to view the disks:</mark>
                                                                                                                         
     lsblk

# Step 2: Create LVM partition:
<mark>Create a new partition using the fdisk or parted tool. For example:</mark>

    sudo fdisk /dev/sdb

                                                                                                                    
In the fdisk environment, follow these steps: 
*   Press the <mark>{n}</mark> key to create a new partition.
*   Select the partition type (Primary or Extended). Usually Primary.
*   Specify the partition size.
*   Then change the partition type with <mark>{t}</mark> and enter the code <mark>{8e}</mark> (LVM).
*   Save the changes with <mark>{w}</mark>


# Step 3: Set the partition as a Physical Volume (PV):
  <mark>To use LVM, you need to convert the partition to a physical volume (PV):</mark>:

    sudo pvcreate /dev/sdb1

