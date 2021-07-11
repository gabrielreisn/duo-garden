---
permalink: posts/{{ title | slug }}/index.html
title: Things i have learned while working with a video-player library
date: 2021-07-11T03:00:00Z
tags: []
description: ''

---
From the previous month, I have been working with video players for enhancing first-time user experience, and that has been simply amazing for discovering new UX approaches, especially on a timeframe where video content got so much attention with platforms like TikTok and now Instagram changing the product focus to a more video-based thing.

For this article sake, I've been using [https://plyr.io/](https://plyr.io/ "https://plyr.io/") for development, which supports self-hosted HTML5 videos, youtube and Vimeo

From a UX perspective, I've seen a few "autoplay with mute" patterns for making the video more attractive for the final user without frustrating the experience/user focus. Twitter has been doing that for timeline videos and now Facebook is doing the same for stories. In my case since it was something educative for the user about the product, after clicking on the video overlay (btw we kept the controls like the big play button, making it look more like a gif) the video would restart and play with sound, pretty simple, but clever and effective.

From an engineering perspective, well, things are a lot easier nowadays, but one thing can still be a pain: interacting with 3rd-party video providers api's (especially the big ones, yes, Vimeo and Youtube). Both use some iframe for injecting the video. We can think about security reasons of course but that makes customizing it a bit hard, youtube takes advantage of that and adds a lot of junk/ own branding, that's good for them since generates organic traffic, but depending on your use case, can be terrible.

![](https://user-images.githubusercontent.com/13686332/124141946-32dd1f80-da60-11eb-8a46-c0112eb580fd.png)

Fortunately, someone posted a solution on [https://github.com/sampotts/plyr/issues/976#issuecomment-862810641](https://github.com/sampotts/plyr/issues/976#issuecomment-862810641 "Github")

Youtube positions the iframe using an absolute value for the cover, making it possible to stretch the video height at a level where all the branding  (and mainly that suggested video terrible panel) dispairs.

![](https://user-images.githubusercontent.com/13686332/124141883-25279a00-da60-11eb-9689-e6b1c7955ace.png)  
The following snippet made the fix for it

    iframe[id^='youtube'] {
      top: -50%;
      height: 200%;
    }

The whole problem began in 2018 when the `?rel` param was removed   
[https://developers.google.com/youtube/player_parameters#release_notes_08_23_2018](https://developers.google.com/youtube/player_parameters#release_notes_08_23_2018 "https://developers.google.com/youtube/player_parameters#release_notes_08_23_2018")