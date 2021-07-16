# Readability-Bot
Hey, this document will walk you through setting up a Bot Framework bot using the Bot Composer and LUIS.

## Overview
1. [Prerequisite](https://github.com/Sakyawira/Readability-Bot/tree/main#prerequisite)
2. [Creating Your Bot](https://github.com/Sakyawira/Readability-Bot/tree/main#creating-your-bot)
3. [Deploying Your Bot](https://github.com/Sakyawira/Readability-Bot/tree/main#deploying-your-bot)
4. [Create Intent and Entities](https://github.com/Sakyawira/Readability-Bot/tree/main#create-intent-and-entities)
5. [Dialog System](https://github.com/Sakyawira/ClothPhysics#dialog-system)
6. [Testing Your Bot](https://github.com/Sakyawira/Readability-Bot/tree/main#testing-your-bot)
7. [Calling an API](https://github.com/Sakyawira/Readability-Bot/tree/main#calling-an-API)

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
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/ManageProfile.png?raw=true" />

2. Click add new and fill in the name, choose publish to Azure.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/NewProfile.png?raw=true" />

3. Select "Create new resources".
4. Configure the Publishing Resources. Pick the same resource group that you created before to make it easier to manage. Pick the region that is closest to you.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/ConfigurePublishingResources.png?raw=true" />

5. Make sure you unselect all the optional resources, we already made one of them and will just create the rest manually if we need them.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/UnselectOptionals.png?raw=true" />

6. Click Create.

7. Go to Azure portal https://portal.azure.com/

8. Look for Resource Groups and check if the Resources has been created. You should have these Resources created for you.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/ResourceGroups.png?raw=true" />

9. Now we need to create a Prediction resource (the keen eyed among you might notice that we could have created the Prediction resource in the optionals menu, but there we will not be able to pick the price).
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/MarketPlace.png?raw=true" />

10. Look for Language Understanding. And click create.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/CS.png?raw=true" />

11. Select only the Prediction resource as we already created the authoring resource, and select the F0 pricing tier. Select Review and Create, then Create.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/ConfigCS.png?raw=true" />

12. Now that we have both our Prediction and Authoring Resource, we must assign them to our Bot Composer profile.


13. Go to Bot Composer, go to Publish > Publishing Profile > yourProfile > Edit.


14. Instead of Creating New Resources, we now want to import existing resources. 
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/ConfigResources.png?raw=true" />

15. In this json looking file, just under name, you want to add the following code (replace "Your-LUIS-Prediction" with the name of your prediction resource)
```javascript
    "luisResource": "Your-LUIS-Prediction"
```
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/luisPrediction.png?raw=true" />

16. Scroll down and fill the luis settings with the Key and Endpoints that can be found in your respective authoring and prediction resources on Azure Portal.
<img src="https://github.com/Sakyawira/Readability-Bot/blob/main/Media/luisSettings.png?raw=true" />

17. Click import.


18. Go back to Publish and Publishh the Bot. Wait a couple of minutes and your bot should be published.

## Create Intent and Entities

Intent is a way for the Bot to recognise what you want it to do. Using LUIS, we can make the Bot recognise different intents. To add a new intent to the bot go to Create, go to any of your dialog, and click on the three dots. Select "Add ew trigger."

The name of the trigger will be the same as the name of your intent. The trigger phrases are the different sentences that might trigger this intent. Essentially, LUIS will train a NLP model to recognise the intent using these senteces.

Name your trigger as "FetchAnimeQuotes" and copy the following code to the phrases.

```.lu
- tell me a quote from {anime=Shingeki no Kyojin}
- can you quote {anime=Naruto} for me 
- what is a famous quote from {anime=fate/zero}
- tell me a quote from {anime=re:zero}
- show me a quote from {anime=Berserk}
- quote {anime=Death Note}


> entity definitions:
@ ml anime
```
If you have noticed that there is a line "@ ml anime". This is our entity. Basically, we are also training LUIS to recognise a specific word /phrase in our sentence as a variable. We will then be able to extract this variable to be used in our dialog logic.

Go ahead and submit. You have now created a new intent. 

## Dialog System

I am going to go through some of the features the dialog has. Dialog is basically the logical component that handles the interaction between the user and the bot. For example, in it, you can design what the bot will do if it recognises the intent in the user's message.

For example, let's make the bot tell us the anime it recognises.

Go to the FethAnimeTrigger, and click on the small blue plus sign. Select "Create condition" > "Branch:If/Else". On the dialog to the side paste this code:
```
=exist(@anime)
```
So, now your bot will be able to do different things based on whether it recognises any anime title in your sentence.

Next up, we want the bot to Set a property for us to use. This is basically like setting a global variable. Click the blue plus sign under "True", and select "Manage Properties > Set a Property". On the property dialog box, paste "user.anime", on the value paste "=@anime".

Now let's make the bot Send a Response to us. Under the Set a Property node, click the blue plus sign again. This time we want to use the "Send a response" node. On the Responses dialog box, paste in this code:

```
Fecthing quotes from "${user.anime}"...
```

Great! Now, we need to test whether this work :D

## Testing Your Bot

1. You will want to use Bot Framework Emulator here. You can also use the built in Web Chat, but the Emulator will help you debug.

2. On the top right of the composer, click on stat Bot. One the Bot is started, if you have installed the Bot Emulator, you can select "Test in Emulator".

3. On the Emulator, typed in "get a quote from Naruto".

4. And you should see this:

## Calling an API

Now, let's do something more interesting. We are now going to call an API that will actually fetch a quote from an anime. Under the send a response node, add a new node called "Send an HTTP request". There, you want to put this API:

```
https://animechan.vercel.app/api/quotes/anime?title=${user.anime}
```

Notice how we put the property "user.anim"? We can reference our property almost anywhere, so it will be useful here! Make sure you also set the result property, which will store the response of the HTTP request. In our case let's set it to "turn.results"

Now, we also want to generate a random number. The reason is the response of this API is actually not one quote, but 10 of them. We want to make sure that we don't return the same quote everytime plus another way to showcase the thing you can do in the composer!

Add another Set a Property node. Set the property as "user.randomNumber" and set its value to "=rand(0,9)". This will generate random number between 0 and 9.

Finally wa want the Bot to send you a response. Add a response node and paste this code to its responses dialog box:

```
"${turn.results.content[user.randomNumber].quote}" 
\- ${turn.results.content[user.randomNumber].character} from ${turn.results.content[user.randomNumber].anime}
```

And that's it. Go ahead and Restart your Bot and Chat, and it should show something like this: