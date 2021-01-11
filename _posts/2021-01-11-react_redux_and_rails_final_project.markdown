---
layout: post
title:      "React Redux and Rails Final Project"
date:       2021-01-11 19:39:26 +0000
permalink:  react_redux_and_rails_final_project
---


Long over due, but I'm finally submitting my final project. I think I lost a lot of hairs following the logic of Redux. The struggle intensifies. 

![](https://pbs.twimg.com/media/EkexQeZWAAExDv5?format=png&name=900x900)

## The stack
* React
* Redux
* Rails API
* Coingecko API
* Twitter authentication

## What does it do?
It's an app for cryptocurrency and stocks data visualization.

[Coingecko API](https://www.coingecko.com/api/documentations/v3) provides trending searches and I used that for the home page. Once the user clicks, it fetches two separate request to gather more data about a specific cryptocurrency. The first request is are back details like price, market cap, twitter, etc. The second request is to get historical data that I used to make the data alive! With that request, I generated candle charts using the highcharts.com component. 

A user can also post comments, but only when they are logged in. I used Twitter as the login process. I used the OAuth gem. Then I used rails session along with the front end react to verify who the current user is. 

## Challenges

The most challenging for me was Redux, following the data flow took me a while to understand. I had to use developer plugins with Chrome browser for better visualization and flow to fetching. I used this [Redux Dev Tools](https://github.com/zalmoxisus/redux-devtools-extension), it's really pretty cool. 


## Next

I like how the project turned out. Lots of things I still want to add, but for now, its a good Minimum Viable Product that scratches my own itch. I wanted a website that can display mutiple stock charts in one page and I was able to do that. I also wanted a search bar that searches Coingecko and therefore skipping the ads and other fluffy non essestial details. I wanted interactive charts, and with the help of Highcharts component and Tradingview widget, I was able to implement it in the app.

I will update this post with my youtube walkthrough as soon as it finishes uploading. Thanks.
