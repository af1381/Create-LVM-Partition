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

# Step 4: Create Volume Group (VG):
<mark>Create a Volume Group and add your physical volume to it:</mark>
     
    sudo vgcreate my_vg /dev/sdb1
  
* Here my_vg is the name of the volume group, which you can change.

# Step 5: Create Logical Volume (LV):
 <mark>Now you can create one or more Logical Volumes within your volume group. For example, to create a 10GB Logical Volume:</mark>

    sudo lvcreate -L 10G -n my_lv my_vg

   * -L 10G: Specifies the logical volume size.
   * -n my_lv: Logical volume name (here my_lv).
   * my_vg: Volume group name.

# Step 6: Format the logical volume:
  <mark>To use a logical volume, you must format it. For example, with the ext4 file system:</mark>
   
    sudo mkfs.ext4 /dev/my_vg/my_lv

# Step 7: Mount the logical volume :
<mark>To use a logical volume, you must mount it:</mark>
* Create a directory for the mount:
  
      sudo mkdir /mnt/my_lv
* Mount the logical volume:

      sudo mount /dev/my_vg/my_lv /mnt/my_lv

* For permanent mount, add it to the fstab file. Edit the /etc/fstab file and add the following line:

       /dev/my_vg/my_lv /mnt/my_lv ext4 defaults 0 0

# Step 8: Check the settings:
 <mark>To check the LVM status, use the following commands:</mark>
 * Viewing physical volumes:

       sudo pvs

* View volume groups:

       sudo vgs

* Viewing logical volumes:

        sudo lvs
