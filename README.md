# Readability-Bot
Hey, this document will walk you through setting up a Bot Framework bot using the Bot Composer and LUIS.

## Overview
1. [Prerequisite](https://github.com/Sakyawira/Readability-Bot/tree/main#prerequisite)
2. [Creating Your Bot](https://github.com/Sakyawira/Readability-Bot/tree/main#creating-your-bot)
3. [Deploying Your Bot](https://github.com/Sakyawira/Readability-Bot/tree/main#deploying-your-bot)
4. [Create Intent](https://github.com/Sakyawira/ClothPhysics#Sphere-Collision)
5. [Create Entities](https://github.com/Sakyawira/ClothPhysics#Pyramid-Collision)
6. [Dialog System](https://github.com/Sakyawira/ClothPhysics#Burning)
7. [Calling an API](https://github.com/Sakyawira/ClothPhysics#Dynamic-Particle-Densityn)
8. [Testing Your Bot](https://github.com/Sakyawira/ClothPhysics#Dynamic-Size)

## Prerequisite
In order for you to follow along with this documentation, you must have the following and their dependencies installed in your computer.
1. [Bot Composer](https://docs.microsoft.com/en-us/composer/install-composer?tabs=windows)
2. [Bot Framework Emulator](https://github.com/microsoft/BotFramework-Emulator/releases/tag/v4.13.0)

You will also need the following account.
1. [Microsoft Azure](https://azure.microsoft.com/en-us/)

## Creating Your Bot
1. Click on "Create New".
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/CreateNew.png?raw=true" />
2. Pick the C# Core Bot with Language.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/CoreBotWithLanguage.png?raw=true" />
3. Name your bot and pick the Azure Web App runtime.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/NameAndRuntime.png?raw=true" />
4. Your bot should be created after a couple of minutes. However, you need to now setup LUIS, click on the "Set up Language Understanding" label.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/SetUpLUIS.png?raw=true" />
5. Select "Create and Configure New Azure Services"
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/Create%20and%20Configure%20New%20Azure%20Resources.png?raw=true" />
6. Login to Azure.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/LoginToAzure.png?raw=true" />
7. Select your subscription. If you have not created a subscription yet, you can either use your student email to get a free subscription or sign up for a free trial using a credit card.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/PickSubs.png?raw=true" />
8. Create an Azure Resource Group by selecting "Create new", and pick "Australia East" for your region for best connection.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/PickResourceGroupAndRegion.png?raw=true" />

## Deploying Your Bot

1. Create a publishing profile. Go to Configuration -> Connections -> Select Publishing Profile -> Manage Profile.
2. Click add new and fill in the name, choose publish to Azure.
3. Select "Create new resources".
4. Configure the Publishing Resources. Pick the same resource group that you created before to make it easier to manage. Pick the region that is closest to you.
5. Make sure you unselect all the optional resources, we already made one of them and will just create the rest manually if we need them.
6. Click Create.
7. Go to Azure portal https://portal.azure.com/
8. Look for Resource Groups and check if the Resources has been created. You should have these Resources created for you.
9. Now we need to create a Prediction resource (the keen eyed among you might notice that we could have created the Prediction resource in the optionals menu, but there we could will not be able to pick the price).
10. Look for Language Understanding. And click create.
11. Select only the Prediction resource as we already created the authoring resource, and select the F0 pricing tier. Select Review and Create, then Create.
12. Now that we have both our Prediction and Authoring Resource, we must assign them to our Bot Composer profile.
13. Go to Bot Composer, go to Publish > Publishing Profile > yourProfile > Edit.
14. Instead of Creating New Resources, we now want to import existing resources. 
15. In this json looking file, just under name, you want to add the following code (replace "Your-LUIS-Prediction" with the name of your prediction resource)
```javascript
    "luisResource": "Your-LUIS-Prediction"
```
16. Scroll down and fill the luis settings with the Key and Endpoints that can be found in your respective authoring and prediction resources on Azure Portal.
17. Click import.
18. Go back to Publish and Publishh the Bot. Wait a couple of minutes and your bot should be published.

