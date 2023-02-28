# backTrack
repush dataLayer events that occurred before consent loaded.

Google Tag Manager over-rides the object.push() functionality of the dataLayer array, to create a queue that can be used to process events.
One of the major benefits of this, is that events triggered before GTM loads will be processed when finally does load.

This functionality does not exist for Consent Management tools however. If an event is triggered before the trust logic has loaded - it will be missed by the tracking.

backTrack is a tag template that adds functionality to repush these missed events into the queue once more, so that data isn't missed.

Steps to implement/configure:
1- Create a tag utilising the template. 

2- Set the tag to fire once per page (IMPORTANT). 

3- Add a trigger to the tag, so that it fires on the first event with consent, see the example below for OneTrust.

<img width="1215" alt="Screenshot 2023-02-28 at 15 09 23" src="https://user-images.githubusercontent.com/125863377/221878439-16792901-e974-454c-818b-6212b0fa579d.png">

4- Adjust the positive REGEX to match the events that you wish to repush. By default the tag will ignore GTM specific pushes and most major consent tool pushes.  

5- (Optional) If you wish to prevent recursive merge for specific objects, change the setting to 'specific' and add the objects as a comma separated list. For example: ecommerce,products.skus. 

        -N.B If the object is embedded, you must specify the entire path to the object.
6- Test that everything behaves as expected.
