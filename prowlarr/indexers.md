---
title: Prowlarr Indexers
description: 
published: true
date: 2021-08-28T16:22:09.045Z
tags: 
editor: markdown
dateCreated: 2021-06-06T11:45:31.974Z
---

This page will describe how to add and configure indexers in Prowlarr, and keep them synced with your other programs like Sonarr, Radarr, Lidarr, Readarr, etc.

## Adding an Indexer

To add an indexer, first click on `Indexers` on the left, then `Add Indexer` (the Plus symbol) at the top of the page.

![ind_1_addindexer.png](/assets/prowlarr/ind_1_addindexer.png)

Choose your indexer from the list, or type a partial name in the box to find your indexer. If your indexer is not listed, please use "Generic Newznab" (for Usenet) or "Generic Torznab" (for torrents).

> Using `Generic` assumes your indexer supports standardized *znab formats. If it doesn't, then this will not work
.{.is-info}

> Note that almost every Usenet site is compatible with Generic Newznab.
{.is-warning}

> If your tracker or indexer is not listed and not on our [supported indexers](/prowlarr/supported-indexers) page, you can request it be added via our [Indexer Requests Site](https://requests.prowlarr.com)
{.is-info}

## Editing an Indexer

To edit an indexer, first click on `Indexers` on the left, then click the wrench icon to the far right of the Indexer you wish to edit.

## Viewing an Indexer Id or URL

To view details about an indexer, first click on `Indexers` on the left, then click the i (information) icon to the far right of the Indexer you wish to edit.

Details available may include:

- Id in Prowlarr
- Description
- Encoding
- Language
- Site
- Newznab/Torznab Prowlarr URL

## Indexer Settings

Once you've selected your indexer, there will be a pop-up containing further information you will need to configure it. Note that the specific settings will change slightly for each indexer based on their required fields and the type of indexer you're configuring.

![ind_3_indexer2.png](/assets/prowlarr/ind_3_indexer2.png)

- Name - Select a name for this indexer. When it syncs to your apps, it will add `(Prowlarr)` behind it.

- Enable - Check the box to enable this indexer.

- Redirect - Check the box if a redirect is necessary. There are only a couple of indexers where this is required to avoid being banned. If enabled, this will pass the grab link directly to the application rather than proxying it via Prowlarr.

- App Profile - Select your App Profile here. These can be created in [`Settings` -> `Apps`](/prowlarr/settings#applications). The Standard default, profile already exists, and looks like this:

![ind_3_settingsapps.png](/assets/prowlarr/ind_3_settingsapps.png)

- Query Limit - (Advanced Option) If your indexer limits your API hits per day, you can enter that number here to avoid exceeding the limit.

- Grab Limit - (Advanced Option) If your indexer limits your Grabs per day, you can enter that number here to avoid exceeding the limit.

- Download link - If you're adding a torrent indexer, you may need to choose what kind of download link to use.

- Credentials (API Key, Session ID, Cookie, Username/Password, etc.) - You may have to enter an API key, a session id, or other credentials from your indexer (usually found in your Profile Page or under Security), select search orders, or other options for your specific indexer.

- Tags - Use tags to specify default clients, specify Indexer Proxies, or just to organize your indexers.

- Indexer Priority - (Advanced Option) Select the indexer priority here from 1-50 (1 being highest). These priorities will sync to your apps.

- Test your indexer, and if a green checkmark appears, you're okay to save it. When you save it, depending on your sync settings, it will be added to your apps automatically.

### Adding a custom YML definition

- If you wish to add a custom Cardigann compatible YML definition file for an indexer that is not supported:
  - Navigate to (or create) the Custom Indexer Definition folder named `Custom` within the `Definitions` folder of [Prowlarr's App Data folder](/prowlarr/appdata-directory)
    - Example paths:
      - Windows: `C:\ProgramData\Prowlarr\Definitions\Custom`
      - Linux: `/home/$USER/.config/Prowlarr/Definitions/Custom`
      - OSX: `/Users/$USER/.config/Prowlarr/Definitions/Custom`

  - Save the [Cardigann compatible YML file](/prowlarr/cardigann-yml-definition) within the folder and ensure Prowlarr has permissions to access it.

## Supported Indexers

- [See this wiki page for a list of supported indexers](/prowlarr/supported-indexers/)
