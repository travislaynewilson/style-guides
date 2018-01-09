# Travis' Web Language Style Guide

*My approach to writing clear, concise web content*

## Table of Contents

  1. [Language](#language)
      1. [Addressing users](#addressing-users)
      1. [Avoid the pronoun "we"](#avoid-the-pronoun-we)
      1. [Be concise](#be-concise)
      1. [Write in the present](#write-in-the-present)
      1. [Write simply and directly](#write-simply-and-directly)
      1. [Write conversationally](#write-conversationally)
      1. [Text for buttons and related elements](#text-for-buttons-and-related-elements)
      1. [Write for all levels of readers](#write-for-all-levels-of-readers)
      1. [Use consistent words in all parts of a feature](#use-consistent-words-in-all-parts-of-a-feature)
      1. ["1, 2, 3", not "one, two, three"](#1-2-3-not-one-two-three)
      1. [Begin with the objective](#begin-with-the-objective)
      1. [Reveal detail as needed](#reveal-detail-as-needed)
      1. [Never say "never"](#never-say-never)
      1. [Text for buttons and related elements](#text-for-buttons-and-related-elements)
  1. [Tone](#tone)
      1. [Be friendly, respectful, and focus on the user](#be-friendly-respectful-and-focus-on-the-user)
      1. [Be humble](#be-humble)
      1. [Be inviting](#be-inviting)
      1. [Be positive](#be-positive)
      1. [Be essential](#be-essential)
  1. [Capitalization](#capitalization)
  1. [Punctuation](#punctuation)



## Language



### Addressing users

Your UI should address the user using either:

- **Second person, “you” or “your”**: Use this conversational style for most situations, as though the app is speaking directly to the user.

  ```
  Quickly open the camera without unlocking your screen

  Your places
  ```

- **First person, “I” or “my”**: In some cases, you may need to use this form of address to emphasize the user's ownership of content or actions.

  ```
  I agree to follow the Google Terms of Service

  My Account
  ```


Avoid mixing "me"/"my" with "you"/"your.”

> Why? It can cause confusion to see both forms of addressing the user in the same context.

```
/* avoid */
Change your preferences in My Account
```
 
**[⬆ back to top](#table-of-contents)**<br /><br />

  
  
### Avoid the pronoun "we"

Focus on the user and what they can do with your app, rather than what you or your app is doing for the user.

One exception is when a person takes an action for a user, such as reviewing an appeal or responding to a suggestion. Here, the use of “we” is appropriate.

Good | Avoid
---- | -----
Get started with these popular posts | To get you started, we’re showing you the most popular posts this week.
We’ll review your appeal and respond within a few days | Your appeal will be reviewed, and you will receive a response within a few days
    
**[⬆ back to top](#table-of-contents)**<br /><br />
    
    
    
### Be concise

Write in small, scannable segments to facilitate navigation and discovery.

Keep your sentences and phrases short, with as few concepts as possible.

Good | Avoid
---- | -----
Send money to anyone in the US who has an email address. It’s fast, easy, and free. | Send (and receive) money with friends and family in the US with an email address. It’s a two-step process with little-to-no latency and there aren’t any charges for the recipients of the money.
Read the instructions that came with your phone | Consult the documentation that came with your phone for further instructions

**[⬆ back to top](#table-of-contents)**<br /><br />



### Write in the present

Use the present tense to describe product behavior. 

Avoid using the future tense to describe the way a product always acts.

When you need to write in the past or future, use simple verb forms.

**[⬆ back to top](#table-of-contents)**<br /><br />



### Write simply and directly

Use simple, direct language that is easy for users to understand.

Try to keep your content simple and scannable.

Common introductory phrases may be omitted.
  
Good | Avoid
---- | -----
Save changes? | Would you like to save your changes?
Delete reminder? | Are you sure you want to delete this reminder?
Message sent | Message has been sent
Register to rate | You must register before you can rate this pharmacy
 
**[⬆ back to top](#table-of-contents)**<br /><br />



### Write conversationally

Use language that simulates a conversation with the user.

Avoid language that solely describes actions pertaining to the UI.
  
Good | Avoid
---- | -----
Got it | Close window
Sign in | Login
Done | Save changes
 
**[⬆ back to top](#table-of-contents)**<br /><br />


  
### Write for all levels of readers

Pick common words that are clearly and easily understandable to both beginning and advanced English readers.

Good | Avoid
---- | -----
Turn on notifications | Enable notifications


Avoid industry-specific terminology or names invented for UI features.

Good | Avoid
---- | -----
Preparing video…  | Buffering…
“Exporting to PDF” isn’t supported on your phone | "Exporting to PDF" is only supported on dual-core devices


Refer users to the labels on UI elements, not the type of element (such as menu or button).

Good | Avoid
---- | -----
Click **Continue** | Click the Continue button
  
**[⬆ back to top](#table-of-contents)**<br /><br />
  
  
  
### Use consistent words in all parts of a feature

Use verbs in a consistent manner across the description of an action.

When possible, prefer using verbs that are distinctly associated with the feature.

Good | Avoid
---- | -----
Remove photo | Delete photo
Remove photo? | Remove photo from page?
Compose mail | New message
Add contact | New contact
  
**[⬆ back to top](#table-of-contents)**<br /><br />
  
  
  
### "1, 2, 3", not "one, two, three"

Use numerals in place of words for numbers.  

One exception is when mixing uses of numbers, such as "Enter two 3s."
  
> Why? Using numerals promotes scannability.

Good | Avoid
---- | -----
You have 3 messages | You have three messages
  
**[⬆ back to top](#table-of-contents)**<br /><br />
  
  

### Begin with the objective

If a sentence describes both an objective and the action needed to achieve that objective, start the sentence with the objective.
  
> Why? Starting a sentence with the objective sets the user's expectation early and promotes scannability.

Good | Avoid
---- | -----
To remove a photo from this album, drag it to the trash | Drag a photo to the trash to remove it from this album

**[⬆ back to top](#table-of-contents)**<br /><br />



### Reveal detail as needed

It's not necessary to describe every detail in the first interaction. Reveal increasing detail about features as the user explores them and needs the information.
  
Good | Avoid
---- | -----
Remove downloaded book? | Are you sure you want to remove this downloaded book? You won’t be able to access it unless you’re online.

**[⬆ back to top](#table-of-contents)**<br /><br />
  
  
  
### Never say "never"

Avoid “never” and other absolutes.

Good | Avoid
---- | -----
Your email address isn't shared | We'll never share your email address

**[⬆ back to top](#table-of-contents)**<br /><br />
  
  
  
### Text for buttons and related elements


Button | Usage
------ | -----
Add | Adds an item to a collection
Back | Allows multi-step processes
Back to top | Scrolls to the top of the page
Cancel | Cancels an action
Collapse | Collapses a collection of items in a view
Delete | Deletes an existing item
Discard | Cancels an action and deletes a current, unsaved work item
Dismiss | Causes a message or dialog to disappear without any consequences
Done | Confirms the completion of a multi-step process
Download | Downloads an existing, saved item to their local machine
Edit | Allows the user to an existing, saved item
Expand | Expands a collection of items in a view
Export | Allows the user to bundle and export an item in a specific format to their local machine
Help & feedback | Opens the support section of the website
Got it | Causes a message or dialog to disappear without any consequences (similar to OK)
Learn more | Takes the user to additional content
Manage | Allows the user to edit or delete an existing, saved item
Next | Takes the user to the next step of a multi-step process
No thanks | Allows a user to decline 
Not now | Let’s a user postpone an action or decision. Use only when the call to action in the dialog is essential to the functionality of the product, for legal reasons, or for another urgent reason.<br />*Warning*: Do not use “Not now” as a mechanism to avoid providing a “No thanks” option.  
OK | Allows the user to confirm an action that’s relevant to the task at hand
Remove | Removes an existing item from a collection of items
Search | Locates an item in a given context
Sign in | Confirms an authenticates action for a user
Sign out | Confirms a logout action for a user
Skip | Gives the user a way to avoid an interruption and proceed with a task


Good | Avoid
---- | -----
Add | New
Back | Previous, Go back
Cancel | Nevermind
Delete | Destroy
Done | Save, Save changes, Finish, Submit
Next | Continue, Proceed, Forward
No thanks | No, Decline
Not now | No
OK | Ok, Okay, Close
Register | Create account
Sign in | Login, Log in
Sign out | Logout, Log out
  
**[⬆ back to top](#table-of-contents)**<br /><br />
  
  
  
  
## Tone 


### Be friendly, respectful and focus on the user

Your app’s text should complement its design: intuitive, efficient, casual, and trustworthy.

Good | Avoid
---- | -----
**MyApp isn’t responding**<br />Do you want to close it? | **Sorry!**<br />Activity in MyAppActivity (in the MyApp app) is not responding

**[⬆ back to top](#table-of-contents)**<br /><br />



### Be humble

Reveal what a feature does, without bragging or over-promising.

Good | Avoid
---- | -----
All your savings in one place | Great deals at places you’ll love
More restaurant reviews | All restaurant reviews

**[⬆ back to top](#table-of-contents)**<br /><br />


### Be inviting

Focus on the benefits of each feature. Omit implementation details, caveats, and restrictions when features are introduced.

Good | Avoid
---- | -----
To save power, switch Location mode to Battery saving mode | Manually control GPS to prevent other apps from using it

**[⬆ back to top](#table-of-contents)**<br /><br />


### Be positive

Present information in a positive light: it’s reassuring.

Good | Avoid
---- | -----
Use 24 characters or fewer for file names | Your file name must be less than 25 characters
Try again | The action failed

**[⬆ back to top](#table-of-contents)**<br /><br />



### Be essential

Communicate essential details, so that users can focus on their own tasks. Sometimes the most effective UI contains no text at all.

Good | Avoid
---- | -----
**Processing...**<br />We're contacting PayPal. This can take up to five minutes. | **Processing...**<br />We need to communicate with Paypal servers to process your order. This may take up to five minutes.

**[⬆ back to top](#table-of-contents)**<br /><br />




## Capitalization

Coming soon!

**[⬆ back to top](#table-of-contents)**<br /><br />




## Punctuation

Coming soon!

**[⬆ back to top](#table-of-contents)**<br /><br />
