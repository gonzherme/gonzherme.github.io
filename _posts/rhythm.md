---
title: "Rhythm"
#+author_profile: true
#+permalink: /rhythm/
---


# An Application to Match Your Running Pace with Music

Rhythm is a Python-based application designed to enhance a runner's treadmill experience by adapting music tempo to maintain a consistent running pace. Once on the treadmill, Rhythm helps you stay on track by synchronizing the beats per minute (BPM) of the songs in your playlist with your running pace.


# Features

-   **Set Your Running Goals**: once you are on a treadmill, the app allows you to define your target running distance and target time, and it will automatically adjust the bpm of the songs in your playlist to keep you running at the right pace.

-   **Adaptive Music**: Rhythm alters the beats per minute of the songs to match your steps per minute. This ensures that the music motivates you and maintains a rhythm that aligns with your current running speed.

-   **Graphical Interface**: the app features a graphical user interface (GUI) with visual elements such as animated GIFs and interactive buttons to simulate a moving environment while running. The 3D graphics add a fun, immersive experience, making it feel as if you are actually running through a virtual landscape.

-   **User Interaction**: The app provides an interactive interface through which users can edit their running goals. You can also track your progress with various counters, including pace, distance, and time.


# How It Works

The user inputs their target distance and target time for a run into the app, and Rhythm calculates the pace needed to complete the run. It then changes the bpm of every song on the playlist to match the cadence the user needs to run at to achieve the set goal.

-   **Real-Time Feedback**: The app provides feedback on whether you're on track to meet your goal. If you're falling behind, you'll hear motivational messages like "You're falling behind, try a bit harder!" and if you're keeping up, you'll hear messages like "Good work! Keep it going!"

-   **Song Alteration**: The app loads songs from the user's playlist and changes the tempo of the tracks to match the calculated steps per minute. The playlist consists of original songs and altered versions, where the songs are dynamically modified to match the required BPM.


# Technical Overview

Rhythm leverages several libraries and tools to achieve its goal of syncing music with running pace:

-   **Audio Management**: Rhythm uses librosa, an ML model that calculates the BPM of an audio file. It also uses pydub to handle the manipulation and playback of audio files. These libraries enable the app to load and alter songs according to the desired BPM.

-   **Tempo Detection**: The app uses a custom-built algorithm to estimate your tempo in real time based on the interval between each of your steps. This tempo is then used to adjust the music playback to match your rhythm.

-   **Graphical Interface**: the GUI is built from scratch using Tkinter and the CMU 15-112 Fundamentals of Programmimng graphics package to simulate a virtual outdoors running experience.

-   **Stride Length and Pace Calculation**: The app calculates your stride length based on your height and uses that data to determine your steps per minute. From there, it calculates your required pace to complete the set distance within the target time.


# Technical Challenges

-   **3D Graphical Simulation**: the project features a visually immersive simulation where an avatar runs down a long road, creating the experience of a runner. Surprisingly, the frontend emerged as the most challenging part of the project. The graphics were developed entirely from scratch using the CMU 15-112 Fundamentals of Programming graphics package, which provides basic functions for drawing geometric shapes (lines, circles, rectangles) by specifying coordinates of endpoints or corners.the project includes a feature that animates an avatar running down a long road, simulating the experience of a runner. Surprisingly, the frontend turned out to be the most challenging part of the project. The graphics were built entirely from scratch using the CMU 15-112 Fundamentals of Programming graphics package, which provides basic functions for drawing geometric shapes like lines, circles, and rectangles by specifying the coordinates of endpoints or corners.

To simulate depth and distance, the graphics utilize a [one-point perspective](https://www.studentartguide.com/articles/one-point-perspective-drawing#:~:text=One%20point%20perspective%20is%20a,look%20three%2Ddimensional%20and%20realistic.) technique. Objects are projected from an infinitely distant central point on the screen, expanding outward toward the viewer. While the rendered objects—such as an avatar, running track, trees, and buildings—appear simple, the geometrical complexity was significant. Each moving point and object required precise re-rendering and positioning using line equations and projections, demanding extensive calculations to ensure a smooth animation.

-   **Estimating running tempo**: to dynamically calculate the runner’s steps in beats per minute (BPM), the project employs a custom estimator algorithm. It records the timestamps of each step and uses the most recent six (or fewer) steps to compute the average time between consecutive steps. The tempo is then converted into BPM by dividing 60 by the average interval and returned as an integer. Initial values default to 0 BPM until enough steps are recorded. If a time gap between two consecutive steps exceeds two seconds, the system resets to maintain accurate calculations.

-   **Audio file types**: the project relies on the librosa library for audio processing, which only supports `.wav` files. This limitation required converting standard `.mp3` files to `.wav` format without compromising audio quality.

-   **Slow audio file processing**: if there is one thing I can take away from this project is that python is *slow* and quite terrible for audio file handling. Python's performance for audio handling was a significant bottleneck. The pydub library, used for changing the BPM of songs, exhibited slow processing speeds, especially with .mp3 files. As a result, all songs had to be pre-processed before use, rather than adjusting BPM dynamically during playback. This limitation will be addressed in the improvements section.

-   **Altered pitch**: pydub does not use any pitch preservation algorithms, since it simply speeds up or slows down the songs. This leads to higher pitch when speeding songs up, and lower pitch when slowing them down. This causes the altered songs to sound quite different from their original version. This issue will also be further discussed in the improvements section.


# Improvements and Future Work

There are many improvements to be made to the treadmill version of rhythm, for example:

-   **Cloud storage**: currently, all `.mp3` files are stored locally on the user’s test device. Transitioning to cloud storage would allow users to dynamically download songs from a centralized database as they listen. Key considerations for this feature include:
    -   <span class="underline">Batch Loading</span>: preloading songs in batches of five ensures smooth playback. If a user skips a song, the next one is
        already queued and ready.
    -   <span class="underline">Streaming Logic</span>: implementing a streaming mechanism to load songs in 10-second snippets enables immediate
        playback without requiring the entire song to be downloaded upfront.

-   **Unaltered pitch**: to address pitch distortion, the app could implement Time-Scale Modification (TSM) algorithms. TSM preserves pitch while speeding up or slowing down songs and is far more efficient than pydub, enabling real-time BPM adjustments.

-   **Mobile transition**: the current beta version runs exclusively on laptops. Rewriting the app in Swift and deploying it to the Apple App Store would make it accessible on mobile devices, significantly broadening its reach.

**Expanding beyond treadmills**
Future iterations of the app could support outdoor running by dynamically detecting the runner's cadence and matching it to the music’s BPM in real time. This requires:

-   **Phone accelerometer**: the app would use accelerometer data to calculate the user’s cadence, continuously adjusting the BPM of the music to match their steps.

-   **Dynamic bpm changes**: replacing pre-processed BPM adjustments with real-time modifications. This would require efficient algorithms, such as TSM, for seamless playback. (pydub is too slow)

-   **GPS tracking**: integrating GPS would allow the app to monitor the runner’s speed and ensure they stay on pace to meet their goals.

