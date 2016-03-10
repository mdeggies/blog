---
layout: post
title: "Technical Challenge: Learn from my Mistakes"
date: 2016-03-09 20:38:32 -0800
comments: true
categories: [programming, interviews, javascript]
---


![Connect4](http://i.imgur.com/CMt4ZDx.png?1)

After applying to a few startups on Angellist, I was super excited to have gotten through my very first phone interview. At the end of the call, the HR rep scheduled me for a technical challenge. He said I would have up to 24 hours to complete the challenge, but that I'd have to check in at the 2 hour mark and report my progress. I would be assessed on both the first draft of my code at the 2 hour mark, and the final version.

The task was pretty straightforward: to create Connect 4 in the language I felt most comfortable in. Since I applied for a backend position, I wasn't supposed to create any front-end or accept any user input. The program was supposed to simulate the turns taken by players and have a function to print out the board in ASCII, like so:

``` javascript ASCII output after two turns have been taken
* * * * * * *
* * * * * * *
* * * * * * *
* * * * * * *
* X O * * * *
```

Now.. this was a pretty challenging task for me. I got the basic version down, but it took me about 4 hours to complete and another hour of debugging before I felt comfortable enough to submit the final version. Here's what I learned from the whole process:

## Don't freak out!

Once I got the challenge emailed to me, I set an alarm for 2 hours. While this helped me keep track of my time, it also made me really anxious as I saw the minutes slipping by. I would have gotten further along much faster if I didn't obsessively check the time every five minutes.

## Find a quiet place to work

When living in a house with 20 other people, it's hard to find a quiet place to think, let alone code. My advice is: either lock yourself in your room and ask your roommates not to bother you, or get out of the house for a few hours. I ended up on a park bench for my last- and most productive- hour.

## Hit MVP before trying to get fancy

Everyone always says to hit MVP first before trying anything fancy, even if your MVP is the most obnoxious piece of code you've ever written. Now I know why I keep hearing this- it's the best piece of advice out there. Get **something** working and then revise if you have any time left. If not.. you won't have anything working to show for all of your hard work. To reiterate: **GET SOMETHING WORKING!**

I didn't take my own advice on this one, and I ended up wasting a lot of time trying to debug a function that just wasn't working. At my two hour check-in, I barely had any working code to show.

## If you don't have time..

Sometimes there just isn't enough time to refactor. I submitted the final version of this challenge about 5:30 hours in. It isn't fancy- actually, it barely hits MVP- but it works.

I had a lot going on- I had another in-person interview to prepare for, I had to continue working on another piece of code that my team needed to present the next day, and I was just plain exhausted from coding so much.

## Are you sure you want to submit?

The thing is- I probably could have created a more elegant solution if I had spent more time on it. That's the thing about coding: it's impossible not to improve. The more time you spend coding, the better you get, the smarter you become.

I did have the full 24 hours to finish the challenge, but I submitted at around the 6 hour mark. In hindsight, I should have slept on it for a few hours and woken up to work on it the next day with a fresh pair of eyes. I was afraid that taking all of the allotted time would reflect negatively on my abilities, but you know what- I think it's better to take more time to submit something you can be proud of than to submit the bare minimum and regret it all week.

## My solution

I'm not very proud of my code, nor am I happy with how far I got on this challenge, because I really did just barely get MVP. I don't expect this to land me the job I was going for. In fact, I will be suuuper surprised if I get any reply back from that HR guy, but that's part of the reason I'm posting this now.

## This is honestly the skill level I'm at right now

This is how I code. This is truly a reflection of where I'm at. Sometimes it takes me forever to get anywhere (like it did with this challenge). Sometimes it takes me minutes. That's how it is for us stone-cold beginners. But you know what... that's okay! I'm getting there, and you'll get there too. With each new challenge we take on and refuse to give up on, we get better and better. We shave minutes off of our time. We're able to think more logically and efficiently. And most of all, we can feel proud of ourselves because we really did try our hardest.. and we didn't give up!

So without further ado, here's my super basic (somewhat randomized) version of Connect 4.

``` javascript Basic Connect 4
/* A randomized Connect 4 Javascript Game that works with any board size */

'use strict';

var gameBoard = [];
var player1;
var player2;
var gameOver = 0;

const boardSize = 4;

function gameInit() {
  for (var i=0; i<boardSize; i++) {
    gameBoard[i] = [];
    for (var j=0; j<boardSize; j++) {
      gameBoard[i][j] = '*';
    }
  }
  console.log('Start Game');
  console.log(gameBoard);
  player1 = 1;
  player2 = 0;
}

function randomMove() {
  return Math.floor(Math.random() * (boardSize));
}

function piecePlacement(x, y, piece) {
  var placed = 0;

  while (!placed) {
    if (gameBoard[x][y] === '*') {
      gameBoard[x][y] = piece;
      placed = 1;
      return;
    }
    else {
      //iterate up through column
      for (var i=x-1; i>=0; i--) {
        if (gameBoard[i][y] === '*') {
          gameBoard[i][y] = piece;
          placed = 1;
          return;
        }
      }
    }
    var x = boardSize-1;
    var y = randomMove();
  }
}

function move(player) {
  var x = boardSize-1;
  var y = randomMove();
  var piece;

  if (player === 1) {
    console.log('Player 1 (Os) turn');
    piece = 'O';
  }
  else {
    console.log('Player 2 (Xs) turn');
    piece = 'X';
  }

  checkWin(player);
  piecePlacement(x, y, piece);
  console.log(gameBoard);
}

function winning(count) {
  if (count === boardSize) {
    return 1;
  }
  return 0;
}

function checkVertical(piece) {
  var count = 0;
  var j=0;

  while (j<boardSize) {
    for (var i=0; i<boardSize; i++) {
      if (gameBoard[i][j] === piece) {
        count += 1;
      }
    }
    if (winning(count)) {
      return 1;
    }
    j += 1;
    count = 0;
  }
}

function checkHorizontal(piece) {
  var i=0;
  var count=0;

  while (i<boardSize) {
    for (var j=0; j<boardSize; j++) {
      if (gameBoard[i][j] === piece) {
        count += 1;
      }
    }
    if (winning(count)) {
      return 1;
    }
    i += 1;
    count = 0;
  }
}

function checkDiagonals(piece) {
  var count = 0;

  for (var i=0; i<boardSize; i++) {
    for (var j=0; j<boardSize; j++) {
      if (i === j) {
        if (gameBoard[i][j] === piece) {
          count += 1;
        }
      }
    }
  }
  if (winning(count)) {
    return 1;
  }

  count = 0;
  i=0;
  j=boardSize-1;

  while (i<boardSize) {
    while (j>=0) {
      if (gameBoard[i][j] === piece) {
        count += 1;
      }
      j -= 1;
      i += 1;
    }
  }

  if (winning(count)) {
    return 1;
  }
}

function checkStalemate(piece) {
  var count = 0;

  for (var i=0; i<boardSize; i++) {
    for (var j=0; j<boardSize; j++) {
      if (gameBoard[i][j] != '*') {
        count +=1 ;
      }
    }
  }

  if (count >= boardSize*boardSize) {
    return 1;
  }
}

function checkWin(player) {
  var piece;

  if (player === 1) {
    piece = 'O';
  }
  else {
    piece = 'X';
    player = 2;
  }

  if ((checkVertical(piece)) || (checkHorizontal(piece)) || checkDiagonals(piece)) {
    console.log('Game over');
    console.log('Player '+ player + ' won!');
    gameOver = 1;
    return;
  }
  if (checkStalemate(piece)) {
    console.log('Game over');
    console.log('Stalemate!');
  }
}

function play() {
  gameInit();
  while (!gameOver) {
    move(player1);
    if (gameOver) {
      return;
    }
    move(player2);
  }
}

play();

```

If you have any questions, feel free to hit me up at mdeggies@gmail.com, or message me on twitter.

<a href="https://twitter.com/mdeggies" class="twitter-follow-button" data-show-count="false" data-size="large">Follow @mdeggies</a>
<script>!function(d,s,id){var js,fjs=d.getElementsByTagName(s)[0],p=/^http:/.test(d.location)?'http':'https';if(!d.getElementById(id)){js=d.createElement(s);js.id=id;js.src=p+'://platform.twitter.com/widgets.js';fjs.parentNode.insertBefore(js,fjs);}}(document, 'script', 'twitter-wjs');</script>
