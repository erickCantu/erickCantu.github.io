---
title: "Image Protms for Midjourney" 
categories: 
    - Data_Science
    - Promt Engineering
    - Artificial Intelligence
tags: 
    - artificial intelligence
    - data science
    - promts
    - midjourney
    - art
    - imaging
last_modified_at: 2023-04-28T23:00:00-01:00
image: /assets/images/posts/promts_midjourney/ecantu_Create_a_composite_landscape_photograph_for_the_header_o_35851b07-126a-45da-aa1d-25e61c565656_top.png
---

The importance of having the correct prompt to recreate an image in Midjourney is the base to achieve the expected results. A bad prom;t leads to find either not the target or nice surprises.  Even when the main goal is to create an artistic image of our imagination, it is necessary to have a structure to meet our needs with the minimum use of resources. 

With this purpose in mind, we can use a GPT solution to simplify our work. I am presenting a prompt structure. This structure is being used in ChatGPT-4 to create 3 possible prompts for Midjourney. 

```
I) Your role
Take the role of a Prompt Engineer with bast experience in Midjourney. 

II) The Request Context:
You will use the following structure to create prompts:
Content, Medium, Style, Lighting, Color Palette, Composition.

Unless the variables values are given to you, generate random values based in the following definitions:
Medium: insert artistic medium here.
Style: insert an Artist or Genre. 
Lighting: insert a lighting type utilized in photography or painting.
Color Palette: insert the color pallet to use, verify that matches the style type.
Composition: insert cameras models, specific lenses, photography or image types, positional elements.

III) Your work:
I will provide your with content ideas. 
With these ideas you will help to write 3 different prompts to create images and art. 
Write in natural language, utilize specific, precise, and articulated language. 
Include the following text at the end of each promt:
"--no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark.
```

### Example - EDA King County Washington

**For the EDA post, I added a new image header to the webpage. To create it, I used the following prompt.**

`An aerial recreation of King County Seattle Washington housing. Consider key sightseeing in Seattle. To be use in a realtor marketing campaign. The target market is high income.
Medium: photo realistic image.
Style: 4K photograph 
Lighting: emphasize depth and contrast
Color Palette: early golden hour
At  the end of the prompt add  --aspect 7:4 `

**ChatGPT-4 provided the following prompts:**

1. `Design a captivating aerial image of King County Seattle Washington housing, incorporating significant Seattle landmarks, intended for a realtor marketing campaign, in a photo-realistic 4K photograph with lighting that accentuates depth and contrast, and showcasing a rich midnight blue color palette. –no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark. –aspect 7:4`

2. `An aerial recreation of King County Seattle Washington housing. Consider key sightseeing in Seattle. To be use in a realtor marketing campaign. The target market is high income. Medium: photo realistic image Style: 4K photograph Lighting: emphasize depth and contrast Color Palette: early golden hour At the end of the prompt add –aspect 7:4`

3. `Compose an impressive aerial representation of King County Seattle Washington housing, highlighting key attractions in Seattle, suitable for a realtor marketing campaign targeting high-income clients, as a photorealistic 4K photograph with evocative lighting that highlights depth and contrast, and featuring an early golden hour color palette. –no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark. –aspect 7:4`

**The provided prompt to Midjourney was:** 

`Compose an impressive aerial representation of King County Seattle Washington housing, highlighting key attractions in Seattle, suitable for a realtor marketing campaign targeting high-income clients, as a photorealistic 4K photograph with evocative lighting that highlights depth and contrast, and featuring an early golden hour color palette. --no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark. --aspect 7:4 --s 750 --v 5 --q 2 `

**And the results are:**
![image](/assets/images/posts/promts_midjourney/ecantu_Compose_an_impressive_aerial_representation_of_King_Coun_2880dd47-91d0-4b21-8ac5-0e98f1145cb3.webp "Compose an impressive aerial representation of King County Seattle Washington housing, highlighting key attractions in Seattle, suitable for a realtor marketing campaign targeting high-income clients, as a photorealistic 4K photograph with evocative lighting that highlights depth and contrast, and featuring an early golden hour color palette. --no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark. --aspect 7:4 --s 750 --v 5 --q 2 ")

