---
title: "Dialogue System"
layout: single
toc: true
toc_label: "Post Content"
categories:
    - Dialogue
tags:
    - Dialogue
    - Core Systems
---

## Introduction

This is a branching, modular dialogue system.

Core Concept: Create an infinite branching dialogue system that can rival that of CRPG's such as Baldur's Gate 1 & 2, Pathfinder Kingmaker and Wrath of the Righteous, Neverwinter Nights and Pillars of Eternity 1 & 2.




## DialogueComponent

The DialogueComponent is the brains behind the whole system. This can be applied to any AActor, APawn or ACharacter that the player can converse with. This controls the flow of the dialogue via a DataTable.

![DialogueComponent.h](/assets/DialogueSystem/DialogueComponentH.png)

![DialogueComponent.cpp](/assets/DialogueSystem/DialogueComponentCPP.png)

The DialogueComponent holds information to the DialogueWidget, DialogueDataTable and the CurrentDialogueID. It also had information of the NPC that it is associated with, however that was removed, and I just didn't remove the commented out code, or the NPC line from the header file before the screenshot was taken.

***StartDialogue()*** being BlueprintCallable makes this system extremely modular with blueprints, allowing it to be attached to any actor in the game at all, making the system modular to apply.

***SelectPlayerResponse(FName NextDialogueID)*** is what handles the branching system entirely. This gets the DialogueID line from the DataTable that is tied to the player response. If the player response DialogueID is 'none' it ends the conversation, and closes the dialogue window.

***ShowDialogue(FName DialogueID)*** This is where the dialogue is pulled from the data table and shown to the player. If the dialogue data is nullptr, nothing will happen. If the DialogueWidget doesn't exist, it will create one, then update the dialogue. 

This works by finding the row 'DialogueID' in the DataTable, which must be named appropriately to the PlayerResponse DialogueID.




## DialogueStructures

![DialogueStructures.h](/assets/DialogueSystem/DialogueStructuresH.png)

The dialogue structures are the DataTable and the player's responses. The ***FPlayerResponse*** struct contains the *ResponseText*, which is the text that will appear on the button that the player has the option to press to continue the dialogue, and *NextDialogueID* which is where the dialogue will go if the option is selected.
***FDialogueData*** contains the NPC's dialogue, and an array of ***FPlayerResponse***, this allows the player to have multiple options for each part of the dialogue, this could effectivly be infinite, but I'm sure there's a limit.



![DialogueDataTable1](/assets/DialogueSystem/DialogueDT1.png)

This is an example of the dialogue data table that can hold the infinitely branching dialogue. The **Row Name** is what MUST match the NextDialogueID of the PlayerResponse. In this case, one of the responses from the player must lead to the NextDialogueID of 'WhatAreYou'.

![DialogueDataTable2](/assets/DialogueSystem/DialogueDT2.png)

This is the whole information for row *Initial*, which is the greeting to the player. The player is given two options here, to ask the NPC what they are, or to just say goodbye. Asking the NPC 'What are you?' leads to the NextDialogueID of WhatAreYou, like what was stated above, this matches the next row. Also the player can say 'Goodbye' which leads to NextDialogueID of 'none' which looking back to the DialogueComponent, you can see that 'none' ends the dialogue.

![DialogueDataTable3](/assets/DialogueSystem/DialogueDT3.png)

This screenshot is a little redundant, but it's a way to show how the dialogue can be simply ended by giving the player one choice. The Response Text could also be set to something like 'End Conversation', or 'End Dialogue' too.

## Dialogue Widget

***TO BE ADDED***

## Dialogue Response Button

***TO BE ADDED***

## Basic NPC

***TO BE ADDED***