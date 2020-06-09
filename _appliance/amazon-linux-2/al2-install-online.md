---
title: [Install the ThoughtSpot application on online clusters that use Amazon Linux 2]
summary: "Install ThoughtSpot on Amazon Linux 2 online clusters."
last_updated: 6/8/2020
sidebar: mydoc_sidebar
permalink: /:collection/:path.html
---
Before starting the install, complete the [pre-installation steps]({{ site.baseurl }}/appliance/amazon-linux-2/al2-prerequisites.html). If you are using the [AWS SSM agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent.html){:target="_blank"} as an alternative to SSH, you must run the Ansible playbook and all commands on the __SSM console__.

In an online cluster, the hosts can access the public repositories to download the required packages.

Before you build the ThoughtSpot cluster and install the ThoughtSpot application on the hosts, you must run the Ansible playbook. The TS Ansible playbook prepares your clusters in the following manner:

- Ansible installs the required packages: YAML, Python, and R packages; see [Packages installed with ThoughtSpot for Amazon Linux 2]({{ site.baseurl }}/appliance/amazon-linux-2/al2-packages.html).
- It creates and configures local user accounts for ThoughtSpot:
   - `admin` user has full administrative functionality
   - `thoughtspot` user can load data in the application
- It installs the ThoughtSpot CLI, `tscli`.
- It configures the ThoughtSpot host nodes:
   - checks that customization scripts can execute on the nodes
   - checks that the partitions meet minimum size requirements

   | &#10063; | [1. Prepare the `/tmp` disk](#tmp) |
   | &#10063; | [2. Configure the Ansible Playbook](#configure-ansible) |
   | &#10063; | [3. Run the Ansible Playbook](#run-ansible) |
   | &#10063; | [4. Install ThoughtSpot](#install-thoughtspot) |

{: id="tmp"}
## Prepare the `/tmp` disk
1. Run the following script to set the disk name:
    ```
    set -e
    DISK=dev/<disk_name>
    PART=$<DISK>1
    ```
2. Unmount `/tmp` if necessary:
    ```
    sudo umount /tmp || true
    ```
3. Remove `/tmp` from `/etc/fstab`:
    ```
    sudo sed -i "/.*tmp.*/d" /etc/fstab
    ```
4. Remove `/tmp` from the partition table:
    ```
    echo -e "d\nw\n" | sudo fdisk $<DISK>
    ```
5. Partition the disk:
    ```
    sudo parted -s $<DISK> mklabel gpt
    sudo parted -s $<DISK> mkpart primary xfs 0% 100%
    ```

6. Create the file system:
    ```
    sudo mkfs.xfs -f $PART
    echo "UUID=$(sudo blkid -o value -s UUID $PART) /tmp xfs defaults,nofail 0 1" | sudo tee -a /etc/fstab
    sudo mount /tmp
    sudo chmod 777 /tmp
    ```

7. Create a working directory for Ansible:
    ```
    set -e
    WORKDIR=/tmp/ansible
    rm -rf $WORKDIR
    mkdir -p $WORKDIR
    cd $WORKDIR
    ```


{: id="configure-ansible"}
## Configure the Ansible Playbook

To set up the Ansible, follow these steps:

<ol>
  <li><p>Obtain the Ansible tarball by talking to your ThoughtSpot contact. Download it to your local machine.</p> <p>You can download it by running the following command: <code>current_tarball-location cp new_tarball_path ./</code>. For example, <code>aws s3 cp s3://example_path/6.1.1-2.offline.ansible.tar.gz ./</code>.</p></li>

  <li>Unzip the Ansible tarball, to see the following files and directories on your local machine:<br/>
   <dl>
    <dlentry>
      <dt>customize.sh</dt>
      <dd>This script runs as the last step in the preparation process. You can use it to inject deployment-specific customizations, such as enabling or disabling a corporate proxy, configuring extra SSH keys, installing extra services, and so on.</dd>
    </dlentry>
    <dlentry>
      <dt>hosts.sample</dt>
      <dd>The Ansible inventory file.</dd>
    </dlentry>
    <dlentry>
      <dt>prod_image</dt>
      <dd>This directory contains the ThoughtSpot tools and <code>tscli</code>, the ThoughtSpot CLI binary.</dd>
    </dlentry>
    <dlentry>
      <dt>README.md</dt>
      <dd>Basic information for the unzipped file</dd>
    </dlentry>
    <dlentry>
      <dt>rpm_gpg</dt>
      <dd>This directory contains the <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2rl_verify.html" target="_blank">GPG keys</a> that authenticate the public repository.</dd>
    </dlentry>
    <dlentry>
      <dt>toolchain</dt>
      <dd>The tools that are necessary to compile the instructions you define in the Ansible Playbook, the source code, into executables that can run on your device. The toolchain includes a compiler, a linker, and run-time libraries.</dd>
    </dlentry>
    <dlentry>
      <dt>ts-amzn-new.yaml</dt>
      <dd>The Ansible Playbook for new installations.</dd>
    </dlentry>
    <dlentry>
      <dt>ts-amzn-update.yaml</dt>
      <dd>The Ansible Playbook for updates.</dd>
    </dlentry>
    <dlentry>
      <dt>ts-amzn.yaml</dt>
      <dd></dd>
    </dlentry>
    <dlentry>
      <dt>yum.repos.d</dt>
      <dd>This directory contains information about the yum repo used by the cluster.</dd>
    </dlentry>
  </dl>
  </li>

  <li><p>Copy the Ansible inventory file <code>hosts.sample</code> to <code>hosts.yaml</code>, and using a text editor of your choice, update the file to include your host configuration.</p> <p>Copy the file by running this command: <code>cp hosts.sample hosts.yaml</code>. </p>
  <p>If you are using SSM, you must additionally run a command to replace the <code>ts_partition_name</code>, and run a command to create a single partition on the disk mounted under <code>/export</code>. Run the following command to replace the <code>ts_partition_name</code>:<br> <pre><code>TS_DISK=disk_name_for_export_partition
  TS_PARTITION_NAME=${TS_DISK}1
