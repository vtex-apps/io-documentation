# How to submit an app in the app store

## Glossary

**App:** specific software implemented using VTEX IO to provide some additional resource to the VTEX platform, be it some integration with external service, new technical or layout functionality.

**App Store or VTEX App Store:** marketplace for VTEX-approved plug & play solutions for users of the VTEX Platform.

**Network Partner Program:** the main benefit is to have access to a VTEX account, in order to be able to test and develop new apps and to have access to tech support from VTEX partner team. By default this program requires a monthly fee, but for the cases of only app development partners for App Store, there are special conditions, without charging the fee for at least 6 months. See more about the Partner Program ([https://network.vtex.com/terms_of_use](https://network.vtex.com/terms_of_use)).

## Resume

- 1 - Share your interest

    [https://forms.gle/wpkXMxgSfCXwMPbs8](https://forms.gle/wpkXMxgSfCXwMPbs8)

- 2 - Sign a commercial agreement
- 3 - Submit your App (app-store@vtex.com.br)

## Steps

### 1 - Share your interest:

Fill out the following form to **share your interest** in publishing your application / integration on the VTEX App Store: [https://forms.gle/wpkXMxgSfCXwMPbs8](https://forms.gle/wpkXMxgSfCXwMPbs8)

This will help us to ensure the best approach to partners and organization of publication demands.

### 2 - Sign a commercial agreement:

If the form was filled out and the internal team agrees that the application makes sense to exist on the VTEX App Store, it is necessary to sign a commercial contract for distribution of the application and sign up for the **Network Partner Program**, if you are not already registered.

![https://github.com/manoel-gumes/images/blob/master/Flow.png](https://github.com/manoel-gumes/images/blob/master/Flow.png)

### 3 - Submit your App:

Submit the app's source code and all necessary metadata to be evaluated by the app store verification team.

### Validation Steps

The homologation process must ensure that the launched applications have a clear value proposition, are safe, stable, and aligned with VTEX's intentions as a brand and business when ensuring compliance with business, design and technology standards.

- Business validation - the app has a business model with viable and sustainable pricing and accomplishes what it proposes.
- UX validation - The App offers a satisfactory user experience, following VTEX styleguide (tachyons is required if you are creating a front end block).
- Security and performace validation - the app has efficient and safe performance.

### Validation assets:

Need to be sent to the VTEX App Store team throught this email: **app-store@vtex.com.br**.

- Zip file of the exact version that you want to submit, this version should be published in your very own account, and you should send also a link of an account with the app istalled and set up. In addition to the source code, the zip file must contain the following:
    - **Permissions:**

        It is necessary to inform the list with the VTEX APIs and any external links that your app will access. The link to your app's permissions must be registered in the manifest.json file, in the field: "billingOptions" → "policies".

    - **Terms of use:**

        The rules for using the App must be described, and it is in the partner's interest to have this type of record to guard against legal risks. Through this instrument, the partner can define the situations in which he will be responsible and for which situations he cannot be responsible for failures. It is important to define exactly the meaning of the terms used and to properly delimit the scope of the service that the app offers to avoid any future complaints.

        The link to the terms of use for your app must be registered in the file manifest.json, in the field: "billingOptions" → "termsURL".

        ```json
        "billingOptions": {
            "termsURL": "{Put the URL here}",
        		...
          },
        ```

    - **Support:**

        You must provide at least one contact for support, it can be an email and/or a link to your company's support. The links must be registered in the file manifest.json, in the field: "billingOptions" → "support".

        ```json
        "billingOptions": {
            "termsURL": "{Put the URL here}",
            "support": {
              "url": "{Put the URL here}"
            },
          },
        ```

    - **Price:**

        It is necessary to configure the pricing in the manifest.json file, in the field: "billingOptions" → "policies"

        You can see the details ot: [http://help.vtex.com/pt/tutorial/modelos-de-cobranca-de-apps](http://help.vtex.com/pt/tutorial/modelos-de-cobranca-de-apps).

        ```json
        "billingOptions": {
            "termsURL": "{Put the URL here}",
            "support": {
              "url": "{Put the URL here}"
            },
            "policies": [
              {
                "currency": "BRL",
                "billing": {
                  "taxClassification": "software",
                  "invoiceProvider": "vtex",
                  "items": [
                    {
                      "itemCurrency": "BRL",
                      "calculatedByMetricUnit": {
                        "metricId": "metricsExample",
                        "metricName": "Metrics Example",
                        "ranges": [
                          {
                            "exclusiveFrom": 0,
                            "multiplier": 1
                          }
                        ],
                        "metricsRoute": "{Put the URL here}"
                      }
                    }
                  ]
                }
              }
            ]
          },
        ```

    - **Name:**

        The name of the app doesn't necessarily need to indicate directly what it does. It may be a short, playful name that sells your proposal well. Ideally, avoid very technical names that are hard to remember.

        In the file, the name must be in the txt file (title.txt) in the "public" → "metadata" → "en-US" / "es-AR" / "pt-BR" folders. The name must be compatible with the folder of the chosen language.

    - **Short description:**

        The description of the app must be very objective, with a maximum of three sentences, saying what your app is and the main benefit / gain for the customer who will buy it. It is what will lead the user to buy or be interested in knowing more about the solution.

        In the file, the short description must be in the txt file (short_description.txt) in the "public" → "metadata" → "en-US" / "es-AR" / "pt-BR" folders. The texts must be compatible with the folder of the chosen language.

    - **Full description:**

        The details of the app should contain all the necessary information for your customer such as:

        **About:**
        What is your app, what does it propose to do, what are the advantages for the shopkeeper?

        **Features:**
        What are its main features? Can divide into topics.

        **How to set up and use:**
        How do I configure?
        Technical implementation / configuration details
        How I use?

        In the file, the full description must be in the txt file (full_description.txt) in the "public" → "metadata" → "en-US" / "es-AR" / "pt-BR" folders. The texts must be compatible with the folder of the chosen language.

        You can use the Markdown syntax, example:

        ```markdown
        ## About

        The app VTEX Shopping Ads syncs your products in VTEX to Google Merchant Center (GMC) and allows you to create and manage Google Shopping Campaigns directly from the VTEX platform. This way, you can, simply and quickly, increase the traffic to your site.

        ## Functionalities
        - Integration of your VTEX catalog with the Google Merchant Center
        - Creation and management of Google Shopping Smart Campaigns

        ## How to set up
        1 - Check that you are running the latest version of VTEX admin. To do that, check on the bottom of the admin sidebar if there's a link to update the version. If the link is available, do the update.

        2 - Install the app from VTEX App Store.

        3 - After installing the app, locate the ‘Other’ section in your Admin and click on VTEX Shopping Ads. Once you have started the app, follow its initial instructions to set it up and start to run a campaign.

        ## Comments
        - The app is being launched to work only with Brazilian stores that sell in BRL.
        - Billing is done directly by VTEX, so you will receive a unified invoice.
        - More details about how to set up can be found on the following link: https://help.vtex.com/tracks/como-fazer-campanhas-atraves-do-google-shopping-app--47kz5PRQPK0IEaqGqiIuA/1FT4KHCSbGmQCsmUQk286w
        ```

    - **Icon:**

        The app's icon is really important as it creates an identity for your app while also differentiating itself between the others in the App Store. It is also the only place in the VTEX App store where you can visually establish and express your identity.

        The icon must be a **.png** and have a **minimum size of 128 x 128px with 1:1 ratio** and must have a **transparent background.**

        In the file, your icon must be in the "public" → "metadata" folder.

        Do not try to fill the entire space. Try to keep the edges of the icon limited to 75% of the side of the square. Examples:

        ![https://github.com/manoel-gumes/images/blob/master/Icon.png](https://github.com/manoel-gumes/images/blob/master/Icon.png)

    - **Screenshots:**
    Screenshots are important for the customer to visually understand how your app will behave, whether in the admin or in the store itself. Visually supporting all the information written in the “details” section mentioned above.

        In the file, these images must be in the "public" → "metadata" → "en-US" / "es-AR" / "pt-BR" → "screenshots" folder, in png or gif format.

        It is important to remember that the texts in the screenshots must be compatible with the folder of the chosen language.

        ![https://github.com/manoel-gumes/images/blob/master/desktop-01.png](https://github.com/manoel-gumes/images/blob/master/desktop-01.png)

        ![https://github.com/manoel-gumes/images/blob/master/desktop-02.png](https://github.com/manoel-gumes/images/blob/master/desktop-02.png)

        ![https://github.com/manoel-gumes/images/blob/master/desktop-03.png](https://github.com/manoel-gumes/images/blob/master/desktop-03.png)

        Screeshots will be ordered according to their name: screenshot_1_mobile.png, screenshot_2_mobile.png, ... / screenshot_1_desktop.png, screenshot_2_desktop.png, ...
