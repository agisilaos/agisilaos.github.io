---
layout: post
title: WWDC Scholarship Application - A Process in Review
date: 2018-04-27
categories: writing
---

For those of you that have followed along with my journey, you know this was my third time entering to win a scholarship and attend WWDC. I did a lot of things differently over the course of the last two years, from research and, writing to designing a playground book. After researching everything around a playground book including what it makes it interactive and interesting I designed the book using sketch and build it using (you guessed it!) Xcode Playgrounds.

## Research

There were so many things (e.g interactive messages, notes, best practices) Apple provides in the documentation and WWDC videos, and I wanted to have a good grasp of them before moving forward with an idea.

| ![passion](/images/passion.png){:class="img-responsive"} |
|:--:|
| *Presentation slide from Apple's keynote* |

One of the slides that made me think deeply and realize what I wanted to build and why is the one above. Neural Networks was one of my favorite subjects in University and when I got started with it I was having a hard time understanding the basics; which is the sole reason I decided to build a book about the Basics of Neural Networks.

## Design of the book

When it comes down to designing a book, it’s not only about the visuals. Playground books consist of two things: The left  side contains all of the text and the right side which is the Live View is where all of your visuals to live there. The hardest part for me was how to write the book. It was a first for me, and I wanted it to be accessible and understandable for everyone.

I spent most of my design time focusing on that because I had a pretty good sense of how the visuals should look like. Since the review time for our playgrounds was 3 minutes I decided to build 2 chapters plus an overview page  guranteeing it was  short and sweet.

I spent one night designing it and after being happy with the turnout, I moved to the development phase.

## Development

Let me start by saying, you have to use Airdrop to send your project back and forth to your iPad because you can’t test your Playground Book with a Mac. Because of that, the development phase consumed a lot more of my time than I anticipated. I spent in total 2:30 hours solely doing so 🙃

My next obstacle was the debugging of the book. If you ask anyone developing a playground or a playground book  I guarantee they’ll call it the same thing. I saved a little time and a lot of my sanity by creating an Xcode project first, developed a chapter there and then move that over to the Playground book. This process saved me a lot of time. It isn’t perfect but I’m sure the team behind Playgrounds is working on a solution.

The next thing I had to tackle was one of my own “demons”. I’m very particular about a number of things while working, so I wanted all of my code to be clean, have extensions and all of that shiny stuff. Long story short, I couldn’t do that, so my code ended up looking like a hot mess.  (It was working perfectly fine so I dealt.)

Throughout all the years I’m doing iOS development, I’ve become most familiar with Interface Builder. In this particular case, I had to set constraints in code because I couldn’t use the IB. It was a great learning process since I haven’t used this method a lot before and it was genuinely fun. I learned a lot of things and applied all the tips Alex Akers(@a2) shared with me last summer during my time at Microsoft.

My last concern was that I didn’t want to use a lot of resources like assets from design etc because I wasn’t sure how they would look on split screen versus full screen. So I decided to write the UI in code. That was arguably the most difficult task I had to do and it was what consumed most of my development time.

Alas, I finished with the development 3 hours before submissions were due! Hello anxiety, my old friend...

## Essays

Part of the scholarship application was to write a couple of essays. In the first one, I had to describe our Playground (what technologies we used, how we solved the problems we had using Apple’s technologies). The second essay wasn’t technical. It was inspirational. I had to write about how we share our excitement and knowledge about programming with the community.

With the main project being done and ready for submission, I was less anxious and focused on finishing the essays. In less than 1:30 hours and given it always takes a lot of time for me to write thoughtful and well-organized essays, I was super happy with how they turned out.

## What I learned along the way

1. Time Management

    Time management is super important in everything we do, especially when it comes to working on any Scholarship submission. Since my full time focus is on Iris Health, I was working on this in my spare time, and I had to make sure I designed  my time in a way that ensured I had work, scholarship and personal time  and not waste any second of it.

2. Think of your playground as an MVP

    My second realization was that I need to think of my playground as an MVP (Minimum Viable Product). You don’t have the time to make your submission perfect but you have the time to pay attention to details and that’s one of the reasons that may your submission stand out.

3. Make something original and that you’re passionate

    One of the slides that really stood out to me from the WWDC presentation was the one about passion. By creating something you’re passionate and really care about, you will feel good, motivated and have more fun while doing it. So when it comes to creating a side project and/or a WWDC Scholarship Application think about what **you** really want to create and do that. People can sense passion and drive.

4. Have fun

    Last but not least on my list, have fun! I can only imagine how cool and what an honor it is  to get a scholarship and believe me I would have loved to, but don’t do things for the end goal, do them for the ride. In every one of my submissions the past 3 years I learned a ton of new things which I can apply to my projects. It’s an achievement on its own to go from an idea to a product in a week, so be proud of that. It’s not easy.

![submission-status](/images/Submission-Status.png)

Congrats to everyone who won a scholarship!. Have any questions about my experience or want to share how you approached your process? I’d love to hear it. Let’s talk shop on twitter or via email.
