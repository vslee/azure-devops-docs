---
title: Get started with NuGet packages
description: Use Azure Artifacts to publish and consume NuGet packages
ms.technology: devops-artifacts
ms.custom: contperf-fy21q3
ms.topic: quickstart
ms.assetid: C5112218-DA7E-4016-986D-2D0F70DAFA44
ms.date: 02/18/2022
monikerRange: '<= azure-devops'
"recommendations": "true"
---

# Get started with NuGet packages in Azure Artifacts

[!INCLUDE [version-lt-eq-azure-devops](../includes/version-lt-eq-azure-devops.md)]

Azure Artifacts enables developers to publish, and download NuGet packages from different sources such as feeds and public registries. Artifact feeds can be private to share your packages with your team and specific users, or public to share them publicly with anyone on the internet.

## Prerequisites

- An Azure DevOps organization. [Create an organization](../organizations/accounts/create-organization.md), if you don't have one already.
- [Install NuGet client tools](/nuget/install-nuget-client-tools)

## Create a feed

You can create two types of feeds: project-scoped and organization-scoped feeds. All public feeds are scoped to their hosting project and they inherit its visibility settings.

[!INCLUDE [](includes/create-feed.md)]

## Connect to feed

::: moniker range=">= azure-devops-2019"

1. From within your project, select **Artifacts**, and then select your feed.

1. Select **Connect to feed**.

    :::image type="content" source="./media/connect-to-feed-azure-devops-newnav.png" alt-text="Connect to your feed":::

1. Select **NuGet.exe**.

    :::image type="content" source="./media/nuget-connect-feed.png" alt-text="NuGet.exe feed connection":::

1. If this is the first time using Azure Artifacts with Nuget.exe, select **Get the tools** and follow the instructions to install the prerequisites.

    1. Download the [latest NuGet version](https://www.nuget.org/downloads).
    1. Download and install the [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider#azure-artifacts-credential-provider).

1. Follow the instructions in the **Project setup** to add a nuget .config file.

    :::image type="content" source="./media/project-setup.png" alt-text="Project setup":::

::: moniker-end

::: moniker range="tfs-2018"

1. Select **Build and Release** > **Packages**.

1. Select your feed from the dropdown menu.

1. Select **Connect to feed**.

    :::image type="content" source="./media/connect-to-feed.png" alt-text="Connect to feed - TFS":::

1. Select **NuGet** and follow the instruction to connect to your feed.

    :::image type="content" source="./media/connect-to-nuget-feed-tfs.png" alt-text="Connect to NuGet feed - TFS":::

::: moniker-end

## Install and publish a sample NuGet package  

If you don't have a NuGet package but want to try publishing NuGet packages to your feed, you can install the _HelloWorld_ sample package.

1. Install the sample NuGet package:

   ```Command
   nuget install HelloWorld -ExcludeVersion
   ```

1. Set up your nuget.config file and publish your package to your feed:

   ```Command
   nuget sources add -Name <SourceName> -Source <SourceURL> -username <UserName> -password <Pat>
   nuget push -Source <SourceName> -ApiKey key <PackagePath> #example:(.\Get-Hello.1.0.0.nupkg)>
   ```

## Download NuGet packages with Visual Studio

[!INCLUDE [](includes/nuget/consume.md)]

## Related articles

- [Publish NuGet packages with Azure Pipelines](../pipelines/artifacts/nuget.md)
- [Publish packages to NuGet.org](./nuget/publish-to-nuget-org.md)
- [NuGet.org upstream source](./nuget/upstream-sources.md)