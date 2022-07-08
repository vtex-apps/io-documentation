---
title: Running native A/B tests
description: "Our native A/B testing solution is designed entirely for ecommerce businesses seeking to optimize their conversion by measuring and comparing traffic between a variant workspace and the master."
date: "19/08/2019"
tags: ["ab", "test", "a/b", "running", "store", "testing", "workspace", "native"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/store/running-native-ab-testing.md"
---

# Running A/B tests
  
An A/B test compares traffic between two workspaces: the master and a production workspace, and reveals which version is best for your business needs.

For example, suppose you want to update your store's landing page. To confirm the beneficial results of your changes, you can run an A/B test and base your decisions on quantitative metrics.

To execute an A/B test, you can use the VTEX IO CLI or the [A/B Tester Admin app](https://developers.vtex.com/vtex-developer-docs/docs/vtexarg-abtester). For more information, please refer to the following sections.

![ab-testing](https://user-images.githubusercontent.com/52087100/64129197-21a62780-cd91-11e9-86f9-1ec8a3d2e2c8.png)


## Running A/B tests via the Admin
The A/B Tester app allows you to run A/B tests via Admin. To use the app, first you need to install it in your account:

1. Open the terminal and use the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) to log in to the desired account.

2. Install the A/B Tester app in the `master` workspace to enable A/B testing on your store website by running:

  ```
  vtex use master
  vtex install vtex.ab-tester
  ```

3. Type `y` to confirm that you want to install the app in the `master` workspace. 

4. Install the **A/B Tester Admin app** in the `master` workspace by running the following:

  ```
  vtex install vtexarg.abtester
  ```
  
5. Type `y` to confirm the installation.
6. Now, access the Admin and go to Installed Apps > AB Tester. 
7. Create A/B tests, compare and finish tests, referring to the [A/B Tester Admin app documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtexarg-abtester#usage).

## Running A/B tests via the VTEX IO CLI

### Step 1 - Enabling A/B testing

1. Open the terminal and use the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) to log in to the desired account:

  ```
  vtex login {accountName}
  ````

2. [Create and switch to a Production workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace) by running the following command:

  ```
  vtex use {workspaceName} --production
  ```

3. Perform the changes you want to test in the production workspace you are using. For example, install or edit an app.

  > ⚠️ If your store uses the [Checkout UI Custom](https://developers.vtex.com/vtex-developer-docs/docs/vtex-checkout-ui-custom-v0) app, you must first publish its configurations on your new production workspace. Otherwise, you might experience undesired consequences, such as losing the Checkout custom Javascript code and styles.

4. Switch to the master workspace.

  ```
  vtex use master
  ````

5. Install the VTEX A/B tester app in the Master workspace to enable A/B testing on your store website by running:

  ```
  vtex install vtex.ab-tester
  ```

  > ℹ️ You can run `vtex ls` to make sure that you have successfully installed `vtex.ab-tester` in the `master` workspace.

6. Run the following command in the master workspace.

  ```
  vtex workspace abtest start
  ```

  ![ab-testing-step4](https://user-images.githubusercontent.com/52087100/64129583-50bd9880-cd93-11e9-8b80-f1fe4cad943b.png)

7. Select the production workspace you want to use for comparison with the master and agree to proceed.

### Step 2 - Configuring the traffic and time

By agreeing to proceed with the test, you will need to answer the two following questions:

1. `What's the proportion of traffic initially directed to the master workspace?`. You must answer this question with any whole number between 0 and 10000. For example, if you answer `9000`, you'll set 90% of the traffic to the master workspace.

  > ℹ️ To promote the changes from your production workspace in the safest way possible, we strongly recommend that you leave 90% of traffic dedicated to the master and the other 10% to the production workspace being tested.

2. `What's the amount of time respecting the restriction?`. This is the amount of time (in hours) during which the traffic proportion stated in the previous question remains constant. After this period, the A/B testing system automatically balances the traffic proportions, sending more traffic to the best-performing workspace. There are two possible answers to this question:
  - **Answer `0` to automatically proceed with the A/B test.** In this case, VTEX IO will automatically split your website traffic between workspaces, routing 50% of your store's traffic to the master and the other 50% to the production workspace being tested. Following that, the platform will automatically balance traffic every three minutes based on the conversion rates. This means that traffic will be gradually routed from the workspace with the lowest conversion rate to the workspace with the highest conversion rate. It's important to note that the test does not end on its own. We also suggest that you evaluate the test results on a daily basis.
  - **Answer with the number of hours you want to keep constant the proportion of traffic previously specified.** During peak operational periods, it's critical for the test to extract as much data as possible. At the same time, the test shouldn't overextend and end up being harmful to users who are navigating the workspace with the poorest performance.
  
  > ℹ️ You can run many A/B tests simultaneously by comparing two or more workspaces to the master individually. However, if you opt to set up the traffic manually, the A/B test will distribute the traffic evenly among all production workspaces being A/B tested. For example, suppose you started an A/B test between workspace A and master, routing 90% of traffic to the former and 10% to the latter. If you run a new A/B test between workspace B and the master, each production workspace, A and B, will only receive 5% of the store's traffic.
 
### Step 3 - Interpreting the test results

Any time during the A/B test, you can run the following command to check the live results:

```
vtex workspace abtest status
```
 
![ab-testing-step5](https://user-images.githubusercontent.com/52087100/64129599-69c64980-cd93-11e9-85fd-575665fbf532.png)

If desired, you can still update the workspaces being used in the A/B test. However, notice that the fewer changes made to these workspaces, the more accurate your results will be.

Before completing your A/B test, it's important to understand both workspaces' comparative and final results.

#### Comparative results

- **Conversion** - Conversion rate percentage that each workspace displayed during the test.
- **Expected Loss** - Expected conversion loss percentage for the store if the lower conversion rate workspace is chosen as the winner (according to the **Conversion** results).
- **N. of Sessions** - Total number of sessions for each workspace since the beginning of the test.
- **N. of Sessions (last 24hrs)** - Number of sessions for each workspace during the test's last 24hrs.

#### Final results

- **Start Date** - Date and time for the beginning of the test.
- **Running Time** - Test duration.
- **Probability B beats A** - Probability, in percentage points, that the production workspace is better for your store than the current master workspace. This calculation is based on the number of sessions and the number of sessions with completed sales. Notice: if the result of these metrics is greater than `10%`, the production workspace is able to become the winner.
- **Winner** - Workspace you chose as the winner. 

> ⚠️ The main results of the A/B test are aimed at scenarios where the platform automatically directed store traffic. While you can and should use A/B tests even if you manually direct the traffic, bear in mind that the numbers behind each result reflect an automatic segmentation according to each workspace experience.

**The best way to validate your A/B test workspace winner is to set a maximum conversion loss value according to your store operation size.**

For example, you can set a maximum conversion loss of `0,0001%` when starting your test. Then, when either workspace achieves an `Expect Loss` result greater than `0,0001%`, you should end the test and declare a winner.

### Step 4 - Finishing the A/B test

If your test has already reached the time frame you've manually set for it, or if you have already detected a winner during Step 3, run the following command in Master to finish the test.

```
vtex workspace abtest finish
```

> ⚠️ If you have manually set a predefined time frame to run your A/B test, it's important that you pay attention to the test during this entire period. Although the platform automatically redistributes traffic according to how each workspace is behaving after the set time frame, overseeing the test is fundamental to its success.

When running the command, a list of all workspaces being tested by the `vtex.ab-tester` app in Master will show up. Select the one which should end. For example:

![ab-testing-step6](https://user-images.githubusercontent.com/52087100/64129622-a7c36d80-cd93-11e9-9b77-9a0bae552439.png)

> ⚠️ Note that you will only end the test on the selected workspace. **It will not promote any workspace to master**. You must do that by yourself to make the new configurations public for all users.

