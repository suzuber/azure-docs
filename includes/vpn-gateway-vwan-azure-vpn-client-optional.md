---
 author: cherylmc
 ms.service: vpn-gateway
 ms.topic: include
 ms.date: 03/07/2025
 ms.author: cherylmc
#Customer intent: this file is used for both virtual wan and vpn gateway articles.
---
## Working with VPN client profile configuration files

The steps in this article require you to modify and import the Azure VPN Client profile configuration file. The following profile configuration files are generated, depending on the authentication types configured for your P2S VPN gateway.

* **azurevpnconfig.xml**: This file is generated when only one authentication type is selected.
* **azurevpnconfig_aad.xml**: This file is generated for Microsoft Entra ID authentication when there are multiple authentication types selected.
* **azurevpnconfig_cert.xml**: This file is generated for Certificate authentication when there are multiple authentication types selected.

To work with VPN client profile configuration files (xml files), use the following steps:

1. Locate the profile configuration file and open it using the editor of your choice.
1. Using the examples in the following sections, modify the file as necessary, then save your changes.
1. Import the file to configure the Azure VPN client. You can import the file for the Azure VPN Client using these methods:

   * **Azure VPN Client interface**: Open the Azure VPN Client and select **+** and then **Import**. Locate the modified .xml file. Configure any additional settings in the Azure VPN Client interface (if necessary), then select **Save**.

   * **Command-line prompt**: Place the appropriate downloaded configuration xml file in the *%userprofile%\AppData\Local\Packages\Microsoft.AzureVpn_8wekyb3d8bbwe\LocalState* folder, then run the command that corresponds to the configuration file name. For example, `azurevpn -i azurevpnconfig_aad.xml`. To force the import, use the `-f` switch.

## DNS

### Add DNS suffixes

> [!NOTE]
> At this time, additional DNS suffixes for the Azure VPN Client aren't generated in a format that can be properly used by macOS. The specified values for DNS suffixes don't persist for macOS.

To add DNS suffixes, modify the downloaded profile XML file and add the **\<dnssuffixes>\<dnssufix> \</dnssufix>\</dnssuffixes>** tags.

```xml
<azvpnprofile>
<clientconfig>

    <dnssuffixes>
          <dnssuffix>.mycorp.com</dnssuffix>
          <dnssuffix>.xyz.com</dnssuffix>
          <dnssuffix>.etc.net</dnssuffix>
    </dnssuffixes>

</clientconfig>
</azvpnprofile>
```

### Add custom DNS servers

To add custom DNS servers, modify the downloaded profile XML file and add the **\<dnsservers>\<dnsserver> \</dnsserver>\</dnsservers>** tags.

```xml
<azvpnprofile>
<clientconfig>

    <dnsservers>
        <dnsserver>x.x.x.x</dnsserver>
            <dnsserver>y.y.y.y</dnsserver>
    </dnsservers>

</clientconfig>
</azvpnprofile>
```

> [!NOTE]
> When using Microsoft Entra ID authentication, the Azure VPN Client utilizes DNS Name Resolution Policy Table (NRPT) entries, which means DNS servers aren't listed under the output of `ipconfig /all`. To confirm your in-use DNS settings, consult [Get-DnsClientNrptPolicy](/powershell/module/dnsclient/get-dnsclientnrptpolicy) in PowerShell.

## Routing

### Split tunneling

Split tunneling is configured by default for the VPN client.

### Forced tunneling

You can configure forced tunneling in order to direct all traffic to the VPN tunnel. Forced tunneling can be configured using two different methods; either by advertising custom routes, or by modifying the profile XML file.

> [!NOTE]
> Internet connectivity isn't provided through the VPN gateway. As a result, all traffic bound for the Internet is dropped.

* **Advertise custom routes:** You can advertise custom routes `0.0.0.0/1` and `128.0.0.0/1`.

* **Profile XML:** You can modify the downloaded profile xml file and add the **\<includeroutes>\<route>\<destination>\<mask> \</destination>\</mask>\</route>\</includeroutes>** tags.

For Azure VPN Client for Windows:

* Version 2.1900:39.0 or higher. You can include the route 0/0. Modify the downloaded profile xml file and add the **\<includeroutes>\<route>\<destination>\<mask> \</destination>\</mask>\</route>\</includeroutes>** tags. Make sure to update the version number to 2.
* Version lower than 2.1900:39.0: You need to add two custom routes: 0.0.0.0/1 and 128.0.0.0/1.

For Azure VPN Client on macOS:

- macOS version 14 or higher. Only the custom route 0/0 is supported. The routes 0.0.0.0/1 and 128.0.0.0/1 aren't supported.

You can include the custom route `0.0.0.0/0` in the xml file:

 ```xml
  <azvpnprofile>
  <clientconfig>

    <includeroutes>
        <route>
            <destination>0.0.0.0</destination><mask>0</mask>
        </route>
    </includeroutes>

  </clientconfig>
  </azvpnprofile>
  ```

You can add the custom routes `0.0.0.0/1` and `128.0.0.0/1` in the xml file:

   ```xml
  <azvpnprofile>
  <clientconfig>

    <includeroutes>
        <route>
            <destination>0.0.0.0</destination><mask>1</mask>
        </route>
        <route>
            <destination>128.0.0.0</destination><mask>1</mask>
        </route>
    </includeroutes>

  </clientconfig>
  </azvpnprofile>
  ```

> [!NOTE]
>
> * The default status for the clientconfig tag is `<clientconfig i:nil="true" />`, which can be modified based on the requirement.
> * A duplicate clientconfig tag isn't supported on macOS, so make sure the clientconfig tag isn't duplicated in the XML file.

### Add custom routes

You can add custom routes. Modify the downloaded profile XML file and add the **\<includeroutes>\<route>\<destination>\<mask> \</destination>\</mask>\</route>\</includeroutes>** tags.

```xml
<azvpnprofile>
<clientconfig>

    <includeroutes>
        <route>
            <destination>x.x.x.x</destination><mask>24</mask>
        </route>
        <route>
                <destination>y.y.y.y</destination><mask>24</mask>
            </route>
    </includeroutes>

</clientconfig>
</azvpnprofile>
```

### Block (exclude) routes

The ability to completely block routes isn't supported by the Azure VPN Client. The Azure VPN Client doesn't support dropping routes from the local routing table. Instead, you can exclude routes from the VPN interface. Modify the downloaded profile XML file and add the **\<excluderoutes>\<route>\<destination>\<mask> \</destination>\</mask>\</route>\</excluderoutes>** tags.

```xml
<azvpnprofile>
<clientconfig>

    <excluderoutes>
        <route>
            <destination>x.x.x.x</destination><mask>24</mask>
        </route>
        <route>
            <destination>y.y.y.y</destination><mask>24</mask>
        </route>
    </excluderoutes>

</clientconfig>
</azvpnprofile>
```

> [!NOTE]
> * To include/exclude multiple destination routes, put each destination address under a separate route tag _(as shown in the above examples)_, because multiple destination addresses in a single route tag won't work.
> * If you encounter the error "_Destination cannot be empty or have more than one entry inside route tag_", check the profile XML file and ensure that the includeroutes/excluderoutes section has only one destination address inside a route tag.

