---
layout: post
title: "My future prediction in 2009"
description: "The prediction for future technology in 2009"
categories: [blog]
tags: [UI,mobile-phone,report,technology]
---

## Lots of my prediction for future came true.

Back in 2009 when I took the UI class at Tokodai, I made a report to predict the future of UI. I just unintentionally found the report today, and decide to publish it. Remember, this report is written in 2009.

## Japan's feature phone

Nowadays mobile phone has become a part of the life of many people. Japan is in the vanguard of combining the mobile phone with other goods such as watch, music player, TV, radio, calculator. Moreover, the phone becomes very friendly with the man. It is easy to use and very comfortable, although there are still some features needs to improve.

### Text input layout

Firstly, typing English the text input system is most troublesome, because it is designed for typing Japanese. It can remember from short Japanese word to simple sentence, and more than that, the flexibility to guess what next the word is, base on the typed history of the owner. However, using this kind of English inputting system causes so much troublesome. We must be tired of pressing so much button for a simple sentence, for example, to type "where do you go?” each letter need press times as follow.

    W: 1 time, h: 2 times, e: 2 times, r: 3 times, d: 1 times, o: 3 times, y: 3 times, u: 2 times, g: 1 times, ?: 4 times, space: 1 times.

To input "where do you go?” we need to press keyboard for 33 times. According to usability system from Nielsen, lacking learn-ability, efficiency, error correctability, flexibility, and satisfaction making this input system likely unacceptable compared with Japanese input system, which has all usability listed. In fact, Japanese inputting system is harder to improve, because it does not has any special character to distinguish between words, which is similar to "space" in English. Despite those difficulties, Japanese inputting system is far better than English inputting system.

### T9 System

To improve this input system, firstly we have to improve efficiency because 33 times of pressing the button for "where do you go?" is unacceptable. We can improve efficiency a lot just by merging with T9 input system. T9 system is an English inputting system with the basic idea of typing one button per letter. For example, to type "where", instead of pressing 10 times these button 9(w),4,4(h),3,3(e),7,7,7(r),3,3(e); we just input 9,4,3,7,3 button. T9 system searches for all the words that made by this arrangement. In this case, there are two words: "where" and "weird," but "where" appears more frequently than "weird", so "where" is chosen. With the T9 system, writing down a sentence can be done by pressing times of the number of characters in that sentence, for instance, "where do you go?" generally needs 16 times. Having T9 system merged into Japanese mobile phone almost double efficiency because we just have press down the number of character. Moreover, because T9 system chooses only words that appear in the dictionary, we do not have to think about correct error system anymore.

To improve flexibility and learn-ability, we can remember the sentence that user wrote. Every time user writes a word, history can be recalled to finish the sentence without entirely writing it. For example, by remembering "where do you go?", If user inputs "where", the system can make a guess "where do you go?" and offer a sentence just by a word "where". This is entirely done in Japanese inputting system.

### Keyboard layout of feature phone

The second is the keyboard layout. Ordinarily, mobile phone in Japan has two buttons for calling: one button for making a call, picking up the phone, which symbolized by hanging on the phone, and one for stop a call which symbolized by hanging off the phone. These two buttons are somewhat similar, and usually, confuse me which one I should press if I want to pick up or stop a call. In general, these two buttons fulfill 3 functions: make a call when the phone is idle (not calling); pick up a call if there is an incoming call; hang off the phone while calling. Typically, I rarely deny an incoming call, and even in such case, I usually use the silent button on the side of the phone, not hanging off button.

Because we can not make a call, or pick a call while calling, so these 3 functions are independent of each other respectively. So why don't we merge two buttons in one? One button for making a call, picking up a call, and stopping a call help avoiding user's confusing, as well as reduce user's failures.

### Prediction for mobile phone and the future UI

The third is about mobile phone functionality design, a bit outside of interface. Every day, I have to bring a mobile phone, a key holder with several keys, a wallet with many cards, an iPod while going out, and put everything in the pocket. As a result, I usually confuse to pick a speculated one from a bunch of things in the pocket. Why can we design a phone interact with an object like a phone to open a door, a phone to identify or phone to purchase goods?

