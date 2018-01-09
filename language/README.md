# Travis' Web Language Style Guide

*My approach to writing clear, concise web content*

## Table of Contents

  1. [Language](#language)
      1. [Addressing users](#addressing-users)
      1. [Avoid the pronoun "we"](#avoid-the-pronoun-we)
      1. [Be concise](#be-concise)
      1. [Write in the present](#write-in-the-present)
      1. [Write simply and directly](#write-simply-and-directly)
      1. [Text for buttons and related elements](#text-for-buttons-and-related-elements)
      1. [Write for all levels of readers](#write-for-all-levels-of-readers)
      1. [Use consistent words in all parts of a feature](#use-consistent-words-in-all-parts-of-a-feature)
      1. ["1, 2, 3", not "one, two, three"](#1-2-3-not-one-two-three)
      1. [Begin with the objective](#begin-with-the-objective)
      1. [Reveal detail as needed](#reveal-detail-as-needed)
      1. [Never say "never"](#never-say-never)
  1. [Tone](#tone)
  1. [Capitalization](#capitalization)
  1. [Punctuation](#punctuation)




## Language


### Addressing users

- Your UI should address the user using either:

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


- Avoid mixing "me"/"my" with "you"/"your.”

  > Why? It can cause confusion to see both forms of addressing the user in the same context.

  ```
  /* avoid */
  Change your preferences in My Account
  ```
 
**[⬆ back to top](#table-of-contents)**

  
  
### Avoid the pronoun "we"


- Focus on the user and what they can do with your app, rather than what you or your app is doing for the user.

  Good | Avoid
  ---- | -----
  Get started with these popular posts | To get you started, we’re showing you the most popular posts this week.
  
  
  - **Note:** One exception is when a person takes an action for a user, such as reviewing an appeal or responding to a suggestion. Here, the use of “we” is appropriate.
  
    Good | Avoid
    ---- | -----
    We’ll review your appeal and respond within a few days | Your appeal will be reviewed, and you will receive a response within a few days
    
**[⬆ back to top](#table-of-contents)**
    
    
### Be concise

- Write in small, scannable segments to facilitate navigation and discovery.

  Good | Avoid
  ---- | -----
  Send money to anyone in the US who has an email address. It’s fast, easy, and free. | Send (and receive) money with friends and family in the US with an email address. It’s a two-step process with little-to-no latency and there aren’t any charges for the recipients of the money.


- Keep your sentences and phrases short, with as few concepts as possible.

  Good | Avoid
  ---- | -----
  Read the instructions that came with your phone | Consult the documentation that came with your phone for further instructions

**[⬆ back to top](#table-of-contents)**


### Write in the present

- Use the present tense to describe product behavior. 
- Avoid using the future tense to describe the way a product always acts.
- When you need to write in the past or future, use simple verb forms.

**[⬆ back to top](#table-of-contents)**



### Write simply and directly

- Use simple, direct language that is easy for users to understand.

  Common introductory phrases may be omitted.
  
  Good | Avoid
  ---- | -----
  Save changes? | Would you like to save your changes?
  Message sent | Message has been sent
  Register to rate | You must register before you can rate this pharmacy
 
**[⬆ back to top](#table-of-contents)**

  
### Write for all levels of readers

- Pick common words that are clearly and easily understandable to both beginning and advanced English readers.

  Good | Avoid
  ---- | -----
  Turn on Location History | Enable Location History
  
  
- Avoid industry-specific terminology or names invented for UI features.

  Good | Avoid
  ---- | -----
  Preparing video…  | Buffering…
  “Exporting to PDF” isn’t supported on your phone | "Exporting to PDF" is only supported on dual-core devices

  
- Refer users to the labels on UI elements, not the type of element (such as menu or button).

  Good | Avoid
  ---- | -----
  Click **Continue** | Click the Continue button
  
**[⬆ back to top](#table-of-contents)**
  
  
  
### Use consistent words in all parts of a feature

  - Use verbs in a consistent manner across the description of an action.
  
  Good | Avoid
  ---- | -----
  Remove photo | Delete photo
  Remove photo? | Remove photo from page?
  
**[⬆ back to top](#table-of-contents)**
  
  
### "1, 2, 3", not "one, two, three"

  - Use numerals in place of words for numbers.
  
  One exception is when mixing uses of numbers, such as "Enter two 3s."
  
  > Why? Using numerals promotes scannability.
  
  Good | Avoid
  ---- | -----
  You have 3 messages | You have three messages
  
**[⬆ back to top](#table-of-contents)**
  

### Begin with the objective

  - If a sentence describes both an objective and the action needed to achieve that objective, start the sentence with the objective.
  
  > Why? Starting a sentence with the objective sets the user's expectation early and promotes scannability.
  
  Good | Avoid
  ---- | -----
  To remove a photo from this album, drag it to the trash | Drag a photo to the trash to remove it from this album

**[⬆ back to top](#table-of-contents)**


### Reveal detail as needed

  - It's not necessary to describe every detail in the first interaction. Reveal increasing detail about features as the user explores them and needs the information.
  
  Good | Avoid
  ---- | -----
  Remove downloaded book? | Are you sure you want to remove this downloaded book? You won’t be able to access it unless you’re online.
  
**[⬆ back to top](#table-of-contents)**
  
  
### Never say "never"

  - Avoid “never” and other absolutes.
  
  Good | Avoid
  ---- | -----
  Your email address isn't shared | We'll never share your email address

**[⬆ back to top](#table-of-contents)**
  
  
### Text for buttons and related elements


Button | Usage
------ | -----
Back | Allows multi-step processes
Cancel | Cancels an action
Dismiss | Causes a message or dialog to disappear without any consequences
Done | Confirms the completion of a multi-step process
OK | Allows the user to confirm an action that’s relevant to the task at hand
Got it | Causes a message or dialog to disappear without any consequences (similar to OK)
Learn more | Takes the user to additional content
Next | Takes the user to the next step of a multi-step process
No thanks | Allows a user to decline 
Not now | Let’s a user postpone an action or decision. Use only when the call to action in the dialog is essential to the functionality of the product, for legal reasons, or for another urgent reason.<br /><br />**Warning**: Do not use “Not now” as a mechanism to avoid providing a “No thanks” option.  
Skip | Gives the user a way to avoid an interruption and proceed with a task
  
**[⬆ back to top](#table-of-contents)**
  
  
  
  
