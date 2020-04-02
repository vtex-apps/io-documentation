---
title: Running native A/B tests
description: "Our native A/B testing solution is designed entirely for ecommerce businesses seeking to optimize their conversion by measuring and comparing traffic between a variant workspace and the master."
date: "19/08/2019"
tags: ["ab", "test", "a/b", "running", "store", "testing", "workspace", "native"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/store/running-native-ab-testing.md"
---

# Running native A/B tests

## Introduction
  
An A/B test compares website versions of your choosing to uncover, based on a single metric, **which version is best** (having the highest return rate) for your business needs. 

Suppose that you wanted to give your store a new landing page. In order to avoid any unpleasant surprises that may arise from the change, this decision should be taken based on a metric that can be quantified to show the change's proven results.

The problem can be easily handled by running a A/B test. The VTEX IO native A/B testing solution is designed entirely for **ecommerce businesses** seeking to optimize their conversion by measuring and comparing traffic between 2 different workspaces: a variant production workspace and the master workspace.

![ab-testing](https://user-images.githubusercontent.com/52087100/64129197-21a62780-cd91-11e9-86f9-1ec8a3d2e2c8.png)

Follow the steps below to learn more about the installation and execution of an A/B test running entirely on the VTEX IO platform:

## Step 1 - Enabling A/B testing

1. In your terminal and using the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference), authenticate yourself in the desired account by running `vtex login {accountName}`;
2. Once logged into the desired account, [create a Production workspace](https://vtex.io/docs/recipes/development/creating-a-production-workspace) and run the command `vtex use {productionWorkspaceName}` in order to start working in it;
3. Perform the changes you want to test, such as the installation of a new app, for example, in the production workspace you are working in. Don't forget to save your changes;
4. Run the `vtex use master` command in order to change the Production workspace you are working in to the Master one;
5. Install the VTEX A/B tester app in the Master workspace in order to enable A/B testing on the site by running `vtex install vtex.ab-tester`;

<div class="alert alert-info">
You can run <code>vtex ls</code> to make sure that you have successfully installed <code>vtex.ab-tester</code>  in the <code>master</code> workspace.
</div>

6. While still working in the master workspace, run `vtex workspace abtest start` to choose a production workspace from the list made available for you. The chosen workspace will be compared to the Master;
  
![ab-testing-step4](https://user-images.githubusercontent.com/52087100/64129583-50bd9880-cd93-11e9-8b80-f1fe4cad943b.png)

7. Select the production workspace in which you've already performed all desired changes and then agree to proceed.

<div class="alert alert-info">
<strong>You may simultaneously run more than one A/B test in VTEX IO</strong>, thereby comparing two or more  workspaces with the master workspace. You will just have to do it separately. But be aware: if the traffic has been manually set, it will be divided equally between all the production workspaces currently being tested. For example: a first A/B test is started between Master and WorkspaceA, diverting 90% of traffic to the former and only 10% to the latter. If a new A/B test is then configured, the production workspace that will be tested and WorkspaceA will only have 5% of store's traffic each.
</div>

## Step 2 - Configuring the traffic and time

By agreeing to proceed with the test, Toolbelt will inquire about the user **traffic bandwidth** in each workspace (`What's the proportion of traffic initially directed to the master workspace?`) as well as the **test time frame** (`What's the amount of time respecting the restriction?`).

Your A/B test can be configured to work in two distinct ways: automatically and manually.

### Automatically

To automatically proceed with the A/B test, letting VTEX IO take over the test control and **automatically splitting site traffic between workspaces**, you should do the following: 

1. Answer with any whole number between 0 and 10000 when asked `What's the proportion of traffic initially directed to workspace master?` ;
2. Set the answer to `What's the amount of time respecting the restriction?` as `0`.

In this scenario, VTEX IO will initially have 50% of your store's traffic stay with the master workspace while migrating the other 50% to the production workspace that's being tested.

During the test, **the platform will automatically balance traffic** every 3 minutes according to the conversion rate that arises. This means that **the workspace with less conversion will progressively relay its traffic to the workspace with more conversion**. 

<div class="alert alert-warning">
Notice that the test, although automatic, will not end by itself. It's important to evaluate and interpret the test status daily.
</div>

### Manually 

If you opt to manually define traffic and time frame, you should:

1. Answer with `9000` to `What's the proportion of traffic initially directed to workspace master?` in order to set the traffic proportion of 90%;

<div class="alert alert-warning">
To not break your store and to promote the changes from the new workspace in the safest way possible, it is strongly recommended that percentage value of traffic dedicated to the master workspace be <code>90%</code>, leaving just 10% of the store's total traffic for the production workspace being tested.
</div>

2. Give an answer in hours to the following question: `What's the amount of time respecting the restriction?`.

<div class="alert alert-warning">
 You should <strong>preferably configure you A/B test for a day a week</strong>, answering the question in step 2 with a value of <code>24</code>. It's important for the test to be able to extract the maximum amount of data during intense operational periods and that it doesn't overextend to be deleterious to users navigating the workspace with the poorer experience.
</div>

## Step 3 - Interpreting the test results

Any time during the A/B test, you can run the `vtex workspace abtest status` command to follow the results live.

![ab-testing-step5](https://user-images.githubusercontent.com/52087100/64129599-69c64980-cd93-11e9-85fd-575665fbf532.png)

<div class="alert alert-info">
<strong>The workspaces are not frozen and can continue to receive updates during the period in which they undergo A/B testing.</strong> But keep in mind that the less changes are made to both workspaces, the more relevant your results will be, helping you come to the correct decision afterwards.
</div>

Before completing your A/B test, it's important to understand the comparative and the final results from both workspaces.

### Comparative results

- **Conversion** - Conversion rate percentage that each workspace displayed during the test;
- **Expected Loss** - Expected conversion loss percentage for the store if the lower conversion rate workspace is chosen as winner (according to the **Conversion** results);
- **N. of Sessions** - Total number of sessions for each workspace since the beginning of the test;
- **N. of Sessions (last 24hrs)** - Number of sessions for each workspace during the test's last 24hrs.

### Final results

- **Start Date** - Date and time for the beginning of the test;
- **Running Time** - Test duration;
- **Probability B beats A** - Probability, in percentage points, that the production workspace is better for your store than the current master workspace. This calculation is based on the number of sessions and number of sessions with completed sales. Notice: if this metric's result is greater than `10%`, the production workspace is ble to become the winner;
- **Winner** - Workspace you chose as winner. 

<div class="alert alert-warning">
The main results of the A/B test are aimed for scenarios where store traffic was automatically directed by the platform. While you can and should use A/B tests even if you manually direct the traffic, bear in mind that the numbers behind each result reflect an automatic segmentation according to each workspace experience.
</div>

**The best way to validate your A/B test workspace winner is to set, according to your store operation size, a maximum conversion loss value.**

For example: when starting your test, you can set `0,0001%` as the conversion loss maximum value. The decision to end the test and declare a winner will therefore be taken when either of the workspaces reaches an `Expect Loss` result greater than `0,0001%`.

## Step 4 - Finishing the A/B test

Run the `vtex workspace abtest finish` command in `master` if your test has already reached the time frame you've manually set for it or if feel that a winner was already detected following as interpretation recommended in step 3.

<div class="alert alert-warning">
 If you have set a predefined time frame of <code>24</code> hours to run your A/B for example, it's important that you pay attention to the test during this entire period. Although the platform continues to automatically redistribute traffic according to how each workspace is behaving after the set time frame, overseeing the test is fundamental to its success.
</div>

When running the command, a list of all workspaces being tested by the `vtex.ab-tester` app in Master will show up. Select the one which should end. For example:

![ab-testing-step6](https://user-images.githubusercontent.com/52087100/64129622-a7c36d80-cd93-11e9-9b77-9a0bae552439.png)

<div class="alert alert-warning">
Note that you will only be ending the test on the selected workspace. <strong>It will not promote any workspace to master<strong>. You must do that by yourself if you want to make the new configurations public for all users.
</div>