sed -i "s/xvda9/$TS_PARTITION_NAME/g" hosts.yaml</code></pre> Then run this command to create a single partition on the disk mounted under <code>/export</code>: <br> <pre><code>sudo parted -s /dev/$TS_DISK mklabel gpt
sudo parted -s /dev/$TS_DISK mkpart primary xfs 0% 100%</code></pre></p>
  <br/>

      <dl>
       <dlentry id="hosts">
      <dt>hosts</dt>
      <dd>Add the IP addresses or hostnames of all hosts in the ThoughtSpot cluster.</dd>
    </dlentry>
    <dlentry id="admin_uid">
      <dt>admin_uid</dt>
      <dd>The admin user ID parameter. Use the default values. If using SSM, the <code>ssm_user</code> uses the default value, <code>1001</code>. You must choose a new value.<br/>
</dd>
    </dlentry>
    <dlentry id="admin-gid">
      <dt>admin_gid</dt>
      <dd>The admin user group ID. Use the default values. If using SSM, the <code>ssm_user</code> uses the default value, <code>1001</code>. You must choose a new value.<br/>
</dd>
    </dlentry>
    <dlentry id="ssh_user">
      <dt>ssh_user</dt>
      <dd><p>The <code>ssh_user</code> must exist on the ThoughtSpot host, and it must have <code>sudo</code> privileges. This user is the same as the <code>ec2_user</code>.</p>
      <p>If you are using AWS SSM instead of ssh, there is no need to fill out this parameter.</p>
</dd>
    </dlentry>
    <dlentry id="ssh_private_key">
      <dt>ssh_private_key</dt>
      <dd>Add the private key for <code>ssh</code> access to the <code>hosts.yaml</code> file. You can use an existing key pair, or generate a new key pair in the Ansible Control server.<br/>
      Run the following command to verify that the Ansible Control Server can connect to the hosts over <code>ssh</code>:<br/><pre><code>ansible -m ping -i hosts.yaml all</code></pre>
      <p>If you are using AWS SSM instead of ssh, there is no need to fill out this parameter or run the above command.</p></dd>
    </dlentry>
    <dlentry id="ssh_public_key">
      <dt>ssh_public_key</dt>
      <dd>Add the public key to the <code>ssh authorized_keys</code> file for each host, and add the private key to the <code>hosts.yaml</code> file. You can use an existing key pair, or generate a new key pair in the Ansible Control server.<br/>
      Run the following command to verify that the Ansible Control Server can connect to the hosts over <code>ssh</code>:<br/><pre><code>ansible -m ping -i hosts.yaml all</code></pre>
      <p>If you are using AWS SSM instead of ssh, there is no need to fill out this parameter or run the above command.</p></dd>
    </dlentry>
    <dlentry id="extra_admin_ssh_key">
      <dt>extra_admin_ssh_key</dt>
      <dd>[Optional] An additional or extra key may be required by your security application, such as Qualys, to connect to the hosts.
      <p>If you are using AWS SSM instead of ssh, there is no need to fill out this parameter.</p></dd>
    </dlentry>
    <dlentry id="http(s)_proxy">
      <dt>http(s)_proxy</dt>
      <dd>If the hosts must access public repositories through an internal proxy service, provide the proxy information.<br/>
      This release of ThoughtSpot does not support proxy credentials to authenticate to the proxy service.</dd>
    </dlentry>  
    <dlentry id="ts_partition_name">
      <dt>ts_partition_name</dt>
      <dd>The extended name of the ThoughtSpot export partition, such as <code>/dev/sdb1</code>.</dd>
    </dlentry>
  </dl>
  </li>
</ol>

{: id="run-ansible"}
## Run the Ansible Playbook

Run the Ansible Playbook from your local machine or the SSM console by entering the following command:

```
ansible-playbook -i hosts.yaml ts-amzn.yaml
```

As the Ansible Playbook runs, it will perform these tasks:

  1. Trigger the installation of [RPM packages]({{ site.baseurl }}/appliance/amazon-linux-2/al2-packages.html)
  2. Configure the local user accounts that the ThoughtSpot application uses
  3. Install the ThoughtSpot CLI
  4. Configure all the nodes in the ThoughtSpot cluster:
     - Format and create export partitions, if they do not exist
     - Format the data disks, and run `prepare disks`

After the Ansible Playbook finishes, your hosts are ready for installing the ThoughtSpot application.

{: id="install-thoughtspot"}
## Install the ThoughtSpot cluster and the application

Refer to [Install ThoughtSpot clusters in AWS]({{ site.baseurl }}/appliance/aws/aws-cluster-install.html) for more detailed information on installing the ThoughtSpot cluster.

Follow these general steps to install ThoughtSpot on the prepared hosts:

1. Download the release artifact from the ThoughtSpot file sharing system.
2. Upload the release artifact to the first host.
3. Run the `tscli cluster create` command. This script prompts for user input.
4. Check the cluster health by running health checks and logging into the application.
