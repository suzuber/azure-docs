---
title: Use the Remote Desktop client to connect to Azure Virtual Desktop
description: Learn how to connect to Azure Virtual Desktop using the Remote Desktop client.
ms.topic: how-to
ms.date: 02/26/2025
ms.author: avdcontent
author: dougeby
ROBOTS: NOINDEX, NOFOLLOW
---

# Use the Remote Desktop client to connect to Azure Virtual Desktop

This article shows you how to connect to Azure Virtual Desktop with the Remote Desktop client.

For Windows there are multiple options:

- **Remote Desktop client for Windows**: A standalone MSI installer. When installed, the application name is *Remote Desktop*.

- **Remote Desktop app for Windows**: Comes from the Microsoft Store. When installed, the application name is *Remote Desktop*.

> [!IMPORTANT]
> Starting March 27, 2026, the Remote Desktop client for Windows (MSI) will no longer be supported. Users should begin migrating to Windows App to ensure continued access to their Azure Virtual Desktop and Windows 365 resources after this date.
>
> Starting May 27, 2025, the Remote Desktop app for Windows from the Microsoft Store will no longer be supported or available for download and installation. Users must transition to Windows App to ensure continued access to Windows 365, Azure Virtual Desktop, and Microsoft Dev Box.
>
> For more information about Windows App, see [Get started with Windows App to connect to devices and apps](/windows-app/get-started-connect-devices-desktops-apps). Learn more about [Known issues and limitations of Windows App](/windows-app/troubleshoot-known-issues-limitations?tabs=windows). 

## Prerequisites

Select a tab for the platform you're using.

# [Windows (MSI)](#tab/windows-msrdc-msi)

Before you can connect to your devices and apps from Windows, you need:

- Internet access.

- A device running one of the following supported versions of Windows:
  - Windows 11
  - Windows 10
  - Windows Server 2022
  - Windows Server 2019
  - Windows Server 2016

