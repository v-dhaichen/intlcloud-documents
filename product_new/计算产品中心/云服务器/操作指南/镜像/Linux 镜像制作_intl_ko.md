## 작업 시나리오

본 문서는 Linux 미러 이미지의 제작 과정을 안내합니다.

## 작업 순서

### 준비 과정

시스템 디스크의 미러 이미지를 제작 후 내보내기 할 경우 아래의 검사를 진행해야 합니다.
> 만약 데이터 디스크를 통해 미러 이미지를 내보내기 하는 경우 이 작업을 건너뛸 수 있습니다.
>

#### OS 파티션 및 시작 모드 검사
1. 다음 커맨드를 실행하여 OS 파티션이 GPT 파티션인지 확인하십시오.
```
sudo parted -l /dev/sda | grep 'Partition Table'
```
 - 리턴 결과가 msdos인 경우, 즉 MBR 파티션으로 표시되면 다음 단계로 이동하십시오.
 - 리턴 결과가 gpt인 경우, 즉 GPT 파티션으로 표시됩니다. 현재 서비스 마이그레이션은 GPT 파티션을 지원하지 않습니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6andlevel2_id=7andsource=0anddata_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVMandstep=1)하고 피드백을 요청하십시오.
2. 다음 커맨드를 실행하여 운영 체제가 EFI 방식으로 시작되었는지 검사하십시오.
```
sudo ls /sys/firmware/efi
```
 - 파일이 존재할 경우 즉 현재 운영 체제가 EFI 방식으로 시작되었음을 표시합니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6andlevel2_id=7andsource=0anddata_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVMandstep=1)하고 피드백을 요청하십시오.
 - 파일이 존재하지 않으면 다음 단계로 이동하십시오.

#### 시스템 키 파일 검사
검사할 시스템 키 파일에는 다음과 같은 파일이 포함되지만 이에 제한되지는 않습니다.
> 시스템 키 파일 위치 및 권한이 정확하게 정의되고 읽기 및 쓰기 가능하도록 해당 발행 표준을 따르십시오.
>
 -/etc/grub/grub.cfg:  kernel 파라미터에서는 uuid가 root를 마운트하는 것을 권장하며 다른 방식(예: root=/dev/sda)으로 인해 시스템이 시작하지 않을 수 있습니다.
 -/etc/fstab: 다른 하드 디스크를 마운트하지 마십시오. 마이그레이션 후 디스크 부재로 인해 시스템이 시작하지 않을 수 있습니다.
 -/etc/shadow: 정상적인 권한으로 읽기 및 쓰기가 가능합니다.

#### 소프트웨어 언마운트
언마운트는 드라이버 및 소프트웨어 (VMware tools，Xen tools，Virtualbox GuestAdditions 및 하위 레이어 드라이버의 소프트웨어)의 충돌을 생성합니다.

