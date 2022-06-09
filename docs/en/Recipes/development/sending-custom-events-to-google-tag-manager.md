# Sending custom events to Google Tag Manager

This guide will teach you how to send custom events to [Google Tag Manager (GTM)](https://tagmanager.google.com/). Custom events can track website interactions that aren't supported by GTM's standard methods. For example, you can set up a custom event to notify GTM that a user has clicked on a particular button.

>ℹ️ For standard Google Tag Manager events and Universal Analytics Enhanced Ecommerce features, please consider using the [Google Tag Manager Pixel app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-google-tag-manager).


## Step by step 

### Step 1 - Tracking a custom event

To notify GTM about a specific action performed on your website, you must send an event to the GTM `dataLayer` whenever that action happens. The GTM `dataLayer` is a JavaScript object that passes information from your website to your GTM container.

1. Open your project in any code editor of your preference.
2. Create a new function to push event data to GTM's `dataLayer` using the following code as a reference.

   ```tsx
   window.dataLayer = window.dataLayer || [];
   export default function push(event: any) {
     window.dataLayer.push(event);
   }
   ```

>ℹ️ Remember to make the `dataLayer` variable available in the `window` object before saving event data in it.
        
3. Go to the code line where the event happens and call your function, providing your event data as an argument. For example:

    ```tsx
    const data = e.data

    push({
        event: 'categoryView',
        categoryId: data.category?.id,
    })
    ```
    
4. Save and deploy your changes.

### Step 2 - Testing the event

1. Access your workspace in the [GTM console](https://tagmanager.google.com/).
2. Click **Preview**.
3. Test if the event trigger is working by performing the action associated with your event on the window opened by **Preview**.

### Step 3 - Creating an event trigger

Once you've validated that the `dataLayer` event is working properly, you'll need to set up a trigger so GTM can perform a specific action when your event is registered.

1. Create a custom event trigger using the [GTM console](https://tagmanager.google.com/). Please refer to [this guide](https://support.google.com/tagmanager/answer/7679219?hl=en) for more information. Notice that you must enter the exact name of your data layer `event` in the **Event name** field. Considering our example, that would be `categoryView`. 
2. If applicable, create new variables of the **Data Layer Variable** type. Please refer to [this guide](https://support.google.com/tagmanager/topic/9125128?hl=en&ref_topic=7683268) for more information. Notice that you must set up new Data Layer variables only if you are sending additional information to your custom event. Considering our example, that would be `categoryId`. 
