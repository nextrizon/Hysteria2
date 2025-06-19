## Setting up a Hysteria2 client node on GL-iNet GL-MT3000(Beryl AX) router
___

>[!NOTE]
>You can use the [following guide](https://cscot.pages.dev/2023/09/13/hysteria2-furious/) on setting up a Hysteria2 server and/or client on a Windows PC

>[!IMPORTANT]
> I'm not responsible if this guide break your router. If it does happen, you can try using [this guide](https://docs.gl-inet.com/router/en/3/tutorials/debrick/) to restore the firmware for your GL-iNet router.

This guide should also work for GL-iNet MT2500A/MT6000 and any OpenWrt router using an ARM Cortex-A53 processor with at least 256MB of flash storage.

### Prerequisites
___
1. Update to the latest firmware for your OpenWrt router. The GL-iNet version of the OpenWrt still stuck version 21 as of writing this guide.
2. Make sure to install LUCI interface in the **Advanced Settings** of the GL-iNet Admin webpage for GL-iNet router or use the `opkg` command after ssh into the router and doing `opkg update` command.

### Installation
___
1. Ssh into your router at 192.168.8.1 as _root_ user with **PuTTY** for Windows or using the built in ssh client in Windows Command Prompt/MacOS Terminal.
2. Run update for OpenWrt packages.

```bash
opkg update
```
> [!NOTE]
>If you haven't install LUCI from the Admin webpage, use the following command to install it.
```bash
opkg install luci-app-opkg
```

3. Run the following command to download and execute a script to update the OpenWrt's LUCI web interface with the custom iStoreOS theme.

```bash
wget -O gl-inet.sh https://cafe.cpolar.top/wkdaily/gl-inet-onescript/raw/branch/master/gl-inet.sh && chmod +x gl-inet.sh && ./gl-inet.sh
```
4. You should see the following Chinese text install menu. Go ahead and press **1** and then **ENTER** for  `GL.iNet GL-MT3000一键iStoreOS风格化`
   ![install script](https://github.com/nextrizon/Hysteria2/blob/main/gl-inet.png)

> [!NOTE]
>This will take couple of minutes for the script to install the iStoreOS theme.
![finish install](https://github.com/nextrizon/Hysteria2/blob/main/install-complete.png)

Press **ENTER** when see above and the **q** at the main install menu as you don't need to install any other module.