#### virtio 드라이버 검사
작업에 대한 자세한 내용은 [Linux 시스템 검사 Virtio 드라이버](https://intl.cloud.tencent.com/document/product/213/9929)를 참조하십시오.

#### cloud-init 설치
자세한 내용은 [Linux 시스템 설치 Cloud-init](https://intl.cloud.tencent.com/document/product/213/12587)를 참조하십시오.

#### 기타 하드웨어 관련 구성 검사
클라우드 업로드 이후의 하드웨어는 다음의 변화가 포함되지만, 이에 국한되지는 않습니다.
 - 그래픽 카드가 Cirrus VGA로 교체됩니다.
 - 하드 디스크가 Virtio Disk로 교체되고 장치 이름은 vda 및 vdb입니다.
 - 네트워크 카드가 Virtio Nic으로 교체되고 기본으로 eth0만 제공됩니다.

### 파티션 및 크기 조회
다음 커맨드를 실행하여 현재 운영 체제의 파티션 형식을 조회하고 복사할 파티션 및 크기를 결정하십시오.
```
mount
```
아래의 리턴 결과를 예로 합니다.
```
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sys on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
dev on /dev type devtmpfs (rw,nosuid,relatime,size=4080220k,nr_inodes=1020055,mode=755)
run on /run type tmpfs (rw,nosuid,nodev,relatime,mode=755)
/dev/sda1 on / type ext4 (rw,relatime,data=ordered)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/unified type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,rdma)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
systemd-1 on /home/libin/work_doc type autofs (rw,relatime,fd=33,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12692)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=39,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12709)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,pagesize=2M)
tmpfs on /tmp type tmpfs (rw,nosuid,nodev)
configfs on /sys/kernel/config type configfs (rw,relatime)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,size=817176k,mode=700,uid=1000,gid=100)
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=100)
```
루트 파티션 `/dev/sda1` 에서 `/boot` 및 `/home` 은 독립적인 파티션이 없고 sda1에 boot 파티션이 포함되어 있으며 mbr이 누락되어 있음을 알 수 있습니다. sda 전체를 복사하면 됩니다.
> 내보내기한 미러 이미지에는 최소한 루트 파티션 및 mbr가 포함되어야 합니다. 내보내기한 미러 이미지에 mbr가 없으면 시작할 수 없습니다.
> 현재 운영 체제에서 `/boot` 및` /home`이 독립적인 파티션인 경우 내보내기한 미러 이미지에도 두 개의 독립적인 파티션을 포함해야 합니다.
> 

### 미러 이미지 내보내기
실제 요구 사항에 따라 다양한 방식으로 미러 이미지 내보내기를 선택하십시오.
- [툴 내보내기 사용](# Useplatform)
- [커맨드를 사용해 미러 이미지 내보내기](#ExportImageForUsingCommand)

<span id="Useplatform"></span>
#### 플랫폼 툴을 사용해 미러 이미지 내보내기
VMWare vCenter Convert 혹은 Citrix XenConvert 등과 같은 버츄얼 플랫폼의 미러 이미지 내보내기 툴을 사용하십시오. 자세한 내용은 각 플랫폼의 내보내기 툴 문서를 참조하십시오.
> 현재 Tencent Cloud 마이그레이션에서 지원하는 미러 이미지 형식은 qcow2, vhd, raw, vmdk입니다.
>

<span id="ExportImageForUsingCommand"></span>
#### 커맨드를 사용해 미러 이미지 내보내기
> 커맨드를 사용해 미러 이미지를 수동으로 내보내는 리스크는 상대적으로 높습니다(IO가 사용 중일 때 파일 시스템의 metadata 오류 야기). 미러 이미지를 내보낸 후 [미러 이미지 검사](# CheckMirror)를 실행하여 오류를 제거합니다.
>

다음 커맨드를 실행하여 미러 이미지를 내보낼 수 있습니다.
- **`qemu-img` 커맨드 사용**
예를 들면, 다음 커맨드를 실행하여 `/dev/sda`를 `/mnt/sdb/test.qcow2`로 내보냅니다.
```
sudo qemu-img convert -f raw -O qcow2 /dev/sda /mnt/sdb/test.qcow2
```
이 중 `/mnt/sdb`는 마운트하기 위한 새로운 디스크 및 다른 네트워크 스토리지입니다.
다른 형식으로 전환해야 할 경우 `-O`의 파라미터를 수정하십시오. 수정 가능한 파라미터는 다음과 같습니다.
<span id="-OParameterValue"></span>
<table>
	<tr><th>파라미터</th><th>의미</th></tr>
	<tr><td>qcow2</td><td>qcow2 형식</td></tr>
	<tr><td>vpc</td><td>vhd 형식</td></tr>
	<tr><td>vmdk</td><td>vmdk 형식</td></tr>
	<tr><td>raw</td><td>형식 없음</td></tr>
</table>
- **`dd` 커맨드 사용 **
예를 들면, 다음 커맨드를 실행하여 raw 형식 미러 이미지를 내보냅니다.
```
sudo dd if=/dev/sda of=/mnt/sdb/test.imag bs=1K count=$count
```
이 중 `count` 파라미터는 복사할 파티션의 수량이며 `fdisk` 커맨트를 통해 해당 수량값을 조회할 수 있습니다. 전체 디스크 복사가 필요할 경우 `count` 파라미터는 무시해도 됩니다.
예를 들면, 다음 커맨드를 실행하여 `/dev/sda`의 파티션 수량을 조회하십시오.
```
fdisk -lu /dev/sda
```
다음과 같은 결과를 리턴합니다.
```
Disk /dev/sda: 1495.0 GB, 1494996746240 bytes
255 heads, 63 sectors/track, 181756 cylinders, total 2919915520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disk identifier: 0x0008f290

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048    41945087    20971520   83  Linux
/dev/sda2        41945088    46123007     2088960   82  Linux swap / Solaris
/dev/sda3        46123008    88066047    20971520   83  Linux
/dev/sda4        88066048  2919910139  1415922046   8e  Linux LVM
```
`fdisk` 커맨드의 리턴 결과에 따르면, sda1의 종료 위치는 41945087\* 512 바이트이고 `count`는 20481M으로 설정됩니다.
> `dd` 커맨드를 통해 내보내기한 미러 이미지는 raw 형식이므로 [qcow2, vhd 및 기타 미러 이미지 형식으로 전환](# ImageFormatConversion)하기를 권장합니다.
>

<span id="ImageFormatConversion"></span>
### 미러 이미지 형식 전환
> 현재 Tencent Cloud의 서비스 마이그레이션에서 지원되는 미러 이미지 형식은 qcow2, vhd, vmdk, raw입니다. 압축 미러 이미지 형식을 사용해 전송 및 마이그레이션 시간을 절약할 것을 권장합니다.
> 
 `qemu-img` 커맨드를 사용해 미러 이미지 형식을 전환하십시오.
예를 들면, 다음 커맨드를 실행하여 raw 형식의 미러 이미지를 qcow2 형식으로 전환합니다.
```
sudo qemu-img convert -f raw -O qcow2 test.img test.qcow2
```
- `-f`는 소스 단말기의 미러 이미지 파일 형식입니다.
- `-O` 는 목적 단말기의 미러 이미지 파일 형식입니다. 지원되는 형식은 [`-O` 파라미터](#-OParameterValue)를 참조하십시오.

<span id="CheckMirror"></span>
### 미러 이미지 검사
> 서비스를 정지하지 않고 직접 미러 이미지를 제작하거나 또는 다른 이유로 인해 제작된 미러 이미지의 파일 시스템에 잘못될 수 있으므로 미러 이미지 제작 후 오류 여부를 검사할 것을 권장합니다.
>
미러 이미지 형식이 현재 플랫폼에서 지원하는 형식과 일치할 경우 미러 이미지를 열어 파일 시스템을 직접 검사할 수 있습니다. 예를 들어, Windows 플랫폼은 vhd 형식의 미러 이미지를 직접 추가할 수 있습니다. Linux 플랫폼은 qemu-nbd를 사용해 qcow2 형식 미러 이미지를 열 수 있으며, Xen 플랫폼은 vhd 파일을 직접 시작할 수 있습니다.
Linux 플랫폼을 예로 합니다.
```
modprobe nbd
qemu-nbd -c /dev/nbd0 xxxx.qcow2
mount /dev/nbd0p1 /mnt
```
만약 qcow2 미러 이미지의 첫 번째 파티션을 내보내기 할 경우, 파일 시스템이 손상되며 mount 시 오류가 보고됩니다.
또한, 미러 이미지를 업로드하기 전에 먼저 클라우드 서버를 시작해 미러 이미지 파일의 사용 가능 여부를 테스트할 수 있습니다.
