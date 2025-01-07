---
title: "Projects"
author_profile: true
permalink: /projects/
sitemap: true
---

## Sentiment Analysis Optimization
- Developed [Sentiment Analysis models](https://github.com/gonzherme/sentiment-analysis) using Logistic Regression and k-NN, trained on the [IMDB Movie Review Dataset](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews)
- Preprocessed data with Bag of Words (BOW) and TF-IDF, optimizing for accuracy and computational efficiency
- Analyzed the impact of word embedding dimensionality on model performance, balancing reduced computation cost and accuracy

<video width="560" height="315" controls>
  <source src="../images/sentiment-video.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>

## PlanIt
### HackCMU 2023 Award Winning Project ($1200 prize)
- Developed an ML-powered software, takes input lecture notes or lecture video url, generates a customized study plan for the user
- Built web application using Django. Frontend with JavaScript, HTML, CSS, and Backend with Python querying to OpenAI API
- Integrated a YouTubeTranscript API to extract and synchronize video transcripts to convert into lecture notes


## Rhythm
### Music Pace Adjustment Tool for Runners
- Deployed [Python software tool](https://github.com/gonzoherme/Rhythm) that helps runners keep a desired pace through the music they listen to
- Tool changes the beats per minute of songs to match the steps per minute of the runner
- Implemented manipulation of mp3 audio files with ML beat detection libraries: pydub, scipy, and librosa
