# Play Emby Media Libraries with Zwind

Zwind is a powerful WebDAV Server app for iOS and iPadOS.
With Zwind's resolver add-ons, different types of media content can be mounted into a WebDAV folder tree.

For Emby users, it mainly helps with two workflows:
1. Browse, search, and play movies or TV series from Emby directly on iPhone or iPad.
2. Turn Emby into a WebDAV entry point, so TVs, media players, or other WebDAV-compatible clients can access the media library.

You can think of it as:

**Emby Server -> Zwind WebDAV folder -> Zwind player or third-party WebDAV client**

## Before You Start

1. Install [Zwind](https://apps.apple.com/app/id6755239096).
2. Unlock the **Emby Library Projection Resolver** in Zwind. You can visit [Discord: @Zwind](https://discord.gg/vTyX9qssRF) for a limited-time redemption code.

## Step 1: Create a Local WebDAV Server in Zwind

1. Open Zwind.
2. Tap the **+** button at the bottom left.
3. Choose **Create New Server**.
4. Set **Storage Type** to **Local FileSystem**.
5. Tap **Save**.

After returning to Home:

1. Select the server you just created.
2. Tap the **+** button at the bottom left again.
3. Choose **Add Folder to Current Server**.
4. Select a local folder or an iCloud folder.

## Step 2: Start the Server and Create an Emby Folder

1. Return to Zwind Home.
2. Select the WebDAV server you just created.
3. Tap the start button at the bottom right.
4. After the server starts, Zwind opens its built-in WebDAV Browser.
5. Open the Data Folder you just added.
6. Tap the **+** button at the bottom right.
7. Choose **New Directory**.
8. Enter **Emby** as the folder name.
9. Tap **Create**.

## Step 3: Bind the Emby Folder to a Resolver

1. In Browser, long press the **Emby** folder you just created.
2. Choose **Configure Resolver Binding**.
3. Under **Resolver**, choose **Emby Library Projection Resolver**.

Then enter your Emby connection information:

1. **Emby Endpoints**: enter your Emby Server address.
2. **Username**: enter your Emby username.
3. **Password**: enter your Emby password.

When finished, tap **Save**.

## Step 4: Browse the Emby Media Library

Open the **Emby** folder again. Zwind will generate Emby folders such as:

| Folder | Purpose |
| --- | --- |
| **Libraries** | Browse by Emby library, such as movie libraries or TV libraries. |
| **Recently Added** | Recently added media. |
| **Continue Watching** | Items the current Emby user can continue watching. |
| **Movies**, **Series** | Browse aggregated movie and series views. |
| **Genres**, **People**, **Studios**, **Collections** | Browse by genre, person, studio, or collection. |
| **Search** | Start an Emby search by creating folders named after search terms. |

After opening a media item, you will usually see:

1. playable video files;
2. `.strm` files;
3. `metadata.json` and `metadata.md`;
4. `poster.jpg`;
5. `playback.json`.

Tap a playable video file to play it in Zwind.

## Search Emby Content with Search

Zwind's Emby search is not a text box. It is a folder operation.

1. Open the **Emby** folder.
2. Open **Search**.
3. Tap the **+** button at the bottom right.
4. Choose **New Directory**.
5. Enter what you want to search for as the folder name, such as a title, actor, genre, or year.
6. Tap **Create**.
7. Open the new folder.

Zwind uses that folder name to search your Emby Server and shows the results as browsable media folders.

---

## Play on a TV or Other WebDAV Client

If you want a TV, set-top box, or other media player to access Emby through WebDAV, the device needs to reach Zwind's WebDAV address.

1. Select the server on Zwind Home.
2. Make sure the server is running.
3. Check the server's **Address**.
4. Enter that address in the WebDAV settings of your TV or media player.
5. Open the Emby path you created.

For LAN devices, you can bind the server to `0.0.0.0` or the current LAN address.

---

## Choosing a Media Delivery Mode

In the Emby resolver binding, **Media Delivery** controls how third-party clients open video files.

| Mode | Best for |
| --- | --- |
| **Proxy Media** | Recommended first. The client only needs to reach Zwind, and Zwind reads the media stream from Emby. |
| **Redirect to Emby** | The client can directly reach the Emby Server and can handle Emby's direct playback URL. |
| **Auto** | Zwind chooses proxy or redirect based on the media source. |

---

## Refresh the Emby Cache

Zwind caches some Emby folders, metadata, images, and playback information.

If you just added media in Emby or changed your media library, but Zwind has not shown the change yet, refresh it this way:

1. In Browser, open the **Emby** folder or one of its subfolders.
2. Tap the **+** button at the bottom right.
3. Choose **Refresh Emby**.
4. Wait for **Emby Cache Refreshed**.
5. Pull to refresh the current folder, or open the folder again.

If it still does not change, return to Home and restart this WebDAV server.

---

## Quick Summary

The whole flow is:

**Create a local WebDAV server -> add a Data Folder -> create an Emby folder -> bind the Emby Library Projection Resolver -> browse and play media**

After setup, you only need to open the Emby folder in Zwind and use your Emby media library like a WebDAV directory.

---

## More Help

For more help and discussion, visit:
[Discord: @Zwind](https://discord.gg/vTyX9qssRF)
