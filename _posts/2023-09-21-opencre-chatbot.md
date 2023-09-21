---
layout: post
title: "Exploring OWASP's New Security Chatbot: A Tester's Perspective"
---

Cybersecurity is a vital aspect of software development, but it can also be a daunting and complex one. How do you keep up with the ever-changing cybersecurity landscape? What if you could have a chat with a cyber expert who knows everything about security standards and tools?

## TLDR

In this post, we delve into the world of the OpenCRE Chatbot, your trusty companion in the realm of cybersecurity standards, tailored for software testing. OpenCRE streamlines security requirements, and the Chatbot simplifies information retrieval while citing reputable sources. Discover the combined power of ChatGPT and the OpenCRE Chatbot, each serving distinct purposes in your cybersecurity journey.

## Introduction

LLM's continue to be the hot topic of the time, with arguments flying around about how they will change the world and how they are useless and may as well be thrown in the bin. Underlying this hyperbole is a subset of people who have a good use for them and are aware of their limitations and what they are useful for.

A group that did this was the contributors at OWASP's Open Common Requirement Enumeration (OpenCRE), and thus the OpenCRE Chatbot was born. This post will look at the OpenCRE chatbot from the perspective of a software tester and talk about how we can utilise it to help us improve security within the Software Development Lifecycle (SDLC).

## OpenCRE, what is it?

OpenCRE is a way of parsing and understanding lots of different security standards. Security is a complicated topic and often one with lots of loud opinions; this is where security standards bodies come in. In an ideal world, using a lot of expert opinions and research, they help users have a set of guidelines to help secure any software they are building. However, as can often happen with standards, we don't just have one.

