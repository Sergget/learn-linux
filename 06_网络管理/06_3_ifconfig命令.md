# 6.3 ifconfig命令

ifconfig命令如果不接任何参数，就会输出当前所有启用的网卡信息：

```
$ ifconfig
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:44:41:e9:23  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp1s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.4  netmask 255.255.255.0  broadcast 192.168.50.255
        inet6 fe80::2e0:4cff:fe68:d4c  prefixlen 64  scopeid 0x20<link>
        ether 00:e0:4c:68:0d:4c  txqueuelen 1000  (Ethernet)
        RX packets 6137  bytes 1344568 (1.3 MB)
        RX errors 0  dropped 154  overruns 0  frame 0
        TX packets 7164  bytes 942487 (942.4 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 3160  bytes 554426 (554.4 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 3160  bytes 554426 (554.4 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
其中：
1. 第1行
   - en代表以太网卡，p1s0代表PCI接口的物理位置为(1,0), 其中横座标代表bus，纵座标代表slot.
   - lo 是表示主机的回坏地址，IP地址固定为127.0.0.1，子网掩码为8位，表示本机。
   - UP：代表此网络接口为启用状态（down为关闭状态）
   - RUNNING：代表网卡设备已连接
   - MULTICAST：表示支持组播
   - MTU：为数据包最大传输单元
2. 第2行：
    - inet ：ipv4地址。
    - broadcast：广播地址。
    - netmask：子网掩码
3. 第3行：
   - inet6 ：ipv6地址。
4. 第4行：
   - Ethernet（以太网）表示连接类型；ether：表示为网卡的MAC地址
   - txqueuelen：传输数据的缓冲区的存储长度。
5. 第5行：接受数据包个数、大小统计信息
   - RX：这一行表示网络从启动到目前为止数据包接受情况。
6. 第6行：异常接受包的个数、如丢包量、错误等
7. 第7行：发送数据包个数、大小统计信息
   - TX：与RX一样。RX表示接受。TX表示发送。
8. 第8行：发送包的个数、如丢包量、错误等

其他选项：

- `ifconfig -a` 查看所有网卡信息（包括已禁用）
- `ifconfig -s` 以缩略图标的形式显示网卡信息
- `ifconfig [网卡设备名]` 查看指定的网卡信息
- `ifconfig [网卡设备名] up/down` 启用/禁用指定网卡
- `ifconfig enp1s0 192.168.1.5 netmask 255.255.255.0 mtu 3000` 设置enp1s0 的IP地址，子网掩码和mtu。 

## 帮助文档原文

> man ifconfig

```
NAME
       ifconfig - configure a network interface

SYNOPSIS
       ifconfig [-v] [-a] [-s] [interface]
       ifconfig [-v] interface [aftype] options | address ...

DESCRIPTION
       Ifconfig  is  used to configure the kernel-resident network interfaces.  It is used at boot time to set up in‐
       terfaces as necessary.  After that, it is usually only needed when debugging or when system tuning is needed.

       If no arguments are given, ifconfig displays the status of the currently active interfaces.  If a  single  in‐
       terface  argument  is  given,  it  displays the status of the given interface only; if a single -a argument is
       given, it displays the status of all interfaces, even those that are down.  Otherwise, it configures an inter‐
       face.

Address Families
       If  the  first argument after the interface name is recognized as the name of a supported address family, that
       address family is used for decoding and displaying all protocol addresses.  Currently supported address  fami‐
       lies  include  inet  (TCP/IP,  default),  inet6 (IPv6), ax25 (AMPR Packet Radio), ddp (Appletalk Phase 2), ipx
       (Novell IPX) and netrom (AMPR Packet radio).  All numbers supplied as parts in IPv4  dotted  decimal  notation
       may be decimal, octal, or hexadecimal, as specified in the ISO C standard (that is, a leading 0x or 0X implies
       hexadecimal; otherwise, a leading '0' implies octal; otherwise, the number is interpreted as decimal). Use  of
       hexadecimal and octal numbers is not RFC-compliant and therefore its use is discouraged.

