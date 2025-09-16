---
layout: post
title: This is the data analytics portfolio I really want.
image: "https://miro.medium.com/v2/resize:fit:1100/format:webp/0*mZ4F_UroeSHcO3kM"
category: Data Analytics
author: Me
---

## This is the data analytics portfolio I really want.

For some people, including myself, creating a portfolio is quite challenging. As a Data Analyst, I can’t just put what I had been working on in my previous company into my portfolio — yes, so much confidential data in it. I need another source of a dataset that is open to the public. It will be safe for me to publish the analysis from that data.

Due to this reason, many sources suggest creating a portfolio using the dataset either by scraping a website or downloading from a repository site like [Kaggle](https://www.kaggle.com/).

There is totally no problem with that. But, because I have to create from scratch, I want a portfolio that is more personal and close to me.

> _According to [CareerFoundry](https://careerfoundry.com/en/blog/data-analytics/data-analytics-portfolio-project-ideas/), the most important thing from a portfolio is to demonstrate your skills, ideally using a dataset that interests you._

So I decided to make a personal project that I can use as my portfolio.

I want to have a portfolio that is not only showcasing my skill, but also help me to explore myself and hopefully solve my real-world problem.

Seems too much for a data analytics portfolio? Yes, it is 😂.

Still, having a personalized portfolio really interests me. This made me thinking hard of who I really am and what kind of dataset I can get.

![alt text](https://miro.medium.com/v2/resize:fit:1100/format:webp/0*vsP-VU8YsOSAI8Ly "Photo by Fares Hamouche on Unsplash")

Yes, I am a data analyst. Apart from my professional career, I have many hobbies, and one of them is photography. So why don’t I utilize that another-side-of-me to make a personal project in data analytics?

This way, I can have a more personalized portfolio that might be useful for me. Not only from my data analytics perspective, but also for my photography journey.

I started to think about what kind of data I can get from photography. As we know, photography is about the image. I ever thought on doing image processing, but that would be hard and complicated for me to process the data. I don’t even know what I should do with that.

Then, I remember there is data attached to an image file, called **EXIF**. So, what is it?

![alt text](https://miro.medium.com/v2/resize:fit:640/format:webp/1*kZ1aUBqP-_1zqyxK63q2lg.png "Example of EXIF data on a photo file.")

According to [Adobe](https://www.adobe.com/id_en/creativecloud/file-types/image/raster/exif-file.html), EXIF (Exchangeable Image File Format) is metadata of an image file that provides specific information about a photograph, like camera settings, time, date, GPS location, etc. Every time we take a photo using a digital camera (or even a smartphone), a bunch of information is included in the image file.

When we gather EXIF from all of our photos, we will have a new dataset!

---

As EXIF contains a lot of information of a photo, we can do many analysis here. Just to give you an example: we can find the dates on when did we take a lot of photos in one day. But, so what?

I found an [article](https://psycnet.apa.org/record/2016-27715-001?doi=1) from the _Journal of Personality and Social Psychology_. It shows a connection between happiness and taking photos.

> _In short, this research concluded that taking photos during positive activities can enhance enjoyment and engagement._

Meanwhile, we know the benefit of photography is to capture the moment. People tend to want to have photographs related to their experience of pleasing moments. Through seeing photographs, people love to relive their joyful experiences.

![alt text](https://miro.medium.com/v2/resize:fit:1100/format:webp/0*Wg6xQrITpA2Yy7ua "Photo by Priscilla Du Preez 🇨🇦 on Unsplash")

While the study above did not proclaim that _the more you take pictures the happier you are_, but the act of taking photo and earning a greater happiness do have a positive relationship.

Based on this, we can reflect on ourselves when looking through our photos: when we pressed the shutter, how did we feel?

This practice of reflecting on our past can be valuable to know ourselves more, leads to a better self-awareness and personal growth. More comprehensive articles about the benefit of self-reflection are numerous on the internet, and one of them I suggest to read is [here](https://www.smashingmagazine.com/2018/01/importance-self-reflection-part-2).

Ok, that's just one analysis example. Another analysis that came to my mind will most likely improve my photography skills. I will make a separate article covering another analysis possibilities by using this dataset.

---

After getting the dataset idea, here comes the next step: create the dataset.

Now, how do we gather the EXIF from our photo files? There are many ways to do it. I prefer to use Python as this project relates to data analytics and I am more familiar with it.

![alt text](https://miro.medium.com/v2/resize:fit:1100/format:webp/0*VOoLhjEZ5A_mUH0y "Photo by Rubaitul Azad on Unsplash")

In a nutshell, here is how the code works:

1. Declare the file extensions you want the code to read, such as `jpg, dng, tiff, cr3, nef, rw2, orf`, etc.
2. Declare the photos’ path directory
3. Read all photos’ EXIF based on the declared file extensions inside the declared directory
4. Preprocess the data
5. Export as CSV

Here, I chose to export the dataset as CSV because it’s simpler. Later in production, we can choose to export it into a different format or even directly insert it into a database, depending on our needs.

As the following part is more about technical things, I will share the explanation in the next article. For spoiler, you can see the code [here](https://github.com/arkanhadna/read-exif.git).

---

Having a portfolio is important for most people, including myself. One of the most noticeable benefits of having a portfolio is to show our skills to other people.

On the other hand, creating a data analytics portfolio is a bit tricky. We cannot just show our work at the company, as there will be so much confidential data.

This limitation forced me to look at the other data sources. After some extensive time and thinking, I found a dataset that is close to what I like to do, which is photography. I decided to create a personal project that I can use as my data analytics portfolio based on this dataset.

Not only in data analytics, doing this personal project will give a wider benefit for myself, as it will also help me to improve my photography skills.

Furthermore, it may impact my personal growth positively.

###### This article has been posted on [Medium](https://medium.com/@arkanhadna/this-is-the-data-analytics-portfolio-i-really-want-7e8b16d7b0e9) on Apr 13, 2025