![XKCD comic showing how standards proliferate when people think we should have one more true global standard](../images/posts/XKCD%20Standards.png)
*XKCD comic 927 (https://xkcd.com/927/)*

This leads to this valuable information spread all over the web in different places.

OpenCRE aims to fix this by bringing the information together in "Common Requirements". This is a way of looking through all the information from multiple reputable sources and displaying it in a nested format. The CRE's contain other CRE's and also the sources these requirements are linked to, e.g., OWASP, NIST, etc.

## An Example

To show how OpenCRE can be used. Here is a scenario:

> You are involved in the development of of new functionality for an application. You are concerned that the new functionality could create an opening for a cross-site scripting (XSS) attack. You want to use the collective knowledge of all security standards bodies online, but I don't know where to start.

In this situation, I can navigate to https://opencre.org and use the search bar to search for "XSS".

![OpenCRE with a search of "XSS"](../images/posts/OpenCRE%20XSS%20Search.png)

[On the left](https://www.opencre.org/search/xss) we can see some CRE's. These are common requirements that multiple standards agree with. e.g., many standards bodies have agreed that you should "Escape output against XSS". If I click on that CRE, I get these [results](https://www.opencre.org/cre/366-835).

![OpenCRE 366-835 around XSS](../images/posts/OpenCRE%20366-835.png)

Here, you can see all the standards and tools that help form this CRE. You can see input from [OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/index.html), from [OWASP Application Security Verification Standard (ASVS)](https://github.com/OWASP/ASVS), from [MITRE's Common Weakness Enumeration (CWE)](https://cwe.mitre.org/data/definitions/79.html) and some [OWASP ZAP Scanning Rules](https://github.com/zaproxy). This allows you to study this collective knowledge and think about how it can apply to your new functionality.

## How does the chatbot fit in?

So you have seen how OpenCRE works on its surface; how does the newly added chatbot fit into this?

The chatbot is built on PaLM, a large language model (LLM) from Google. It has the general knowledge from PaLM but has been specifically trained on all the information in OpenCRE and the links it has to the standards and tools. Think of it like ChatGPT, but with a speciality in cyber security standards and the ability to clearly cite its sources.

![OpenCRE Chatbot Homepage](../images/posts/OpenCRE%20Chatbot%20Homepage.png)

In my experience, the chatbot is a simple way to parse the mountains of information encapsulated within OpenCRE. It felt much more intuitive when you didn't know exactly what you were looking for. It allows you to explain your problem in plain English, and the chatbot will try to understand the question.

For example, if I were discussing with the development team a feature that would take user input and display it on the screen but I didn't know the term "XSS" like in the scenario above, I could use the below prompt to understand what I should be looking out for.

![OpenCRE Chatbot with a question about what concerns to have if a new feature in an app allows a user to input a value and that gets displayed on the screen](../images/posts/OpenCRE%20Chatbot%20insert%20question.png)

This not only gives valuable information, but it also links to the references where it was obtained. In conversations with developers and PMs, this can be invaluable, as a suggestion backed by the reputation of OWASP will often have a lot more weight than without.

Another example of how the chatbot can excel over the usual OpenCRE nested browsing is the ability to ask it very specific questions that would potentially take a lot of reading and parsing of information to understand. Below, I ask a question I have often gone back and forth on with developers.

![OpenCRE Chatbot with a question posed about whether you should use field validation in the backend as well as the frontend](../images/posts/OpenCRE%20Chatbot%20dev%20question.png)

OpenCRE chat clearly answers the question with a "No" and then proceeds to explain why and again cite its sources so they can be shared with the team.

## OpenCRE Chatbot vs. ChatGPT

So how does OpenCRE stack up against the 800-pound gorilla in the LLM space, ChatGPT (3.5)?

Asking the same questions as above definitely gives different results.

When asking the first question, I got a very long response. So long, I haven't managed to show it in a screenshot. It's response seems accurate and, in many ways, more helpful on its surface. It certainly breaks the issue down into more understandable and consumable chunks.

![ChatGPT with a question about what concerns to have if a new feature in an app allows a user to input a value and that gets displayed on the screen](../images/posts/ChatGPT%20insert%20question.png)

Next, we see the question about field validation in APIs. We can see it is not quite as forceful with its answer, but again, it goes into further detail about the issues that would arise with no API validation.

![ChatGPT with a question posed about whether you should use field validation in the backend as well as the frontend](../images/posts/ChatGPT%20dev%20question.png)

I believe both of these response styles are useful in different ways; let's go through the benefits of each.

### Open CRE Chatbot

Due to its tendency to give a little information and then defer to its sources for more, OpenCRE Chatbot:

- Allows the source document to be updated and be a constant source of truth.
- Allows a user to verify the information and ensure they trust that source.
- Gives the user the backing and reputation of standards bodies when creating an argument around the information.

### ChatGPT

Due to its outgoing, appeasing, and simplifying nature, ChatGPT:

- Provides more information in the response
- Tries to break complex information into more consumable chunks

## Conclusion

I will continue using both the OpenCRE chatbot and ChatGPT for distinct reasons.

If I am generally trying to learn and understand a subject without critical application, I will continue to use ChatGPT. The ability to question and receive simple, broken-down answers is absolutely invaluable.

If I am in a situation where it is critical to get a subject correct and need the backing of standards bodies to get my point across to the team, I will use the OpenCRE chatbot.

## A tester's perspective

From the perspective of the day-to-day work of a software tester, I can think of many examples of how both chatbots can be utilised.

While writing bug reports, a tester could use the OpenCRE chatbot to obtain standards documents to attach. This allows the person working on the ticket to have a source of truth for the issue. On the flip side a tester may use ChatGPT to try to break down the security issue in simple terms and add this to the description of the ticket so the reader can understand the issue before looking at the more complex document.

In sprint planning or an architecture session, a tester could use OpenCRE to query as they go. They can use it to add standards to stories so the team can understand them before starting work. This is a case where a tester may not want to use ChatGPT, as it may just feed the noise of opinions that is often present in planning sessions.

Finally, a tester could use both ChatGPT and the OpenCRE Chatbot to help run exploratory security testing. In down time, they could use development environments and the knowledge provided to run mini penetration tests. The two tools could be really useful in organising thoughts and gaining knowledge as they test.

These are just a few examples in which a tester could utilise this novel technology to improve the AppSec posture at their work. I'm sure there are many more.

But don't just take my word for it; go ahead and give it a try. Let me know your thoughts on the points discussed above!

[OpenCRE Chatbot](https://opencre.org/chatbot)
