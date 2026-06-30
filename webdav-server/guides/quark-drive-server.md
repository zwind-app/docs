---
title: Configure a Quark Drive server
description: Create a QuarkDrive server in Zwind, paste a Quark cookie, start the server, and open the Quark Drive folder in Browser.
seoTitle: "Configure a Quark Drive WebDAV server on iPhone with Zwind"
keywords:
  - Quark Drive WebDAV
  - QuarkDrive server
  - Zwind Quark Drive
  - iPhone Quark WebDAV
productSlug: webdav-server
section: Guides
parent: guides
order: 33
tags:
  - guide
  - quark
  - webdav
publishedAt: 2026-06-30
updatedAt: 2026-06-30
draft: false
---

Use **QuarkDrive** when you want a Zwind server entry to expose the files in a Quark Drive account. Zwind stores the Quark cookie in the server configuration and uses that session when it reads the cloud drive.

## Prepare the Quark cookie

The **Quark Cookie** is an account session credential. Anyone who has a working cookie can act as that signed-in session, so use a trusted tool or workflow for your own account and paste only the cookie value into Zwind.

The value normally looks like cookie fragments separated by semicolons, for example `__puus=...; kps=...`. Do not paste a full `Cookie:` header label, request URL, browser command, or unrelated text around it.

If the cookie later expires, the server entry can stay in place. You only need to get a fresh cookie and replace the old value in **Quark Cookie**.

## Choose QuarkDrive storage

On a fresh Home screen, tap **Use Quark Drive**. If you already have a server, tap the **+** button at the bottom left and create a new server, then choose **QuarkDrive** as the storage type.

![Choose Use Quark Drive from the first server card.](/assets/docs/webdav-server/quark-drive-server/use-quark-drive.png)

On the configuration screen, confirm that **Storage Type** is **QuarkDrive**. The form should show **Quark Cookie** under the common server fields.

![The QuarkDrive form contains a Quark Cookie field.](/assets/docs/webdav-server/quark-drive-server/quark-drive-form.png)

## Paste the cookie and save

Paste the cookie into **Quark Cookie**. The screenshot uses a short placeholder; use the real cookie from your own Quark session.

![The Quark Cookie field filled with a placeholder value.](/assets/docs/webdav-server/quark-drive-server/quark-cookie-filled.png)

Keep the default **Port** value `0` if you want Zwind to pick an available port when the server starts. Tap **Save**. If **Save** is still disabled, check that **Quark Cookie** is not empty.

## Start the server and browse Quark Drive

After saving, the server appears on Home with a virtual root folder named **/QuarkDrive**. Tap **Start Server** to start it.

![The saved QuarkDrive server shows the QuarkDrive root folder.](/assets/docs/webdav-server/quark-drive-server/quark-server-card.png)

When the server is running, open the server menu at the bottom right and choose **Browse Files**. Browser opens the server root; open **/QuarkDrive** to browse the cloud drive folders and files available to the cookie's Quark account.

![Use Browse Files from the server menu to open the server in Browser.](/assets/docs/webdav-server/quark-drive-server/browser-menu.png)

If the cookie is a placeholder or has expired, the form can still be saved, but Browser will not be able to list the real Quark Drive contents.

## Replace an expired cookie

When Quark signs out the session or the cookie expires, open Home, select the QuarkDrive server, and tap **Edit**. Replace the old **Quark Cookie** value with a fresh cookie, then tap **Save**.

If the server was already running, stop and start it again before browsing. Then reopen **Browse Files** and refresh the Browser directory.

## When Quark Drive cannot be accessed

Check the failure by category:

| What you see | What to check |
| --- | --- |
| **Save** is disabled | **Quark Cookie** is empty. Paste the cookie value, not only spaces or a label. |
| Server starts, but Browser cannot list **/QuarkDrive** | The cookie is expired, incomplete, or from a signed-out session. Replace it with a fresh cookie. |
| Browser waits or reports a connection/network error | The device cannot reach Quark's service from the current network. Try again on a network that can open Quark Drive normally. |
| Browser opens but the expected folders are missing | The signed-in Quark account does not have access to those files, or the cloud drive folder is empty for that account. Confirm the same account in the Quark app or website. |
