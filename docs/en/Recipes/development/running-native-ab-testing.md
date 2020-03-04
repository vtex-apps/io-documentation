---
title: Running native A/B testing
description: "Our native A/B testing solution is designed entirely for ecommerce businesses seeking to optimize their conversion by measuring and comparing traffic between a variant workspace and the master."
date: "19/08/2019"
tags: ["ab", "test", "a/b", "running", "store", "testing", "workspace", "native"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/store/running-native-ab-testing.md"
---

# Running native A/B testing

## Introduction

Our native A/B testing solution is designed entirely for ecommerce businesses seeking to optimize their conversion by measuring and comparing traffic between a variant workspace and the master.

![ab-testing](https://user-images.githubusercontent.com/52087100/64129197-21a62780-cd91-11e9-86f9-1ec8a3d2e2c8.png)

Follow the next steps and learn more about the installation and execution of an A/B testing running entirely on the VTEX IO platform.  

## Step by step

1. Start off by implementing and saving the changes you want to test in a chosen workspace. Then, do not forget to put it in the **production mode**. 
2. Open your terminal and authenticating yourself by running `vtex login`.
3. Then, you must install our A/B testing app on the desired account master workspace. In order to do so, simply run `vtex install vtex.ab-tester`. 

<div class="alert alert-info">
 You can run <code>vtex ls</code> to make sure that you have <code>vtex.ab-tester</code> successfully installed in the <code>master</code> workspace. 
</div>

4. While in `master`, you can run `vtex workspace abtest start` to become a production workspace list available for you. Then, you should choose which workspace from that list will be the one compared to master. 

![ab-testing-step4](https://user-images.githubusercontent.com/52087100/64129583-50bd9880-cd93-11e9-8b80-f1fe4cad943b.png)

At any moment, we can run the `vtex workspace abtest status` command to see the live results: 

![ab-testing-step5](https://user-images.githubusercontent.com/52087100/64129599-69c64980-cd93-11e9-85fd-575665fbf532.png)

5.	You can run the `vtex workspace abtest finish` command in `master` whenever you feel that you already had enough testing or if a winner was already detected. 

Then, a list of all workspaces being tested  by the `vtex.ab-tester` app will show up and you should indicate which one should be ended. 

![ab-testing-step6](https://user-images.githubusercontent.com/52087100/64129622-a7c36d80-cd93-11e9-9b77-9a0bae552439.png)

<div class="alert alert-warning">
By finishing the test, you will only be ending the test on the select workspace. <strong>It will not promote any workspace to master. You must do that yourself.</strong> If you've built an A/B Test with other workspaces you must end them manually as well.
</div>
