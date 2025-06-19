## Setting up a Hysteria2 client node on GL-iNet GL-MT3000(Beryl AX) router
___

>[!NOTE]
>You can use the [following guide](https://cscot.pages.dev/2023/09/13/hysteria2-furious/) on setting up a Hysteria2 server and/or client on a Windows PC

>[!IMPORTANT]
> I'm not responsible if this guide break your router. If it does happen, you can try using [this guide](https://docs.gl-inet.com/router/en/3/tutorials/debrick/) to restore the firmware for your GL-iNet router.

This guide should also work for GL-iNet MT2500/MT6000 and any OpenWrt router using an ARM Cortex-A53 processor with at least 256MB of flash storage.

### Prerequisites
___
1. Update to the latest stable firmware for your OpenWrt router. The GL-iNet version of the OpenWrt still stuck version 21 as of writing this guide.
2. Make to install LUCI interface in the Advance Setting of the GL-iNet Admin webpage for your router.

### Installation
___
1. Ssh into your router at 192.168.8.1 with **Putty** for Windows or the built in ssh client in Windows Command Prompt/MacOS Terminal.
2. Run update for OpenWrt packages.
```opkg update```
3. Run the following command to download the script to update the OpenWrt's LUCI web interface with the custom istore interface.
`wget -O gl-inet.sh https://cafe.cpolar.top/wkdaily/gl-inet-onescript/raw/branch/master/gl-inet.sh && chmod +x gl-inet.sh && ./gl-inet.sh`
