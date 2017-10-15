---
output:
  pdf_document: default
  html_document: default
---

# STAT545-hw01-Mei-Lucy

This is the repository of Lucy Mei.
http://stat545.com


# About Me
## Personality
| **Personality** |        **Level**        |
|-----------------|-------------------------|
| Kindness        | Average :smiley:        |
| Evilness        | Depends :smiling_imp:   |
| Sarcasm         | High :star::star::star: |
| Confidence      | More on the humble side |
| Creativity      | ......High? :satisfied: |

## Background

### Education
I studied **biochemistry** during my undergrad at **UBC** and now I am a Master student in *Experimental Medicine* program. My research project is related to **pediatric cancer** and mainly focuses on *regulation of cytockeleton* during cell division. 

Although I am a Science student now, I have a second career goal to become an **Artist**. I was choosing between Science at UBC and Animation Design at Emily Carr and I am in Science now. Occasionally, ~~I wish I can do design instead~~. (Just kidding, I just want to use the strikeout function)
 
### Hobbies and Interests
- Sports
    + Fishing
        * My favourite sport
    + Skating
        * Just simple skating, learnt by myself
    + Skiing
        * Never tried it before, but I think I like it

***And Other skills?***
1. Chinese Calligraphy
2. Chinese, English, Japanese, a little bit Spanish and German

- Movies and books?
  + Thriller/Mysterious
  + Comedy
  + Detectives
  + Fiction
  + Sometimes action

## Quotes I like
>"Pride relates more to our opinion of ourselves, vanity to what we would have others think of us."
>
> *Pride and Prejudice* by Jane Austen

## Python Code I typed

```R
from PIL import Image

im1 = Image.open("test_image.jpg")
im2 = Image.open("deer.jpg")

(w1, h1) = im1.size
(w2, h2) = im2.size


for i in range(w2):
    for j in range(h2):
        im1.putpixel((i,j), im2.getpixel((i,j)))


im1.save("collage_image.png")

```


## Some works I did
![I made cards sometimes](https://i.imgur.com/GkCPqcm.jpg)

![A practice](https://i.imgur.com/aOPkrZb.jpg)



## Last year I went to Europe, love it, want to go there again
![](https://i.imgur.com/tiDJUnC.jpg)
![](https://i.imgur.com/qRXJwlL.jpg)
![](https://i.imgur.com/LxmDk1v.jpg)


[![Sightview](https://youtu.be/v4hw2dxZaRU)](https://www.youtube.com/watch?v=v4hw2dxZaRU&feature=youtu.be)

Suppppppppppppper Fuuuuuuuuuuun!!
![Suppppppppppper Fuuuuuuun](http://i.imgur.com/iX6W66g.gif)

Source from (https://imgur.com/gallery/YRSmU)


You can see more pictures about me <a href="https://imgur.com/jkxCbUn">at here</a>.


## Report my process
I edited the markdown file locally, then I saved and committed it for all the changes. Then I pushed it to github.com.

I think it is pretty straightforward. One thing I was a little bit confused about was the emoji installation. I installed the emoji packages and I used it according to the instruction. It looked fine on the github page but I tried to preview it with html, the emoji was not showing up, instead it is just a code there. I am not sure if this is what it is supposed to be.
