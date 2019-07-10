---
layout: post
title:      "React and Redux Project "
date:       2019-07-03 19:37:02 -0400
permalink:  react_and_redux_project
---


**Concept and Game Flow**
My project concept is an web app that allows users to make decisions in a group using a "Draw Staws" technique. A good use case would be a group of roommates deciding who has to do which chores in a home. In this example, there might be three roommates and three different chores- cleaning the bathroom, cleaning the kitchen, and vacuuming the living room. 

If they were playing Draw Straws in real life, they might each choose a piece of straw from a bundle of straws of varying lengths. The person with the longest piece would get to choose their preferred chore first. The person with the second longest straw would then choose from the remaining two. The person with the shortest straw would have to take the last remaining chore option. 

In this webapp, the straws of varying length are replaced with a function `shuffleDraw(array)` that randomly shuffles the players and assigns each player their draw order from that random shuffle. Once the game name and number of players are set, the player names and options can be entered. From there, the players are shuffled and each in turn is given the chance to choose their preferred option. Once all of the players have chosen an option, the game is saved and redirects to the Game Show page. Aside from the Game Show page, user can also view a list of Games, list of Players, and individual Player Show pages. 

[Draw Straws Demo Video](https://youtu.be/Ly40kjcGB_o)

**API Backend**
The game database is written in Ruby on Rails and includes seed data to allow the user to see a few examples upon startup. The API includes three models: game, player, and option. An option belongs to a player and belongs to a game. A game has many options and many players through options. Similarly, a player can have many options and many games through options. The create method in the Games Controller plays an important role when a new game is saved. The `createGame` action from the frontend fetches a POST request (with new game data) to 'http://localhost:3001/api/games'  which in turn is directed to the games#create controller action. Redux Thunk middleware allows the request to interact with the API asynchonously, so after the response comes back fromt the API, a dispatch can be sent to the Redux store to update the data there.

**Frontend**
The frontend of this web app is written in JavaScript and each component is loaded onto the page through the Router set up in the App component. The Home link is a functional component that simply displays a welcome message and instructions. The All Players and AllGames links route to container components Players and Games respectively. They each contain lists of functional components, PlayerCard and GameCard. A user can also view an individual player or game by clicking on it- they'd be routed to the appropriate Show page to view more detials about it. 

All of the data about players and games is stored in Redux, and that store is first set when the App component's lifecycle method `componentDidMount()` runs. App is connected to the async actions `fetchGames` and `fetchPlayers` in two ways- first, by importing them from the actions folder, and second, by actually `connect`ing them to the React Redux store upon export. When `componentDidMount()` fires, players are fetched from the API in JSON format and then dispatched to the playersReducer to set the Redux state with the incoming data. The same is done for games. 

Later on, when the user is ready to save a new game, a similar process unfolds. As explained in the API Backend section, the `createGame()` action is called in the `handleSubmit()` function in component GameFormFour. This POSTs the new data to the API and then edits the Redux store as well. 

**Conclusions**
Using an API in conjuction with React and Redux is really fun! Together they offer a lot of functionality and open up a lot of different possibilities for a web app. It's been really fun to connect a frontend interface with a backend API to start to explore some of those possibilities.  

[Github Draw Straws Project](https://github.com/abourke09/draw-straws)
