Whether you are reporting a bug on GitHub or getting help with your issue on StackOverflow, with a tool as complex as SlickGrid it often comes down to needing to be able to *share your use case* with the people who are trying to help.

The following steps are critical in being able to do this:
- create a sample web page in the 'examples' folder of copy of the current 6pac SlickGrid repo on your local computer. You don't need to be using Git locally (it can just be a downloaded and unzipped repo), but the sample *must run* from this location. Modify other files if you need to. It's good to use an existing example as the basis for your page.
- you may need to simplify your use case to get it to run in the sample page. This is good, since *about 80% of the time you will solve your problem during this process*.

Now you have several options for sharing this:
- send the file to the email address on my or another contributor's [GitHub profile page](https://github.com/6pac)
- OR, if this is related t a GitHub Issue, you may add the sample web page and any other modified files to a ZIP file, and add it to a GitHub issue comment, by dragging and dropping it onto the comment (or by clicking the link at the bottom of the comment).

We can then download the page to our local repo. Because we are using the same repo as a starting point, we have a repeatable environment.

### jsFiddle et al

In the past, there have been jsFiddle or jsBin sharings, and they could be regarded as another option.  
However these tools are designed for small and simple javascript snippets, and aren't quite up to projects like SlickGrid with extensive CSS and images.  

With all these tools, external script and css links must be specified. So, for example,  
     ```<script src="../slick.grid.js"></script>```   
must be changed to  
     ```<script src="https://6pac.github.io/SlickGrid/slick.grid.js"></script>```  
See [here](https://jsbin.com/valigaz/edit?output) for a sample using jsBin.  

Both have problems with dynamically constructed relative links (such as used in the Slick.Formatter images in the sample above).  jsFiddle also tampers with the page structure somewhat.

All in all, I would not recommend using these tools, but if you are willing to put in the work to set them up, and live with the shortcomings, you may find they work for you.