For the real-life example, we merge a phone with the navigator, creating navigation applications; we merge mobile phone with the prepaid card, create electric SUICA... We also can merge a phone with the key, create a new application that let user using a phone to lock/unlock an electric door, or merge mobile phone with ID cards. If these applications succeed, it is much more convenient for us.

## Problem in UI with computer

Not only the mobile phone, but the computer has also become cheaper and cheaper to reach. Besides, the computer is faster and faster each year; however, the input devices of Keyboard and mouse, the output devices of Monitor, printer, projector still stay unchanged.

My biggest problem with the computer is Vietnamese input system. The main characteristic of Vietnamese is, there are more than 100 combinations of vowels and intonation. For example, from the origin vowel “o”, Vietnamese has two alternative vowels: “ô” and “ơ”, and each is combined with six intonations create a different meaning. For example, letter “o” combine with six intonations express as: “o”, “ò”, “ó”, “ỏ”, “õ”, “ọ”. As a result, design a keyboard for Vietnamese is nearly impossible, and we prefer inputting software that converts the unique combination of some characters into a Vietnamese character. Before 1998, there are many designs for such a combination like that. Two mainly designs which are mostly used, are VNI and VIQR.

### VIQR vs VNI vs Telex

VIQR input system uses the particular provided characters on English keyboard to input Vietnamese. For example, “o^” becomes “ô”, “o”” becomes “ơ”, “o\`” become “ò”, “o’” becomes “ó”, “o?” becomes “ỏ”, “o~” becomes “õ”, “o.” becomes “ọ”.

VNI input system use vowel and number combination to express alternative vowel and its intonation. For example, “o10” becomes “ò” (no alternative with intonation 1), “o22” becomes “ố” (alternative 2 with intonation 2).

I did two tests to measure how efficient each input system is. The measuring unit of the first test is the distance finger has to move to type a message. Firstly, I defined a distance for pressing each key on the keyboard. For example, keys with zero distance are: “a, w, e, f, space, +, o, I, j”; keys with 1 distance are: “left shift, q, z, s, d, c, r, p, l, k, m, u, h, n”… Each input system is done with 10 tests (assuming no input error), to measure average distance finger has to move per letter. The result is expected. VIQR has average distance around 4.3 while VNI has average distance around 3.1. This is because all combinations from VIQR input system have many special characters that require pressing “shift” to reach, while VNI does not need it.

The second test is how many errors occur if a person types text in VIQR and VNI. The result depends on each person typing still, but for any person, typing Vietnamese using VIQR has much error than in VNI.

In 1992, a new design for inputting Vietnamese was born and was blooming in 1998. It is called TELEX. This inputting system uses characters that never stand after a vowel in Vietnamese to encode a Vietnamese variation of vowel character. For example: “oo” becomes “ô”, “ow” become “ơ”, “ space, f, r, s,  x, j” for intonation. I also did a test on this typing system, and the result is more than expected, the average distance is around 2.3, and there is not so many errors while typing in Telex.

### Eye tracking

Back to the problem while using the computer, the second problem is my eyes often got hurt when using a large monitor. Human eyes can only focus at one point, but because there are many points with the same illumination on the monitor, the eyes must strain to cover all the point like a habit. Because of this action, the eyes have quickly become tired. Maybe in the future, there will be eyes detecting and tracking system, which detect the position that the eyes focus to and reduce illumination of surrounding object. A more straightforward example is when the user types a message; it is naturally that user’s eyes will focus on the message, so we can reduce illumination of surrounding to make it easy for eyes.

Another problem when using the computer is the checkbox. When surfing the internet, there must be some checkboxes (or radio button) that allow people have more options about an object. However, checking these checkboxes are very painful. Because the area to click is tiny, according to Fitts’ law, it costs much time needed for checking these boxes. It is much better if there exists a tool that does the following works: Jump to each checkbox by pressing a key, highlight the content, automatically check that box if a particular key is pressed. I like to code this tools someday.

In conclusion, mobile phone and computer are improved a lot since its appearance. Also, the interaction between human and them is also changed a lot, especially on the mobile phone. Understand about human interface fundamental give me the knowledge to understand how and why they are changed.

## That is it

Do you have any prediction in the past, let's share with me.
