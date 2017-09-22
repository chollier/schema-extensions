# GraphQL Extensions

This project contains a repository of suggested or draft extensions or changes (as minimal as possible for the latter) to your GraphQL Schema.
Using [GraphQL Faker](https://github.com/APIs-guru/graphql-faker) you will be able to proxy your existing schema but also to mock and simulate the proposed changes

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Set up Instructions](#set-up-instructions)
- [GraphQL First development process](#graphql-first-development-process)
  - [I'm an engineer scoping or designing a new feature](#im-an-engineer-scoping-or-designing-a-new-feature)
  - [I'm a back-end engineer and I worked on some of the proposed changes, they just made it to master.](#im-a-back-end-engineer-and-i-worked-on-some-of-the-proposed-changes-they-just-made-it-to-master)
  - [I'm a front-end engineer and I want to use one of the extensions here](#im-a-front-end-engineer-and-i-want-to-use-one-of-the-extensions-here)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Set up Instructions

1. Setting up the project:

First, run npm to initialize the project dependencies
```shell
npm install
```

2. If you schema endpoint requires authentication, insert here instructions to fill in the Header with an auth token or another kind of authentication. Example:

Log in to http://mycompany.com, then run this in the javascript console (Shift-Cmd-J):
```javascript
JSON.parse(localStorage.getItem("session")).accessToken
```
This will return a string that you need to copy and paste in the next command

3. Running an extension file:
```shell
npm start -- --open --extend [your GraphQL endpoint] --header "Authorization:Bearer [THE AUTH TOKEN YOU GOT]" ./example.faker.graphql
```

## GraphQL First development process

We have found that using GraphQL First brings us efficiency and gains in productivity.
Here are a few guidelines to make this happen:

### I'm an engineer scoping or designing a new feature

Since the schema will be used by the front-end team and implemented by the back-end team, it's recommended to pair with a peer when possible. Brainstorming a new schema extension in `graphql-faker` is very easy:
1. first create a new file in this repo, e.g.: `user-avatar.faker.graphql`
2. follow the [Set up Instructions](#set-up-instructions) to start the project with this file:
```
yarn start --open --extend http://localhost:3000/graphql/queries --header "authorization:Bearer [THE AUTH TOKEN YOU GOT]" ./user-avatar.faker.graphql
```
3. Write your extensions:
![screenshot 2017-09-22 10 47 43](https://user-images.githubusercontent.com/1869/30758337-d4e47972-9f86-11e7-98f4-46616380141e.png)
4. Visualize your changes in GraphiQL
<img width="350" alt="screenshot 2017-09-22 10 48 08" src="https://user-images.githubusercontent.com/1869/30758349-e4f232aa-9f86-11e7-9b9e-f264140864f9.png">
5. Try you Query:

![screenshot 2017-09-22 10 50 19](https://user-images.githubusercontent.com/1869/30758399-174b6b4a-9f87-11e7-94bb-23555cb78b4f.png)

6. Open a pull-request and ask for review.
7. Get feedback, when there's a consensus, merge your PR.

### I'm a back-end engineer and I worked on some of the proposed changes, they just made it to master.

Great! Thanks for that :champagne:.

If you only incrementally added some types from an extension suggestion, there's one last thing you should do. Since `graphql-faker` can only extend and not _override_ types, you need to remove from this file the types you just implemented, otherwise it will complain that the type already exists.
Finally let the people who will use API or notify the #graphql channel of the recent release.

### I'm a front-end engineer and I want to use one of the extensions here

Great news, you can start before the back-end is even implemented. You are only a few steps before productivity:
1. clone this repository
2. follow the [Set up Instructions](#set-up-instructions) to start the project with the extension you wish to use:
```
yarn start --open --extend http://localhost:3000/graphql/queries --header "authorization:Bearer [THE AUTH TOKEN YOU GOT]" ./user-avatar.faker.graphql
```
3. explore the schema and get familiar with the extensions
4. eventually you might want to improve some of them to bring realistic mocks or hardcode examples:

```patch
type Avatar {
  # The original avatar URL
- originalUrl: String
+ originalUrl: String @fake(type:avatarUrl, options: { imageCategory: people })
  # The thumbnail resized to 64x64px
- thumbnail64Url: String
+ thumbnail64Url: String @examples(values: ["http://example.com/image.jpg", "http://example.com/image2.jpg"])
}
```
5. open a pull-request with these improvments, they might be useful to others!
