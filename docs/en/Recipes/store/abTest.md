---
title: Running A/B tests
description: "Our native A/B testing solution is designed entirely for ecommerce businesses seeking to optimize their conversion by measuring and comparing traffic between a variant workspace and the master."
date: "19/08/2019"
tags: ["ab", "test", "a/b", "store", "testing", "workspace"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/abTest.md"
---

# Running A/B tests


Our native A/B testing solution is designed entirely for ecommerce businesses seeking to optimize their conversion by measuring and comparing traffic between a variant workspace and the master.

This tutorial aims to cover the installation and execution of an A/B testing running entirely on the VTEX IO platform.  


Start off by implementing and saving the changes you want to test in a chosen workspace. Then, do not forget to put it in the production mode. 

Open your terminal and authenticating yourself by running `vtex login`

3. 	Then, you must install our A/B testing app on the desired account master workspace. In order to do so, simply run `vtex install vtex.ab-tester`   

You can run `vtex ls` to make sure that you have `vtex.ab-tester` successfully installed in the `master` workspace. 

4. 	While in `master`, you can run `vtex workspace abtest start` to become a [production workspace](resource de workspaces) list available for you. Then, you should choose which workspace from that list will be the one compared to master. 




At any moment, we can run:
 ```
vtex workspace abtest status
``` 
To see our live results:



5.	You can run:
 ```
vtex workspace abtest finish
``` 
In `master` whenever you feel that you already had enough testing or if a winner was already detected. Then, a list of all workspaces being tested  by the `vtex.ab-tester` app will show up and you should indicate which one should be ended. 


**Notice:** by finishing the test, you will only be ending the test on the select workspace. **It will not promote any workspace to master.  You must do that yourself.** If you've built an A/B Test with other workspaces you must end them manually as well.
