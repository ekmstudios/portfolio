---
title: Databases for Mobile Apps
description: This article provides an overview of various database options to consider when needing a database for your mobile app. 
---

# Database for Mobile Apps

## Overview

I've primarly worked with iOS and developed and published a few apps on my own, but have never really needed much of a database on the backend. I did create one app that tracked high scores in a simple MYSQL table and used PHP to connect the app to the database. But I'd become increasingly interested in developng an app with authentication, multi-player, and real-time scoring capabilities. 

Here are the three options I'll explore here in this article:

- [Google's Firebase](#firebase)
- [Custom solution using PHP and MYSQL](#custom-solution-using-php-and-mysql)
- [Apple's Cloudkit](#cloudkit)

## Firebase

### High level steps
- Set up project in Firebase console and add Firebase SDK to your iOS app.
- Authentication: Enable providers (email/password, Apple, Google, etc.) via Firebase Authentication.
- Real-time database: Use Firestore or Realtime Database to store and sync player scores, game states, and events instantly.
- Game logic: Implement rules either client-side or with Firebase Cloud Functions (serverless backend logic).
- Analytics/Crashlytics: Add monitoring and analytics for player engagement.

### Pros
- Fast to set up, scalable, excellent for real-time sync.
- Handles authentication, data storage, and serverless logic out of the box.
- Cross-platform support (if you later expand beyond iOS).

### Cons
- Vendor lock-in.
- Advanced queries or heavy data usage can get expensive.


## Conclusion


Keeping in mind that I've primarily focused on iOS but may want to create an Android version sometime in the futu