- .NET Framework 4.6.2 or later. You may need to install this on Windows Server 2016, and some versions of Windows 10. To download the latest version, see [Download .NET Framework](https://dotnet.microsoft.com/download/dotnet-framework).

### Download and install the Remote Desktop client for Windows (MSI)

Here's how to install the Remote Desktop client for Windows using the MSI installer. If you want to deploy the Remote Desktop client in an enterprise, you can use `msiexec` from the command line to install the MSI file. For more information, see [Enterprise deployment](client-features-windows-msrdc.md#enterprise-deployment).

1. Download the Remote Desktop client installer, choosing the correct version for your device:

   - [Windows 64-bit](https://go.microsoft.com/fwlink/?linkid=2139369) *(most common)*
   - [Windows 32-bit](https://go.microsoft.com/fwlink/?linkid=2139456)
   - [Windows ARM64](https://go.microsoft.com/fwlink/?linkid=2139370)

1. Run the installer by double-clicking the file you downloaded.

1. On the welcome screen, select **Next**.

1. To accept the end-user license agreement, check the box for **I accept the terms in the License Agreement**, then select **Next**.

1. For the Installation Scope, select one of the following options:

   - **Install just for you**: Remote Desktop will be installed in a per-user folder and be available just for your user account. You don't need local Administrator privileges.
   - **Install for all users of this machine**: Remote Desktop will be installed in a per-machine folder and be available for all users. You must have local Administrator privileges

1. Select **Install**.

1. Once installation has completed, select **Finish**.

1. If you left the box for **Launch Remote Desktop when setup exits** selected, the Remote Desktop client will automatically open. Alternatively to launch the client after installation, use the Start menu to search for and select **Remote Desktop**.

> [!IMPORTANT]
> If you have the Remote Desktop client (MSI) and the Azure Virtual Desktop app from the Microsoft Store installed on the same device, you may see the message that begins **A version of this application called Azure Virtual Desktop was installed from the Microsoft Store**. Both apps are supported, and you have the option to choose **Continue anyway**, however it could be confusing to use the same remote resource across both apps. We recommend using only one version of the app at a time.

# [Windows (Store)](#tab/windows-urdc)

To access your resources, you need:

- Internet access.

- A device running one of the following supported versions of Windows:
  - Windows 11
  - Windows 10

> [!IMPORTANT]
> The Remote Desktop client for iOS/iPadOS isn't available for download anymore and it's replaced by Windows App. For more information on the Windows App update, see [What is Windows App](/windows-app/overview) and [Get started with Windows App](/windows-app/get-started-connect-devices-desktops-apps?tabs=windows-avd&pivots=azure-virtual-desktop) to connect to desktops and apps.

# [macOS](#tab/macos)

Before you can connect to your devices and apps from macOS, you need:

- Internet access.

- A device running macOS 12 or later.

> [!IMPORTANT]
> The macOS version of the Remote Desktop client isn't available for download anymore. You should use Windows App instead to connect to your desktops and apps. For more information on the Windows App update, see [What is Windows App](/windows-app/overview) and [Get started with Windows App](/windows-app/get-started-connect-devices-desktops-apps?tabs=macos-avd&pivots=azure-virtual-desktop) to connect to desktops and apps.

# [iOS/iPadOS](#tab/ios-ipados)

Before you can connect to your devices and apps from iOS or iPadOS, you need:

- Internet access.

- An iPhone running iOS 16 or later or an iPad running iPadOS 16 or later.

> [!IMPORTANT]
> The iOS/iPadOS version of the Remote Desktop client isn't available for download anymore. You should use Windows App instead to connect to your desktops and apps. For more information on the Windows App update, see [What is Windows App](/windows-app/overview) and [Get started with Windows App](/windows-app/get-started-connect-devices-desktops-apps?tabs=ios-ipados-avd&pivots=azure-virtual-desktop) to connect to desktops and apps.

# [Android/Chrome OS](#tab/android)

Before you can connect to your devices and apps from Android or Chrome OS, you need:

- Internet access

- One of the following:
  - Smartphone or tablet running Android 9 or later.
  - Chromebook running Chrome OS 53 or later. Learn more about [Android applications running in Chrome OS](https://www.chromium.org/chromium-os/chrome-os-systems-supporting-android-apps/).

- Download and install the Remote Desktop client from [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.rdc.androidx).

> [!IMPORTANT]
> The Android client is not available on platforms built on the Android Open Source Project (AOSP) that do not include Google Mobile Services (GMS), the client is only available through the canonical Google Play Store.

# [Web browser](#tab/web)

Before you can access your resources, you'll need to meet the prerequisites:

- Internet access.

- A supported web browser. While any HTML5-capable web browser should work, we officially support the following web browsers and operating systems:

   | Web browser       | Supported operating system       | Notes               |
   |-------------------|----------------------------------|---------------------|
   | Microsoft Edge    | Windows, macOS, Linux, Chrome OS | Version 79 or later |
   | Google Chrome     | Windows, macOS, Linux, Chrome OS | Version 57 or later |
   | Apple Safari      | macOS                            | Version 11 or later |
   | Mozilla Firefox   | Windows, macOS, Linux            | Version 55 or later |

> [!IMPORTANT]
> The Remote Desktop Web client doesn't support mobile web browsers or Internet Explorer. Instead of Internet Explorer, we recommend that you use Microsoft Edge with the Remote Desktop Web client instead.
>
> Starting June 15, 2025, the Remote Desktop Web client will have updated browser requirements. Ensure your browser is updated and meets the following requirements by this date:
> - Remote Desktop will only support browser versions that are 12 months old on a rolling basis.
> - Your browser must support the AVC codec. Most browsers support this codec.
> - Ensure your browser has WebGL enabled. WebGL is enabled by default on most recent browser versions.

---

## Subscribe to a workspace and connect to your desktops and applications

Select a tab for the platform you're using.

# [Windows (MSI)](#tab/windows-msrdc-msi)

### Subscribe to a workspace

A workspace combines all the desktops and applications that have been made available to you by your admin. To be able to see these in the Remote Desktop client, you need to subscribe to the workspace by following these steps:

1. Open the **Remote Desktop** app on your device.

1. The first time you subscribe to a workspace, from the **Let's get started** screen, select **Subscribe** or **Subscribe with URL**.

   - If you selected **Subscribe**, sign in with your user account when prompted, for example `user@contoso.com`. After a few seconds, your workspaces should show the desktops and applications that have been made available to you by your admin.

     If you see the message **No workspace is associated with this email address**, your admin might not have set up email discovery, or you're using an Azure environment that isn't Azure cloud, such as Azure for US Government. Try the steps to **Subscribe with URL** instead.

   - If you selected **Subscribe with URL**, in the **Email or Workspace URL** box, enter the relevant URL from the following table. After a few seconds, the message **We found Workspaces at the following URLs** should be displayed.

      | Azure environment | Workspace URL |
      |--|--|
      | Azure cloud *(most common)* | `https://rdweb.wvd.microsoft.com` |
      | Azure for US Government | `https://rdweb.wvd.azure.us/api/arm/feeddiscovery` |
      | Azure operated by 21Vianet | `https://rdweb.wvd.azure.cn/api/arm/feeddiscovery` |

1. Select **Next**.

1. Sign in with your user account when prompted. After a few seconds, the workspace should show the desktops and applications that have been made available to you by your admin.

Once you've subscribed to a workspace, its content will update automatically regularly and each time you start the client. Resources may be added, changed, or removed based on changes made by your admin.

### Connect to your desktops and applications

To connect to your desktops and applications:

1. Open the **Remote Desktop** client on your device.

1. Double-click one of the icons to launch a session to Azure Virtual Desktop. You may be prompted to enter the password for your user account again, depending on how your admin has configured Azure Virtual Desktop.

### Insider releases

If you want to help us test new builds before they're released, you should download our Insider releases. Organizations can use the Insider releases to validate new versions for their users before they're generally available. For more information, see [Enable Insider releases](client-features-windows-msrdc.md#enable-insider-releases).

# [Windows (Store)](#tab/windows-urdc)

A workspace combines all the desktops and applications that have been made available to you by your admin. To be able to see these in the Remote Desktop client, you need to subscribe to the workspace by following these steps:

1. Open the **Remote Desktop** app on your device.

1. In the Connection Center, select **+ Add**, then select **Workspaces**.

1. In the **Email or Workspace URL** box, either enter your user account, for example `user@contoso.com`, or the relevant URL from the following table. After a few seconds, the message **We found Workspaces at the following URLs** should be displayed.

   If you see the message **We couldn't find any Workspaces associated with this email address. Try providing a URL instead**, your admin might not have set up email discovery. Use one of the following workspace URLs instead.

   | Azure environment | Workspace URL |
   |--|--|
   | Azure cloud *(most common)* | `https://rdweb.wvd.microsoft.com` |
   | Azure for US Government | `https://rdweb.wvd.azure.us/api/arm/feeddiscovery` |
   | Azure operated by 21Vianet | `https://rdweb.wvd.azure.cn/api/arm/feeddiscovery` |

1. Select **Subscribe**.

1. Sign in with your user account. After a few seconds, your workspaces should show the desktops and applications that have been made available to you by your admin.

### Connect to your desktops and applications

Once you've subscribed to a workspace, here's how to connect:

1. Open the **Remote Desktop** app on your device.

1. Select one of the icons to launch a session to Azure Virtual Desktop. You may be prompted to enter the password for your user account again, depending on how your admin has configured Azure Virtual Desktop.

# [macOS](#tab/macos)

> [!IMPORTANT]
> The Remote Desktop client for macOS is no longer available to download. It's been replaced by Windows App. To learn more about Windows App, see [Get started with Windows App to connect to devices and apps](/windows-app/get-started-connect-devices-desktops-apps).

### Subscribe to a workspace

A workspace combines all the desktops and applications that have been made available to you by your admin. To be able to see these in the Remote Desktop client, you need to subscribe to the workspace by following these steps:

1. Open the **Microsoft Remote Desktop** app on your device.

1. In the Connection Center, select **+**, then select **Add Workspace**.

1. In the **Email or Workspace URL** box, either enter your user account, for example `user@contoso.com`, or the relevant URL from the following table. After a few seconds, the message **A workspace is associated with this URL** should be displayed.

   > [!TIP]
   > If you see the message **No workspace is associated with this email address**, your admin might not have set up email discovery. Use one of the following workspace URLs instead.

   | Azure environment | Workspace URL |
   |--|--|
   | Azure cloud *(most common)* | `https://rdweb.wvd.microsoft.com` |
   | Azure for US Government | `https://rdweb.wvd.azure.us/api/arm/feeddiscovery` |
   | Azure operated by 21Vianet | `https://rdweb.wvd.azure.cn/api/arm/feeddiscovery` |

1. Select **Add**.

1. Sign in with your user account. After a few seconds, your workspaces should show the desktops and applications that have been made available to you by your admin.

Once you've subscribed to a workspace, its content will update automatically every six hours and each time you start the client. Resources may be added, changed, or removed based on changes made by your admin.

### Connect to your desktops and applications

To connect to your desktops and applications:

1. Open the **Microsoft Remote Desktop** app on your device.

1. Double-click one of the icons to launch a session to Azure Virtual Desktop. You may be prompted to enter the password for your user account again, depending on how your admin has configured Azure Virtual Desktop.

# [iOS/iPadOS](#tab/ios-ipados)

> [!IMPORTANT]
> The Remote Desktop client for iOS/iPadOS is no longer available to download. It's been replaced by Windows App. To learn more about Windows App, see [Get started with Windows App to connect to devices and apps](/windows-app/get-started-connect-devices-desktops-apps)

### Subscribe to a workspace

A workspace combines all the desktops and applications that have been made available to you by your admin. To be able to see these in the Remote Desktop client, you need to subscribe to the workspace by following these steps:

1. Open the **RD Client** app on your device.

1. In the Connection Center, tap **+**, then tap **Add Workspace**.

1. In the **Email or Workspace URL** box, either enter your user account, for example `user@contoso.com`, or the relevant URL from the following table. After a few seconds, the message **A workspace is associated with this URL** should be displayed.

   > [!TIP]
   > If you see the message **No workspace is associated with this email address**, your admin might not have set up email discovery. Use one of the following workspace URLs instead.

   | Azure environment | Workspace URL |
   |--|--|
   | Azure cloud *(most common)* | `https://rdweb.wvd.microsoft.com` |
   | Azure for US Government | `https://rdweb.wvd.azure.us/api/arm/feeddiscovery` |
   | Azure operated by 21Vianet | `https://rdweb.wvd.azure.cn/api/arm/feeddiscovery` |

1. Tap **Next**.

1. Sign in with your user account. After a few seconds, your workspaces should show the desktops and applications that have been made available to you by your admin.

Once you've subscribed to a workspace, its content will update automatically regularly. Resources may be added, changed, or removed based on changes made by your admin.

### Connect to your desktops and applications

To connect to your desktops and applications:

1. Open the **RD Client** app on your device.

1. Tap one of the icons to launch a session to Azure Virtual Desktop. You may be prompted to enter the password for your user account again, depending on how your admin has configured Azure Virtual Desktop.

# [Android/Chrome OS](#tab/android)

> [!IMPORTANT]
> The Remote Desktop client for Android is being replaced by Windows App. To learn more about Windows App, see [Get started with Windows App to connect to devices and apps](/windows-app/get-started-connect-devices-desktops-apps).

### Subscribe to a workspace

A workspace combines all the desktops and applications that have been made available to you by your admin. To be able to see these in the Remote Desktop client, you need to subscribe to the workspace by following these steps:

1. Open the **RD Client** app on your device.

1. In the Connection Center, tap **+**, then tap **Add Workspace**.

1. In the **Email or Workspace URL** box, either enter your user account, for example `user@contoso.com`, or the relevant URL from the following table. After a few seconds, the message **A workspace is associated with this URL** should be displayed.

   > [!TIP]
   > If you see the message **No workspace is associated with this email address**, your admin might not have set up email discovery. Use one of the following workspace URLs instead.

   | Azure environment | Workspace URL |
   |--|--|
   | Azure cloud *(most common)* | `https://rdweb.wvd.microsoft.com` |
   | Azure for US Government | `https://rdweb.wvd.azure.us/api/arm/feeddiscovery` |
   | Azure operated by 21Vianet | `https://rdweb.wvd.azure.cn/api/arm/feeddiscovery` |

1. Tap **Next**.

1. Sign in with your user account. After a few seconds, your workspaces should show the desktops and applications that have been made available to you by your admin.

Once you've subscribed to a workspace, its content will update automatically regularly. Resources may be added, changed, or removed based on changes made by your admin.

### Connect to your desktops and applications

To connect to your desktops and applications:

1. Open the **RD Client** app on your device.

1. Tap one of the icons to launch a session to Azure Virtual Desktop. You may be prompted to enter the password for your user account again, and to make sure you trust the remote PC before you connect, depending on how your admin has configured Azure Virtual Desktop.

# [Web browser](#tab/web)

When you sign in to the Remote Desktop Web client, you'll see your workspaces. A workspace combines all the desktops and applications that have been made available to you by your admin. You sign in by following these steps:

1. Open your web browser.

1. Go to one of the following URLs:

   | Azure environment | Workspace URL |
   |--|--|
   | Azure cloud *(most common)* | [https://client.wvd.microsoft.com/arm/webclient/](https://client.wvd.microsoft.com/arm/webclient/) |
   | Azure cloud (classic) | [https://client.wvd.microsoft.com/webclient/index.html](https://client.wvd.microsoft.com/webclient/index.html) |
   | Azure for US Government | [https://rdweb.wvd.azure.us/arm/webclient/](https://rdweb.wvd.azure.us/arm/webclient/) |
   | Azure operated by 21Vianet | [https://rdweb.wvd.azure.cn/arm/webclient/](https://rdweb.wvd.azure.cn/arm/webclient/) |

1. Sign in with your user account. Once you've signed in successfully, your workspaces should show the desktops and applications that have been made available to you by your admin.

1. Select one of the icons to launch a session to Azure Virtual Desktop. You may be prompted to enter the password for your user account again, depending on how your admin has configured Azure Virtual Desktop.

1. A prompt for **Access local resources** may be displayed asking you to confirm which local resources you want to be available in the remote session. Make your selection, then select **Allow**.

>[!TIP]
>If you've already signed in to the web browser with a different Microsoft Entra account than the one you want to use for Azure Virtual Desktop, you should either sign out or use a private browser window.

---

## Next steps

To learn more about the features of the Remote Desktop client for Windows, check out [Use features of the Remote Desktop client for Windows when connecting to Azure Virtual Desktop](client-features-windows-msrdc.md).