## Prompts used in this website

### Kickstarter

`Design a vector illustration for a website header with the topic of Kickstarter, depicting a rocket launching to symbolize project success. The style should be modern and sleek, with dramatic lighting and a strong light source coming from behind the rocket. The color palette should include contrasting shades of blues, greens, and whites to convey the excitement of innovation. Compose the image with a diagonal layout, and have the rocket take up most of the frame for a dynamic effect. --no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark. --aspect 7:3 --s 750 --v 5 --q 2 `

**Result:**

![image](/assets/images/posts/promts_midjourney/ecantu_Design_a_vector_illustration_for_a_website_header_with_t_73f6d8ed-d887-4070-a476-95b37d77d65d.png "Design a vector illustration for a website header with the topic of Kickstarter, depicting a rocket launching to symbolize project success. The style should be modern and sleek, with dramatic lighting and a strong light source coming from behind the rocket. The color palette should include contrasting shades of blues, greens, and whites to convey the excitement of innovation. Compose the image with a diagonal layout, and have the rocket take up most of the frame for a dynamic effect. --no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark. --aspect 7:3 --s 750 --v 5 --q 2")

### The Green City Solutions Group

`Take a realistic 4K photograph of a 9-building complex focused on forecasting building energy demand, which includes a fast-food restaurant, standalone retail, strip mall retail, and 7 multi-family buildings. Visibly integrate solar panels, wind turbines, and heat pumps. Use warm, golden-hour sunlight for lighting to emphasize the eco-friendly nature of the buildings. The color palette should consist of earth tones, with subtle green and blue accents to symbolize energy efficiency. Compose the image with an elevated perspective, highlighting the buildings and energy sources from an interesting angle. --aspect 7:3 --no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark. --s 750 --v 5 --q 2`

![image](/assets/images/posts/promts_midjourney/ecantu_Take_a_realistic_4K_photograph_of_a_9-building_complex_f_ceff2667-a1fd-44f3-8715-2cf92c736e75.webp "Take a realistic 4K photograph of a 9-building complex focused on forecasting building energy demand, which includes a fast-food restaurant, standalone retail, strip mall retail, and 7 multi-family buildings. Visibly integrate solar panels, wind turbines, and heat pumps. Use warm, golden-hour sunlight for lighting to emphasize the eco-friendly nature of the buildings. The color palette should consist of earth tones, with subtle green and blue accents to symbolize energy efficiency. Compose the image with an elevated perspective, highlighting the buildings and energy sources from an interesting angle. --aspect 7:3 --no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark. --s 750 --v 5 --q 2")

### Image Prompts for Midjourney

`Create a composite landscape photograph for the header of a personal webpage, combining the mountains of Mexico, including Cañon del Sumidero, Cañón Namurachi, Cañón de Aquetzalli, and Barranca del Cobre, with the Black Forest in Germany, adding mist to create a surreal and mystical atmosphere, using a color palette of dark greens and blues, and composing the image with strong foreground elements to provide depth and scale. No text. No signature. --v 5 --s 750`

![image](/assets/images/posts/promts_midjourney/ecantu_Create_a_composite_landscape_photograph_for_the_header_o_3d043cc6-3d54-42dd-bee1-c01e09cc4a45.webp "Create a composite landscape photograph for the header of a personal webpage, combining the mountains of Mexico, including Cañon del Sumidero, Cañón Namurachi, Cañón de Aquetzalli, and Barranca del Cobre, with the Black Forest in Germany, adding mist to create a surreal and mystical atmosphere, using a color palette of dark greens and blues, and composing the image with strong foreground elements to provide depth and scale. No text. No signature. --v 5 --s 750")

This image still had a Signature in the third variation. Which I thought the `No Signature` part at the end would have been enough. But it did not work. It lead me to better understand the negation process in Midjourney. After this image and other similar ones, I added the command `--no Human, People, Person, Letters, Numbers, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark.` 
