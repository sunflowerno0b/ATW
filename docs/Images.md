## A Better Way to Adding Images 
At the time of writing, I knew nothing about how folks added images to their git pages, digital gardens etc. Trying to figure it out the way, I resorted to creating a flickr, pulling images from the web or my screenshots and uploading the link. I believe its in my Markdown Syntax page, but don't quote me. 

The reason I didn't want to host on flickr is because:
* limit on image storage 
* creating yet another account, thus increasing my digital footprint 
* pulling images from the web is annoying 
* i didn't like my personal mistakes living on the web 

My friend taught me another way. In my currently structure I have a docs folder which contains the guts of my digital garden. To host my own images I need to go to my `docs` folder and create the `img` folder. 
To do that running the command within your path to `docs` : `mkdir img`.
From that directory I can now store my images. But now that they have a place to live, I need to reference them so my mkdoc can pull the image to my ATW site.

When referencing any image in a post it should be `! [ text?] (IMAGE NAME.JPG)`. 

I need to double check this command by trying it out. Will update with any bugs I find. 

### Test

<img src="GIT/ATW/docs/img/outerspace.png">