## Setting up a Hysteria2 client node on GL-iNet GL-MT3000(Beryl AX) router
___

>[!NOTE]
>You can use the [following guide](https://cscot.pages.dev/2023/09/13/hysteria2-furious/) on setting up a Hysteria2 server and/or client on a Windows PC

>[!IMPORTANT]
> I'm not responsible if this guide brick your router. If it does happen, you can try using [this guide](https://docs.gl-inet.com/router/en/3/tutorials/debrick/) to restore the firmware for your GL-iNet router.

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

Step 6. Manual install PassWall2 plug-in in the iStore app page. Download the latest PassWall2 plug-in from [this GitHub page](https://github.com/AUK9527/Are-u-ok/tree/main/apps)
> [!NOTE]
>There are 5 different iStore plug-ins available for router using ARM Cortex-A53 processor. Download the one for **PassWall2** as I couldn't get Hysteria2 working with OpenClash and I didn't bother with the other plug-ins once I got PassWall2 working.
As writing of this guide I downloaded the plug-in file e.g., **PassWall2_25.5.7_aarch64_a53_all_sdk_22.03.7.run**.

![istore plugin](https://github.com/nextrizon/Hysteria2/blob/main/istore.png)

Step 7. Using the above screenshot, select **iStore** on the left side menu, select **手动安装** for Manual Installation, and then select **选择或拖放文件** to upload the PassWall2 .run file to install the plug-in.

Step 8. It going to take a minute or 2 to install the PassWall2 plug-in, the pop-up screen will have **red** dot will it's being install and **green** dot when it finish. Click **green** to exit out of the install screen.

Step 9. You need go back to the GL.iNet Admin Panel webpage and select **Reboot** icon in the upper right corner.

> [!WARNING]
> You must reboot the router after installing the PassWall2 plug-in, else the router will not connect to the Hysteria2 server after you create a Hysteria2 node on this router.

Step 10. Go back to LuCI Admin panel webpage at http://192.168.8.1:8080/cgi-bin/luci/.

![Hysteria2 setup](https://github.com/nextrizon/Hysteria2/blob/main/Hy2setup.png)

Step 11. Using the above screenshot, select the gear icon **服务** for **Service**, and then select **PassWall 2**. Then select the 2nd tab **节点列表** for **Node List** and select either of the blue **添加** buttons to **Add To** the Node List.

![Hysteria2 setup](https://github.com/nextrizon/Hysteria2/blob/main/Hy2node.png)

Step 12. Using the above screenshot, I will update the Hysteria2 node configuration using the settings from the [above guide](https://cscot.pages.dev/2023/09/13/hysteria2-furious/) for the server install.
> [!NOTE]
>The easiest way to do it is to **Export Share Link To Clipboard** from the **[Furious](https://github.com/LorenEteval/Furious/releases) client in the **Edit Configuration** menu and then import config by selecting the **导入分享URL**/**Importing Share URL** in Passwall2 node list page, if you did a test connection using the [above guide](https://cscot.pages.dev/2023/09/13/hysteria2-furious/).

Enter for the following boxes:

|Chinese|English|What to enter|
|-------|-------|-------------|
|节点备注|Node Remark|Unique name for this node in the node list|
|类型|Type|Change to **Hysteria2**|
|协议名称|Protocal Name|Should default to **UDP**|
|地址（支持域名)|IP Adress(Domain Supported)|Either the IP address or the host and domain name of the Hysteria2 server|
|端口|Port|Enter **443** or whatever port # you decided to use in your Hysteria2 server setup|
|端口跳跃范围|Port Hopping Range|You can leave it blank or enter number range like 1000-2000|
|混淆密码|Obfuscated Password|Leave it blank unless you setup obfucation tag in the server config file|
|认证密码|Authentication Password|Enter the password that was used the server config file|
|域名|Domain Name|You can use the same domain as above or change it to **www.bing.com** if you only an IP address or don't use the same domain|
|快速打开|Allow Insecure Connections|Should **not** check the box as the server is using a secure certificate|
|PinSHA256|PinSHA256|Leave it blank, I think it's use when the server isn't using secure ceftificate|
|最大上行(Mbps)|Maximum Uplink(Mbps)|Leave it blank, unless you want to limite the uplink speed|
|最大下行(Mbps)|Maximum Downlink(Mbps)|Again blank, unless otherwise|
### Just leave the rest of the boxes blank

Select blue **保存并应用** button on the bottom of the page to **Save and Apply** the settings that were entered

Step 13. You see the newly created Hysteria2 node under the existing **Xray 分流** node. Click on the **测试** to the Hysteria2 node to do **Test** ping to the Hysteria2 server.

Step 14. Select the 1st tab **基本设置** to go back to the **Basic Setting** Menu

Step 15. Change the **节点** Node selection from the default **Xray 分流** node to the newly created **Hysteria2** node.

Step 16. Select the **主开关 Main Switch** check box to start the Hysteria2 proxy connection when router starts up and select blue **保存并应用** button on the bottom of the page to **Save and Apply** the change.

Step 17. The **Core** status should change from red **未运行** not running to green **运行中** running status.

Step 18. You can test the latency of the Baidu, Google, and Github connections by clicking on the respecting text boxes.

> [!CAUTION]
> If no connection could be made with Baidu, Google, and Github doing the latency test, trying having both domain name in ** 域名**/Domain Name and **地址（支持域名)**/IP Adress(Domain Supported) settings be the same. So instead of using an IP address, use a free subdomain from FreeDNS that will tie to the public IP address of the Hysteria2 server.

> [!Note]
> I haven't test this router setup behind the GFW as I'm setup this up for friend who will be traveling in China in a few months. Only to both a home and cheap VPS servers. I will update this once the travel happens.


