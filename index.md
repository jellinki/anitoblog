---
layout: default
title: Katelyn Gelle's Blog
---

<div style="text-align: center; margin-top: 20px; margin-bottom: 20px;">
  <img src="{{site.baseurl}}/images/anito/wadelink.gif" alt="Link in the Water, The Legend of Zelda: Breath of The Wild" />
</div>  

</script>
<!-- Liquid:  statements -->

<!-- Include submenu from _includes to top of pages -->
{% include nav_home.html %}
<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %} 

## Katelyn's Blog
Hello, welcome to my blog! My name is Katelyn Gelle. I am a senior at Del Norte High School. I am seventeen years old, and my favorite color is purple. Here are my classes this trimester:

<!--to make things appear on separate lines, add two spaces after each "line"-->
1st Period: Physics/Chemistry  
2nd Period: AP Statistics  
3rd Period: AP Literature & Composition  
4th Period: Computer Science  
5th Period: AP US Government & Politics  

Outside of school, I enjoy participating in Science Olympiad as both a coach and a competitor. I am a tutor in English and mathematics, and I love to both teach and play piano! Apart from these, I enjoy listening to K-Pop music, and I recently went to see ENHYPEN's concert in February! :D

### Contact

Want to hear more about me? Visit my [LinkedIn](https://www.linkedin.com/in/katelyn-gelle-6b225b278/)!