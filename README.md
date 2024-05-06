# backTrack
Repush dataLayer events that occurred before consent loaded.

## Why use backTrack

dataLayer events allow you to fire your tags at the right moment with the correct data. The timing becomes more complex when consent becomes involved.
If your dataLayer push arrives before the consent management platform and Google Consent Mode (Basic) have initialised - functionality is needed to delay firing the respective tag.

Trigger groups are the feature available in GTM to handle this, but they are unwieldy and can lead to very messy setups. Some of the data associated with the event may also not be available when the trigger group fires.

backTrack is a template attempting to solve this issue and make handling event-timing a lot easier and more convenient.

## How to use backTrack

1. Install the template from the [community gallery](https://tagmanager.google.com/gallery/#/owners/mohrstade/templates/backTrack)
2. Create a tag using the template.
3. Set the tag to fire once per page.
Add a trigger to fire the tag on the first event with consent.
4. [Optional] Configure the REGEX for which events you want to re-push. By default GTM events and the most common consent events are excluded from being re-pushed. This is very important to prevent the consent state from being altered. To be explicit, change the REGEX to match the specific events you want to re-push.
5. [Optional] Configure the prevent recursive merge feature by changing the setting to ‘On’ and adding any objects that should be cleared between events (for example ecommerce).

### Google Consent - Advanced Mode
Google Consent Mode (Advanced) has its own functionality to automatically fire events again after consent is granted (via the update command). backTrack will function for all tags as it is repushing events.
To prevent duplicate events being sent, a blocking trigger needs to be added to all Google Tags when Consent Mode (Advanced is being used). The blocking trigger should fire on all events with pushType 'Artificial’.

### backTrack_fired
After the tag has finished re-pushing all events, it will set a dataLayer variable `backTrack_fired` with the boolean value `true` to indicate that the tag has already fired.
