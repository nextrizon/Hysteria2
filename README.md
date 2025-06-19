![image](https://github.com/user-attachments/assets/c4acd789-afb8-4cab-9d1e-f5642aa258bd)## Setting up a Hysteria2 client node on GL-iNet GL-MT3000(Beryl AX) router
___

>[!NOTE]
>You can use the [following guide](https://cscot.pages.dev/2023/09/13/hysteria2-furious/) on setting up a Hysteria2 server and/or client on a Windows PC

>[!IMPORTANT]
> I'm not responsible if this guide break your router. If it does happen, you can try using [this guide](https://docs.gl-inet.com/router/en/3/tutorials/debrick/) to restore the firmware for your GL-iNet router.

This guide should also work for GL-iNet MT2500A/MT6000 and any OpenWrt router using an ARM Cortex-A53 processor with at least 256MB of flash storage.

### Prerequisites
___
1. Update to the latest firmware for your OpenWrt router. The GL-iNet version of the OpenWrt still stuck version 21 as of writing this guide.
2. Make sure to install LuCI interface in the **Advanced Settings** of the GL-iNet Admin Panel webpage for GL-iNet router or use the `opkg` command after ssh into the router and using `opkg update` command after step 2.

### Installation
___
Step 1. Ssh into your router at 192.168.8.1 as _root_ user with **PuTTY** for Windows or using the built in ssh client in Windows Command Prompt/MacOS Terminal.
Step 2. Run update for OpenWrt packages.

```bash
opkg update
```
> [!NOTE]
>If you haven't install LUCI from the Admin Panel webpage, use the following command to install it.
```bash
opkg install luci-app-opkg
```

Step 3. Run the following command to download and execute a script to update the OpenWrt's LuCI web interface with the custom iStoreOS theme.

```bash
wget -O gl-inet.sh https://cafe.cpolar.top/wkdaily/gl-inet-onescript/raw/branch/master/gl-inet.sh && chmod +x gl-inet.sh && ./gl-inet.sh
```
Step 4. You should see the following Chinese text install menu. Go ahead and press **1** and then **ENTER** for `GL.iNet GL-MT3000一键iStoreOS风格化`

![install script](https://github.com/nextrizon/Hysteria2/blob/main/gl-inet.png)

> [!NOTE]
>This will take couple of minutes for the script to install the iStoreOS theme.

![finish install](https://github.com/nextrizon/Hysteria2/blob/main/install-complete.png)

Press **ENTER** when see above and the **q** to quit out of the script as you don't need to install any other module.

Step 5. Login into the newly installed LuCI iStoreOS theme from the **Advanced Settings** from the GL-iNet Admin Panel webpage or directly at http://192.168.8.1:8080/cgi-bin/luci/

> [!NOTE]
>All of the text in this LuCI theme is in Chinese, you can enable Chrome browser's auto Google Translate and see the text in your default language.
>But I will continue this guide showing the original Chinese menu.

Step 6. Manual install Passwall2 plug-in in the iStore app page. Download the latest Passwall2 plug-in from [this GitHub page](https://github.com/AUK9527/Are-u-ok/tree/main/apps)
> [!NOTE]
>There are 5 different iStore plug-ins available for router using ARM Cortex-A53 processor. Download the one for **Passwall2** as I could get Hysteria2 working with OpenClash and I didn't bother with the other plug-ins once I got Passwall2 working.
As writing of this guide I downloaded this **PassWall2_25.5.7_aarch64_a53_all_sdk_22.03.7.run** plug-in file.

![istore plugin](https://github.com/nextrizon/Hysteria2/blob/main/istore.png)
Step 7. Using the above screenshot, select **iStore** on the left side menu, select **手动安装** for Manual Installation, and then select **选择或拖放文件** to upload the Passwall2 .run file to install the plug-in.

Step 8. It going to take a minute or 2 to install the Passwall2 plug-in, the pop-up screen will have **red** dot will it's being install and **green** dot when it finish. Click **green** to exit out of the install screen.

Step 9. You need go back to the GL.iNet Admin Panel webpage and select **Reboot** icon in the upper right corner.

Step 10. Go back to LuCI Admin panel webpage at http://192.168.8.1:8080/cgi-bin/luci/.

![Hysteria2 setup](https://github.com/nextrizon/Hysteria2/blob/main/Hy2setup.png)
Step 11. Using the above screenshot, select **服务** for Service, and then select **Passwall 2**. Select the 2nd tab **节点列表** for Node List and select either of the blue **添加** button Add To the Node List.