OPTIONS
       -a     display all interfaces which are currently available, even if down

       -s     display a short list (like netstat -i)

       -v     be more verbose for some error conditions

       interface
              The  name  of the interface.  This is usually a driver name followed by a unit number, for example eth0
              for the first Ethernet interface. If your kernel supports alias interfaces, you can specify  them  with
              syntax like eth0:0 for the first alias of eth0. You can use them to assign more addresses. To delete an
              alias interface use ifconfig eth0:0 down.  Note: for every scope (i.e. same  net  with  address/netmask
              combination) all aliases are deleted, if you delete the first (primary).

       up     This  flag  causes the interface to be activated.  It is implicitly specified if an address is assigned
              to the interface; you can suppress this behavior when using an alias interface by appending an - to the
              alias  (e.g.   eth0:0-).   It is also suppressed when using the IPv4 0.0.0.0 address as the kernel will
              use this to implicitly delete alias interfaces.

       down   This flag causes the driver for this interface to be shut down.

       [-]arp Enable or disable the use of the ARP protocol on this interface.

       [-]promisc
              Enable or disable the promiscuous mode of the interface.  If selected, all packets on the network  will
              be received by the interface.

       [-]allmulti
              Enable  or  disable  all-multicast mode.  If selected, all multicast packets on the network will be re‐
              ceived by the interface.

       mtu N  This parameter sets the Maximum Transfer Unit (MTU) of an interface.

       dstaddr addr
              Set the remote IP address for a point-to-point link (such as PPP).  This keyword is now  obsolete;  use
              the pointopoint keyword instead.

       netmask addr
              Set  the  IP network mask for this interface.  This value defaults to the usual class A, B or C network
              mask (as derived from the interface IP address), but it can be set to any value.

       add addr/prefixlen
              Add an IPv6 address to an interface.

       del addr/prefixlen
              Remove an IPv6 address from an interface.

       tunnel ::aa.bb.cc.dd
              Create a new SIT (IPv6-in-IPv4) device, tunnelling to the given destination.

       irq addr
              Set the interrupt line used by this device.  Not all devices can dynamically change their IRQ setting.

       io_addr addr
              Set the start address in I/O space for this device.

       mem_start addr
              Set the start address for shared memory used by this device.  Only a few devices need this.

       media type
              Set the physical port or medium type to be used by the device.  Not all devices can  change  this  set‐
              ting,  and  those that can vary in what values they support.  Typical values for type are 10base2 (thin
              Ethernet), 10baseT (twisted-pair 10Mbps Ethernet), AUI (external transceiver) and so on.   The  special
              medium type of auto can be used to tell the driver to auto-sense the media.  Again, not all drivers can
              do this.

       [-]broadcast [addr]
              If the address argument is given, set the protocol broadcast address for  this  interface.   Otherwise,
              set (or clear) the IFF_BROADCAST flag for the interface.

       [-]pointopoint [addr]
              This  keyword enables the point-to-point mode of an interface, meaning that it is a direct link between
              two machines with nobody else listening on it.
              If the address argument is also given, set the protocol address of the other side  of  the  link,  just
              like  the  obsolete dstaddr keyword does.  Otherwise, set or clear the IFF_POINTOPOINT flag for the in‐
              terface.

       hw class address
              Set the hardware address of this interface, if the device driver supports this operation.  The  keyword
              must  be  followed by the name of the hardware class and the printable ASCII equivalent of the hardware
              address.  Hardware classes currently supported include ether (Ethernet), ax25 (AMPR AX.25), ARCnet  and
              netrom (AMPR NET/ROM).

       multicast
              Set the multicast flag on the interface. This should not normally be needed as the drivers set the flag
              correctly themselves.

       address
              The IP address to be assigned to this interface.

       txqueuelen length
              Set the length of the transmit queue of the device. It is useful to set this to small values for slower
              devices with a high latency (modem links, ISDN) to prevent fast bulk transfers from disturbing interac‐
              tive traffic like telnet too much.

NOTES
       Since kernel release 2.2 there are no explicit interface statistics for alias interfaces anymore. The  statis‐
       tics printed for the original address are shared with all alias addresses on the same device. If you want per-
       address statistics you should add explicit accounting rules for the address using the iptables(8) command.

       Interrupt problems with Ethernet device drivers fail with EAGAIN (SIOCSIIFLAGS: Resource temporarily  unavail‐
       able)  it  is most likely a interrupt conflict. See http://www.scyld.com/expert/irq-conflict.html for more in‐
       formation.

FILES
       /proc/net/dev
       /proc/net/if_inet6

BUGS
       Ifconfig uses the ioctl access method to get the full address information, which limits hardware addresses  to
       8  bytes.   Because  Infiniband hardware address has 20 bytes, only the first 8 bytes are displayed correctly.
       Please use ip link command from iproute2 package to display link layer informations including the hardware ad‐
       dress.

       While appletalk DDP and IPX addresses will be displayed they cannot be altered by this command.

SEE ALSO
       route(8), netstat(8), arp(8), rarp(8), iptables(8), ifup(8), interfaces(5).
       http://physics.nist.gov/cuu/Units/binary.html - Prefixes for binary multiples

AUTHORS
       Fred N. van Kempen, <waltje@uwalt.nl.mugnet.org>
       Alan Cox, <Alan.Cox@linux.org>
       Phil Blundell, <Philip.Blundell@pobox.com>
       Andi Kleen
       Bernd Eckenfels, <net-tools@lina.inka.de>
```