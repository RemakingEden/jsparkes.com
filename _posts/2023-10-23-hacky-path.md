---
layout: post
title: "Testing the "Hacky Path"
---

![A person walking across a path made of the green text from The Matrix into a greener brighter world | Bing Image Creator](../images/hacky-path.jpg)

Have you ever wondered how hackers find and exploit vulnerabilities in your application? How can you go beyond the conventional happy path and unhappy path testing to uncover hidden flaws in your application?

## TLDR

In this blog post, I share with you the concept of “hacky path” testing, which is a way of testing an application as if it were under attack by a malicious user. I explain how this approach differs from conventional happy path and unhappy path testing and why it is important for both functional and non-functional aspects of software quality. I also provide some examples of hacky path testing scenarios for a simple API contract and discuss the benefits of incorporating this technique into the software development lifecycle.

## Thank you's

Before starting this post, I need to thank [Isabelle Mauny](https://www.linkedin.com/in/isamauny/?originalSubdomain=es) and [Tanya from the WeHackPurple podcast](https://wehackpurple.com/podcasts/) for introducing me to the concept of the "Hacky Path". They briefly touched upon it in [episode 79](https://wehackpurple.com/podcast/episode-79-with-isabelle-mauny/), and I was immediately drawn to the term. However, I should note that my interpretation of it may differ from how either of them uses the term.

## What is the "Hacky Path"?

So, we all know the happy path, right? It's the tests the developers will think of without any prodding. It's the first tests that often comes to your head. How will the ideal user, ideally use our app? Achieving this level of quality in software can be relatively straightforward; then you give it to users, and all hell breaks loose. They do something you never predicted, and now your app is on fire and everyone is screaming. We need to go further.

What about the unhappy path? This is the path less trodden, the tests that assume something has gone wrong. What happens if, for instance, the required data isn't filled out in a form? What if you happen to refresh the page during a crucial moment of loading? Or, imagine you click a button repeatedly before it's had a chance to disable. These tests are designed to uncover the less frequent but still critical situations that users might encounter. We may not expect the user to be able to continue if they hit one of these unhappy paths, but the application should still handle the path gracefully. Ideally, the application should notify the user and offer assistance, ensuring that nothing catastrophic, like a server crash, occurs.

Throughout my seven years of testing experience, I've been a strong advocate for both happy path and unhappy path testing. These approaches have effectively addressed most of my testing needs. However, I've always had a hunch that there's another layer of testing waiting to be explored, a kind of testing that often prompts people to ask, 'Why on earth would anyone do that?' This kind of testing only gets more obvious as you shift left and test at a component level with small changes. The familiar happy path and unhappy path are still crucial, but it gets more and more tempting to try things out that no user would ever do. No regular user at least...

![A devil sat at a laptop in the stereotypical hacker hoodie with the text "I'm no regular user" at the bottom | Bing Image Creator | ImgFlip](../images/im-no-regular-user.jpg)

Introducing Hacky Path Testing. This approach delves into all those quirky, unconventional test scenarios that crossed your mind during those intense API contract discussions with your team. It's about letting your creativity run wild, considering all the nuanced ways in which data and code can be manipulated. These are the test cases that you may have hesitated to bring up, fearing your team might dismiss them as frivolous. However, they serve a unique purpose. These tests aren't designed for the average user; they're designed to challenge your application as if it were under attack by a malicious user.

## An example

Let's discuss a concrete example. you have an API contract like below:

``` markdown

**Endpoint:** `/api/address` **Method:** POST

**Request:**

- **Request Body:** JSON

**Request Body Example:**

json

`{   "street_address": "123 Main Street",   "city": "Example City",   "state": "ES",   "postal_code": "12345",   "country": "Example Country" }`

**Response:**

- **Success Response (201 Created):**
    
    - **Response Body Example:**

json

`{   "id": 1,   "street_address": "123 Main Street",   "city": "Example City",   "state": "ES",   "postal_code": "12345",   "country": "Example Country" }`

- **Error Response (400 Bad Request):**
    
    - **Response Body Example:**

json

`{   "error": "Invalid request data" }`

- **Error Response (500 Internal Server Error):**
    
    - **Response Body Example:**

json

`{   "error": "An internal server error occurred" }`
```

As we can see, it is a generic POST request to add an address to an application.

You consider the happy path:
- Can you add an address from the main area the app operates in?
- Can you add an address from another, less regularly used area the app operates in?
- Can you add an address that only has the required fields filled?
etc.

You consider the unhappy path:
- Does the call fail gracefully when some required fields are not entered?
- Does the call fail gracefully when none of the fields are filled?
etc.

Finally consider the hacky path:
- What happens if you send no data at all?
- What happens if you send a data type that the application is not expecting?
- What happens if you send SQL commands instead of strings?
- What happens if you send something other than JSON in the request body?
etc.

As you can see, these unconventional test scenarios push the boundaries of what regular users would attempt. However, they are crucial not only from a functional but, most importantly, a non-functional perspective.

Functionally, the application may not need to excel in handling these 'hacky calls.' In most cases, it simply needs to stay afloat, continuing to function for the majority of users. The key is ensuring that even in the face of such unexpected inputs, the application gracefully carries on its core functions.

In the realm of non-functional testing, the landscape becomes notably intricate. Malicious users are a different breed; they don't concern themselves with how a regular user interacts with your system. They want to explore it all and test every nook and cranny to see what could go wrong. That 'hacky path' you just stumbled upon that slightly stresses your system—what if a malicious user discovers it and decides to deploy a simple script to barrage it repeatedly? You might suddenly find yourself facing a Denial of Service (DOS) attack.

Consider another scenario: sending a different data type in the request body triggers an unhandled internal server error. From a functional standpoint, your application might appear unscathed, but this mischievous tester might now have uncovered a fingerprint of your tech stack and its versions. Armed with tools like [Metasploit](https://www.metasploit.com/), they could potentially exploit any vulnerabilities and gain root access to your system.

## Why is this important?

Above is a simple example to hopefully highlight the benefits of "hacky path" testing. The more you bring this into your software development lifecycle, the more you will understand and be able to demonstrate its value. You may even find it addictive; it is a great way to understand the core technology behind the applications we test every day. It allows you to be creative and think of all the ways the technology can be used.

There are so many benefits for your application and company. The team will understand the technology better, and the developers will begin to learn all the common ways an application can be misused and fix these without them getting to you. Functionally, the app should be pretty watertight if you have tested it to this extent. Finally, the security of your app should be significantly improved!

As always, though, don't take my word for it. Go and try it out. It's going to be weird at first for you and the team, but you will see results. If you need any help, feel free to reach out. Until then, start walking that "hacky path"!