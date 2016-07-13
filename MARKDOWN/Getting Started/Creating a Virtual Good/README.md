---
nav_sort: 6
src: /Getting Started/Creating a Virtual Good/README.md
---

# Creating a Virtual Good

## Introduction

In the context of the GameSparks platform, a Virtual Good is any in-game asset that can be awarded, accumulated or bought. This would cover XP points and in-game currencies as well as specific goods that deliver benefits in-game (such as convenience, customisation, competitive advantage, and so on). These can be used and consumed cross-platform:
* You can set up Virtual Goods to be bought as IAPs. This is when you associate the Virtual Goods with the Product IDs of the corresponding items on the stores, and when a good is purchased we can reconcile the store receipts with the items.
* You can define relationships between your Virtual Goods so they can be traded or converted.

There are many ways of awarding Virtual Goods. In this tutorial, we'll award the player with a Virtual Good by "purchasing" it, this is done via [BuyVirtualGoodsRequest](/API Documentation/Request API/Store/BuyVirtualGoodsRequest.md).

## Virtual Good

First you will need to navigate to the Virtual Goods page in your Configurator. Next, add a new Virtual Good with the following parameters (shown below). For an in-depth guide about Virtual Goods click [here](/Documentation/Configurator/Virtual Goods.md). All parameters that are not listed below can be left as default.

  * *Short Code* - This is the reference by which we will award the Virtual Good, these are always unique.
  * *Name* - This field is used when listing Virtual Goods in all of the Returns.
  * *Description* - This field is used to display what the Virtual Good is used for, this is primarily for your benefit in the Virtual Goods Configurator.
  * *Currency 1* - This is the amount of Currency 1 that is required to "purchase" this Virtual Good.


![](img/Create/1.png)

## Test Harness

Now everything is set up, you will need to navigate to the Test Harness and authenticate with one of the players you have [registered](/Getting Started/Using Authentication/README.md) previously. The [previous](/Getting Started/Creating an Achievement/README.md) tutorial showed you how to award your player with some currency via an Achievement. Now you are ready to purchase your first Virtual Good. Just to be sure, let's validate that the player has enough of Currency *1* to purchase the Virtual Good using the [AccountDetailsRequest](/API Documentation/Request API/Player/AccountDetailsRequest.md).

![](img/Create/2.png)


To get the Virtual Good you need to navigate to the Store and then [BuyVirtualGoodsRequest](/API Documentation/Request API/Store/BuyVirtualGoodsRequest.md). To do this you will have to fill in JSON builder with the following values and click Play:

  * *currencyType* \- This is the currency you're "paying" with, for us this is *1*.
  * *quantity* \- This is the quantity of the given Virtual Good that you wish to purchase, for us this is *1*.
  * *shortCode* \- The Short Code of your Virtual Good you will be using in this request, for us this will be the *"Gold_Coin"*.

Although receiving a successful BuyVirtualGoodsResponse is a good indication everything has succeeded, you should still validate this by doing an [AccountDetailsRequest](/API Documentation/Request API/Player/AccountDetailsRequest.md). You should see that the currency 1 has decreased by 1 and that you've been awarded with 1 Gold Coin.

![](img/Create/3.png)

![](img/Create/4.png)
 

## SDK Instructions

* [Unity](/Getting Started/Creating a Virtual Good/Unity Virtual Goods.md)
* [Unreal](/Getting Started/Creating a Virtual Good/Unreal Virtual Goods.md)
* [ActionScript](/Getting Started/Creating a Virtual Good/ActionScript Virtual Goods.md)
