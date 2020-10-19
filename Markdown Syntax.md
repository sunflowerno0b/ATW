# Learning Markdown
## Why am I doing this? 
Much like my username, I am a complete no0b when it comes to all things git, linux, command line and tech in general. I've realized in my path of enlightenment there is not tons of information that starts from the bottom of the barrel. Most things I have seen start from a moderate level or they give you the steps expecting you to know certain steps...I am making this for folks that want to learn from scratch, consider this us learning together. 

## Why should I learn markdown? 
In order to work on Git, your repos will most likely be made in markdown. Best practice in Git is to create a “README.md” file. This file normally tells the git user what the project is about, installation information, and much more. Markdown has two versions: rendered version (the pretty/ easy on the eyes)  & the raw version (this will look like code). See the image below for what I mean about "code". 

![alt text](https://live.staticflickr.com/65535/50491849568_c973f82e5c_n.jpg)

*yes i know the above image has incorrect syntax, i will show you why if you keep on reading!*

# Markdown Preview
## Tools & one tip
If you're not yet a seasoned professional with markdown, it’s great to be able to see a preview of the work you’re doing, live. Currently I am on a Mac (iknow boo- but its what i have). I am using the [Brackets](http://brackets.io/) open source tool in conjunction with the Brackets Mark Down Preview. This allows me to see what I am typing in real time. If don't get the extension you can preview it by clicking the lighting bolt icon and it will open up a chrome window for you to preview, pretty neat. Note that it only works with Chrome. Git has its own preview but its annoying to click between two tabs to see what you're doing as you type. File extension for markdown is ".md". 

***I will be looking into Ubuntu Options as well.For you windows users, I hate that OS so you're on your own- or write me and we can work together to find something!***

# Markdown Syntax
## Titles & Subtitles 
If you're anything like me, you will find a cool project on Git and realize that (in some cases not all) that the publisher has made a complete mess of the page and its generally hard to read. I like things to be clean and clear. Dividing your README.md files into chapters (if you will) is a great way to do that. 

The hashtag # has to come first then a space then your title.
No quotations --> # your desired text
- “#” creates  your title (H1)
- “##”  creates your subtitle (H2)
- “###” -“######” creates your other header types (H3-H6)
Remember that space after the hashtag, spacing is key in markdown as I've learned.

## Paragraphs
To write a pargraph(s), you simply have to write text underneath your title, theres no special spacing or characters needed. Depending on your markdown preview or where you're posting one thing to note is line breaks. Some places might as for a line skip to signal a line break. To break that down: if you are on line 2, and enter your text then press enter and continue the paragraph on line 3- your rendered version will not show the text spaced out, it would be one continuously line. To break that line, you have to skip a line and start, so that is 2, skip line 3, and continue your text on line 4. Your rendered version should show that desired line break. 

## Lists
If you want lists you can add those by using one of two symbols: + or -
You can stack your lists by moving to the next line. If you want to indent, you put a space at the start of the line and enter either the + or -. See below for how that would look. 


![alt text](https://live.staticflickr.com/65535/50492839272_11e3eca921_b.jpg)




## Links & Images 
If you want to include links in your markdown files you enter the description within brackets "[description here]" then the url between parenthesis "(https://www.youtube.com)". Note that there should not be space between the brackets and parentheses- it wont work if there is. 
  
For images, the syntax its a little tricky to understand but bear with me. You're going to include an exclamation point followed by brackets with the words "alt text" then your image URL between parentheses. You can pull image URLs by clicking the image, right click and selecting view info, this is different per website, OS, etc. Will work on a break down a few later.

## In-line Code 
To use the in-line code you're going to want to use the tilde symbol, this should normally be under the esc key on your keyboard. I will let you figure that one out as homework! When you want your code to appear in a block you enter three tildes, then the code you would like, followed by three more tildes on the next line. See the example below

![alt text](https://live.staticflickr.com/65535/50507671977_8767ce2401_b.jpg)

If you want to simply make your command seen, you can wrap the command between two tildes. When I say wrap that means one at the start of the command and one at the end. 

## Tables 
I read somewhere that tables are not normally supported in markdown but Git allows it, so I will show you how to do that. The easiest way is with a photo. 
Take note of the pipe being used between each column. Additional, see that in every line there is a space. In the second line(58) you can see that there are three dashes it has to be 3. 
Also notice the spacing before and after each word and pipe- this is important if you want it to work.

![alt text](https://live.staticflickr.com/65535/50507688327_fe74aa9f78_b.jpg)
  
## Spicy Text
If you want to add a little style **to** ***your*** ~~text~~ you can do the following


 - Bold: wrap your word in two asterisks "*"
 - Italics: wrap your word in three asterisks 
 - Strike out: wrap your word in two tildes "~" 
 
 
