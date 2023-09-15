# Weekly Report 3 - 09/07/2023 - 09/14/2023

## Summary 
This week I worked on project 1 to create a personalized cell phone stand. To achieve it, I went through 4 stages, ideation and sketching, modeling and iteration, 3D printing, and reflection. In this report I will record my design in detail and also reflected on the challenges and potential future improvement.

## Project 1: Computational Design

#### Step 1: Ideation and Sketching
Prior to sketching my design, I took some time to survey the cell phone stands available in the market. I made note of the aspects that intrigued me in these designs. Additionally, while browsing, I reflected on my own requirements for a cell phone stand in everyday life.
<p align="center">
  <img width="750" alt="otherStandDesigns" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/b82e923c-37ff-4d7d-8c11-fb69c067b5b5">
</p>

I drew multiple sketches for different design ideas. Considering feasibility and fun, and finally selected the design for a cell phone stand + audio amplifier. 
![IMG_6354](https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/7d2bebeb-3b60-45d5-9547-b1fe484f097e)


#### Step 2: Modeling and Iteration

I used Grasshopper to model my phone stand. The screenshot below shows the initial version of my model.
<p align="center">
  <img width="500" alt="WechatIMG818" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/51eb2213-b21e-4497-a8b9-35e30b271ea2">
  <img width="500" alt="截屏2023-09-13 21 42 56" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/21b498ae-67ae-4fc1-98fc-37fcc8cd1d80">
</p>

I first built a rectangular box with two cylinders as the major part of my model. Then I built a similar but smaller entity and made boolean difference with the bigger one to make the internal structure hollow.
<p align="center">
  <img width="500" alt="截屏2023-09-13 21 43 11" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/df2b7e95-9015-4207-b9fa-8644d29adca1">
</p>

Then I added two rectangular boxes inside the shell to hold the phone.
<p align="center">
  <img width="500" alt="截屏2023-09-13 21 44 09" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/f05b56b1-2241-45bf-8f97-715dd44eab8d">
</p>

The next step I used boxes to created acoustic structures that can amplify the sounds from the phone.
<p align="center">
  <img width="500" alt="截屏2023-09-13 21 44 21" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/ae64d25f-9ce8-4704-ba4b-6641ee592639">
</p>

After exporting the first model and slicing it in cura, I found the extimated time is 8 hours and then I started to consider methods of reducing printing time. I adjusted the parameters in grasshopper to make the model thinner and smaller so that the solid part needed to be printed was reduced. In this process, I also came up with several ideas to improve the model.
<p align="center">
  <img width="500" alt="截屏2023-09-13 21 37 36" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/5bb77b86-a9e5-4fb6-9d0c-2122eb32c015">
</p>

- Adding space for charging cable: 
<p align="center">
  <img width="250" alt="截屏2023-09-13 21 37 49" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/f7e516b0-646b-4621-9573-c95007345246">
</p>

- Extending the internal structure to improve stability:
<p align="center">
  <img width="250" alt="截屏2023-09-13 21 38 10" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/a3052727-ffa8-4a6b-95fc-30aab5f5901b">
</p>

- Deleting the hollow structures on the backside of the stands to improve the audio effect:
<p align="center">
  <img width="250" alt="截屏2023-09-13 21 38 31" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/7b98a6ea-8de7-4242-9ddb-01d898b08bc3">
</p>


The following pictures is the screenshots of the .stl file after baking and eexporting the model.
<p align="center">
  <img width="500" alt="截屏2023-09-13 21 30 26" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/50f6b405-6fd9-4da8-be1f-a477bb74b0c9">
  <img width="500" alt="截屏2023-09-13 21 30 14" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/a010668e-08a2-4ce6-be28-9f57a1bc8fa5">
</p>

#### Step 3: 3D Printing
I put the .stl file in Cura to prepare it for 3D printing. I rotated my model to reduce the support and then sliced it. Compared with my first model, the estimated time was reduced to 6 hours from 8 hours.
<p align="center">
  <img width="500" alt="截屏2023-09-13 22 13 31" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/ad5b2df7-921e-45a8-aa69-73f80eec4373">
</p>

Start my printing!
<p align="center">
  <img width="500" alt=“IMG_6381” src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/3b5298bf-e968-4001-b80e-36b92c797c7a">
</p>

#### Exhibition
This is my initial printout, and it's evident that it didn't turn out as expected. Upon inspection, I realized that I mistakenly selected the profile for the Prusa printer in the print file, but I actually used the Ultimaker 3 for printing. I also chose the fast and lower quality profile while printing. But happily, my design achieved the expected function. The audio amplifier sounds amazing and it can hold my cell phone steadily. 

<p align="center">
  <img width="500" alt=“IMG_6382” src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/37e0d636-c7f2-4df1-9203-bc2f21dbb809">
</p>

After recognizing the errors in printing, I reconfigured the printer to Prusa and printed a piece using the normal profile and this work will be finished after the end of this week’s TDF class.

<p align="center">
  <img width="500" alt=“IMG_6380” src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/4e491e10-ce8c-45f5-b262-0b78eeb097fd">
</p>

Link of the presentation video: https://www.youtube.com/watch?v=A9CtUZZ4MDk


## Reflection
- I learned about GHX after completing my modeling work. It's a feature that enables me to use programming languages for modeling. Given my prior programming experience, I'm interested in exploring this feature. Working with Grasshopper has been overall enjoyable, and I've noticed improvement compared to previous weeks.
- This week, while studying Latour's Compositionist Manifesto in the course 'Debates in Design,' I came across the concept of ecocentrism in ecological politics. I'm interested in further researching the idea of ecocentric design and exploring ways to integrate it into my own design work.
