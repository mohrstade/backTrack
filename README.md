# backTrack
Repush dataLayer events that occurred before consent loaded.

## Why use backTrack?

dataLayer events allow you to fire your tags at the right moment with the correct data. The timing becomes more complex when consent becomes involved.
If your dataLayer push arrives before the consent management platform and Google Consent Mode (Basic) have initialised - functionality is needed to delay firing the respective tag.

Trigger groups are the feature available in GTM to handle this, but they are unwieldy and can lead to very messy setups. Some of the data associated with the event may also not be available when the trigger group fires.

backTrack is a template attempting to solve this issue and make handling event-timing a lot easier and more convenient.

## How to use backTrack

1. Install the template from the [community gallery](https://tagmanager.google.com/gallery/#/owners/mohrstade/templates/backTrack)
2. Create a tag using the template.
3. Set the tag to fire once per page.
4. Add a trigger to fire the tag on the first event with consent.

**Example:**

<img width="1030" alt="Screenshot 2024-05-06 at 20 09 12" src="https://github.com/mohrstade/backTrack/assets/125863377/e521e325-cd73-479d-83b8-9ecc2bac9927">

6. [Optional] Configure the REGEX for which events you want to re-push. By default GTM events and the most common consent events are excluded from being re-pushed. This is very important to prevent the consent state from being altered. To be explicit, change the REGEX to match the specific events you want to re-push.
7. [Optional] Configure the prevent recursive merge feature by changing the setting to ‘On’ and adding any objects that should be cleared between events (for example ecommerce).

**Example:**

<img width="900" alt="Screenshot 2024-05-06 at 20 06 35" src="https://github.com/mohrstade/backTrack/assets/125863377/65ed8dce-6f15-4d07-b615-b13ee2c39039">


### Google Consent - Advanced Mode
Google Consent Mode (Advanced) has its own functionality to automatically fire events again after consent is granted (via the update command). backTrack will function for all tags as it is repushing events.
To prevent duplicate events being sent, a blocking trigger needs to be added to all Google Tags when Consent Mode (Advanced only) is being used. The **blocking trigger** should fire on all events with pushType 'Artificial’.

<img width="902" alt="Screenshot 2024-05-06 at 20 03 19" src="https://github.com/mohrstade/backTrack/assets/125863377/0c223f07-5970-4553-b6c9-15553d418e56">

After the tag has finished re-pushing all events, it will set a dataLayer variable `backTrack_fired` with the boolean value `true` to indicate that the tag has already fired.


### Safety Features
The template has in-built functionality to prevent multiple firings, as this could cause infinite loops. It is still worth explicity setting the tag to fire once per page.


### backTrack_fired
After the tag has finished re-pushing all events, it will set a dataLayer variable `backTrack_fired` with the boolean value `true` to indicate that the tag has already fired.


### A Note on Privacy
The aim of this template is not to track events that occurred before the user provided consent, rather to make handling the timing easier. A consent decision should be enforced by the banner before the user interacts with the page.
If you have a single page application ensure that the entire page is reloaded when consent is changed - as this is needed to unload analytics/marketing libraries.
