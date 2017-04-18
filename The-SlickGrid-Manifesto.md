There are a lot of requests for code for SlickGrid use cases and for updates to core code. We're also being asked for packaging via npm, nuget and bower.  
I have always thought that SlickGrid is best seen as a toolkit. It's not the finished, polished product, ready to use, but it **is** a highly adaptable and flexible foundation that will get you 95% of the way there. 

MLeibman says it best in his wiki:

> The key difference is between SlickGrid and other grid implementation I have seen is that they focus too much on being able to understand and work with data (search, sort, parse, ajax load, etc.) and not enough on being a better “grid” (or, in case of editable grids, a spreadsheet). It’s great if all you want to do is “spruce up” an HTML TABLE or slap a front end onto a simple list, but too inflexible for anything else.

> Data is complicated. It has business rules. It has non-intrinsic properties. Editing one property of an element can lead to cascading changes modifying other properties or even other elements. It has dependencies. What I’m saying, is that dealing with data is best left to the developer using the grid control. Trying to fit all of that into the grid implementation and API will only limit its applicability and add considerable bloat.

The toolkit nature of SlickGrid is actually its strength: it's expected that everyone will customise it a little bit to get where they want to go. But at least we don't all have to try to remove or work around a whole bunch of features we can't use and don't want.

This is the reason that, although your modifications may be very useful, they may not always make it into the main repo. The plugin architecture is there to help keep options modular, but it can't always be used. Changes have to be carefully screened to make sure they are not locking the project into specific use cases.

This is also the reason that we are not going to try to release a deployment version of the code.  
This repo will always be source, it will always require you to create a build process to assemble the components you want and get them into your project, and that's the way it should be.