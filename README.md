# zuck.js

## Put stories EVERYWHERE
MWHAHAHAHA. Seriously. This script is a copy of Facebook Stories of a copy of Facebook Messenger Day of a copy of WhatsApp status of a copy of Instagram stories of a copy of Snapchat stories. 

You can read stories from any endpoint (json, firebase, etc.) and the script will do the rest.


## Features
* Custom themes
* Desktop support (why not?)
* A simple media viewer, with gestures and events
* A simple api to manage your "Stories timeline"
* Lightweight


## How to use
Initialize:

	var stories = new Zuck({
        id: '', //container id or reference
        skin: 'snapgram', //container class
        avatars: true, //show user photo instead of last story item preview
        saveRead: function(storyId, storyItemId, status){
            // function to save user reading story status. if not defined, local storage is used.
        },
        autoFullScreen: false, // enable fullscreen on mobile browsers
        expiresIn: 24, // expiration hours to remove item from story
        backButton: true, // add a back button to close the story viewer
        backNative: false, // uses window history to enable back button on browsers/android
        stories: [ // array of stories
            // See stories structure example
        ]
    });

Add/update a story:

	stories.update(storyId, {item object});

Remove a story:

	stories.remove(storyId); // item id optional

Add/Remove a story item:

	stories.addItem(storyId, {item object});
	stories.removeItem(storyId, itemId);

## Stories structure example
A json example of the stories object:

    {
        id: "", //story id
        photo: "", //story photo (or user photo)
        name: "", //story name (or user name)
        link: "", // story link (useless on story generated by script)
        lastUpdated: "", // last updated date in unix time format
        items: [
            //story item example
            {
                id: "", //item id
                type: "", //photo or video
                length: 5, //photo timeout or video length in seconds - uses 5 seconds timeout for images if not set
                src: "", //photo or video src
                preview: "", // optional - item thumbnail to show in the story carousel instead of the story defined image
                link: "", // a link to swipe up
                time: "", // optional - unix timestamp for created story date
                seem: false // set true if current user was read - if local storage is used, you don't need to care about this.
            }
        ]
    }   
    
## Alternate call
In your HTML:

    <div id="stories">
        <div class="story" data-id="{{story.id}}" data-last-updated="{{story.lastUpdated}}" data-photo="{{story.photo}}">
            <a href="{{story.link}}">
                <span><u style="background-image:url({{story.photo}});"></u><span>
                <strong>{{story.name}}</strong>
            </a>
            <ul class="items">
                <li data-id="{{story.items.id}}" data-time="{{story.items.time}}" class="{{story.items.seem}}">
                    <a href="{{story.items.src}}" data-type="{{story.items.type}}" data-length="{{story.items.length}}" data-link="{{story.items.link}}">
                        <img src="{{story.items.preview}}">
                    </a>
                </li>
            </ul>
        </div>
    </div>

Then in your JS:

	var stories = new Zuck({
        id: 'stories'
    });


## Compatibility