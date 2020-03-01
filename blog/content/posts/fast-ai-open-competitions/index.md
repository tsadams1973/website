---
title: "Tampa Artificial Intelligence Meetup"
date: 2020-02-06
draft: false
type: "post"
description: "Finding State of the Art Techniques Through Open Competition"
tags: ["ai","fastai","imagenette","woofnet","wangnet","meetup"]
---

This week I attended an event put on by the [Tampa Artificial Intelligence Meetup](https://www.meetup.com/Tampa-Artificial-Intelligence-Meetup) entitled ["Finding State of the Art Techniques through Open Competitions"](https://www.meetup.com/Tampa-Artificial-Intelligence-Meetup/events/268349608/). It was a smaller event, with maybe 7 people attending, but welcoming, accessible, and informative.

The organizer, [Scott Mueller](https://github.com/meanderingstream), gave a presentation introducing us (maybe only me?) to [fast.ai](https://www.fast.ai/) and how to use machine learning algorithms to solve different image recognition problems. You can find the [slides here](https://meanderingstream.github.io/competitions_state_of_art/#/).

The presentation kicked off with a quick discussion about learning rate, its importance to, and impact on model performance ([a topic that had been discussed at a previous meetup](https://www.meetup.com/Tampa-Artificial-Intelligence-Meetup/events/267339466/)). This was used to segue into the discussion of fast.ai, and some competitions they are running on image recognition. The first of these was [*imagenette*](https://github.com/fastai/imagenette) (which apparently is to be pronounced with a caricature of a french accent). 

*Imagenette* is a subset of 10 easily classified classes from [ImageNet](http://www.image-net.org/). It was originally created to have a smaller dataset than ImageNet for testing ideas against. However, in addition to this, fast.ai is using the dataset to pose challenges for researchers to create accurate classifiers given different constraints, such as within a certain number of epochs or budget. They have posted a leader board to track the results of this competition.

 In addition to *Imagenette*, fast.ai has both *imagewoof* and *imagewang*. *Imagewoof* is a similar subset of ImageNet classes, but more challenging because it is based on dog breeds. *Imagewang* is a combination of the two subsets with a few other twists regarding the number of images in the sample.

The presentation reviewed a [sample Jupyter Notebook](https://github.com/muellerzr/Practical-Deep-Learning-For-Coders/blob/master/02b_SOTA.ipynb) from the competition. This example was interesting because we could see how some researchers approached the challenge. 

The meetup wrapped up with a discussion on the usefulness of these competitions for developing new approaches to image classification problems.

The next meetup is scheduled for February 12th and should involve a review of a couple papers:

* [Self-Supervised Learning of Pretext-Invariant Representations](https://arxiv.org/abs/1912.01991)

* [Momentum Contrast for Unsupervised Visual Representation Learning](https://arxiv.org/abs/1911.05722)

It was a great experience and I plan to go to more events hosted by the Tampa Bay Artificial Intelligence Meetup in the future.
