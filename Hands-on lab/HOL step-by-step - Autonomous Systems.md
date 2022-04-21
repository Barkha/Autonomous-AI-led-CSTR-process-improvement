<div class="MCWHeader1">
Autonomous Systems with Bonsai
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
April 2022
</div>

Information in this document, including URL and other Internet website references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third-party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2022 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Autonomous Systems with Bonsai hands-on lab step-by-step](#autonomous-systems-with-bonsai-hands-on-lab-step-by-step)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Overview](#overview)
  - [Solution architecture](#solution-architecture)
  - [Requirements](#requirements)
  - [Before the hands-on lab](#before-the-hands-on-lab)
 - [Exercise 1: Creating the Brain](#exercise-1-creating-the-brain)
    - [Task 1: Set up Bonsai on Azure](#task-1-set-up-bonsai-on-azure)
    - [Task 2: Creating a Brian](#task-2-creating-a-brain)
    - [Task 3: Adding Inkling Code](#task-3-adding-inkling-code)
 - [Exercise 2: Creating the Simulator in Bonsai](#exercise-2-creating-a-simulator)
    - [Task 1: Create A Simulator](#task-1-create-a-simulator)
    - [Task 2: Connect to Bonsai Brain](#task-2-connect-to-bonsai-brain)
 - [Exercise 3: Assessment and Optimization](#exercise-3-assessment-and-optimization)
    - [Task 1: Training the Brain](#task-1-training-the-brian)
    - [Task 2: Using Assessments](#task-2-using-assessments)
    - [Task 3: Adding additional concepts to optimize](#task-3-adding-additional-concepts-to-optimize)
 - [Exercise 4: Deploying the brain](#exercise-3-deploying-the-brin)
    - [Task 1: Exporting a Brain](#task-1-exporting-a-brian)
- [After the hands-on lab](#after-the-hands-on-lab)
    - [Task 1: Tear down Azure Resources](#task-1-tear-down-azure-resources)

<!-- /TOC -->

# Autonomous Systems with Bonsai hands-on lab step-by-step

## Abstract and learning objectives

In this hands-on lab, you will learn how to implement a solution with a combination of Bonsai Tool Chain and Python simulatorn to optimization is the Continuous Stirred Tank Reactor using  machine teaching and deep reinforcement learning.

At the end of this workshop, you will be better able to implement solutions for autonomous systems with Bonsai Tool Chain in Azure, using Inkling, a Python Simulator, and the Bonsai UI platform.

## Overview

Contoso is world wide leader in gases, chemicals and services. It's main factory creates 60% of the chemicals needed for industry and manufacturing as well as agriculture.

Contos has been going through a digital transformation and is looking to embrace AI and Autonomous systems for it's Chemial processing plant in order to improve both safety and optimize production. One of the primary targets for optimization is the Continuous Stirred Tank Reactor (CSTR). This reactor is essentially a tank that has a stirring apparatus to continuously mix reactants inside and continuously manufacture a chemical product.

One of the concerns regarding this CSTR is that the chemical reaction happening inside is exothermic, meaning it produces heat. As a result, the reactor temperature must be controlled to prevent thermal runaway, when the reactor becomes uncontrollably hot. The CSTR needs to operate under transient and steady state conditions. During continuous steady-state operation, the CSTR is producing a specified product. When the CSTR is starting up or transitioning to produce different products, it is in transient state. During transient state, it is difficult to control the reactor to reach the target concentration of the product while preventing thermal runaway.

## Solution architecture

![Solution architecture diagram illustrating the use of Autonomous Systems with Bonsai.](media/SolutionArchitectureDiagram.png "Desired solution architecture")

## Requirements

1. Microsoft Azure subscription must be pay-as-you-go or MSDN.
   - Trial subscriptions will _not_ work.
   - To complete this lab setup, ensure your account includes the following:
     - Has the [Owner](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) built-in role for the subscription you use.
     - Is a [Member](https://docs.microsoft.com/azure/active-directory/fundamentals/users-default-permissions#member-and-guest-users) user in the Azure AD tenant you use. (Guest users will not have the necessary permissions.)


## Before the hands-on lab

You should follow all steps in the [Before the hands-on lab setup guide](Before%20the%20HOL%20-%20Continuous%20delivery%20in%20Azure%20DevOps.md) *before* performing the Hands-on lab. Pay close attention to product versions, as the version numbers called out in the lab have been tested and shown successful for the lab.

## Exercise 1: Creating the Brain

Duration: 40 minutes

After a requirements gathering effort, Contoso has decided to use the Bonsai platform to optimize their CSTR process.  They will be optimizing for avoiding thermal runaway as well as minimize concentration reference.

**Help references**

|                                       |                                                                        |
| ------------------------------------- | ---------------------------------------------------------------------- |
| **Description**                       | **Link**                                                              |
| One Dev Minute - What is Autonomous Systems? | <https://youtu.be/U0ztL-bncCU> |
| What is Project Bonsai? | <https://www.youtube.com/watch?v=YjnL5-48T6s> |
| Microsoft Learn - Introduction to Microsoft Project Bonsai | <https://docs.microsoft.com/en-us/learn/modules/intro-to-project-bonsai/> |
| Microsoft Docs - What is Project Bonsai? | <https://docs.microsoft.com/en-us/bonsai/product/> |

### Task 1: Set up Bonsai on Azure

You are going to set the Resource group, create Bonsai Tool Chain, and open Bonsai UI.

1. Log into your Azure subscription.

2. Select Resource group:

![Select Resource Group.](media/1-1.png "Resource Group")

3. Select Create:

![Select Resource Group Create.](media/1-2.png "Resource Group - create")

4. Name your Resourcegroup and select the subscription and region, select review + create.  NOTE that your subscription name will vary.  Note also that Bonsai is only available in US West Geo.

![Select Resource Group Name, Geo.](media/1-3.png "Resource Group - create")

5. Validation should pass.  Create the resource group.

![Create Resource Group.](media/1-4.png "Resource Group - create")

6. Navigate to the Resource Group (using pop-up after create completes). Search for Bonsai. Create a Bonsai service.  This should take a few minutes.

![Create Bonsai.](media/1-5.png "Bonsai - create 1")

![Create Bonsai.](media/1-6.png "Bonsai - create 2")

![Create Bonsai.](media/1-7.png "Bonsai - create 3")

![Create Bonsai.](media/1-8.png "Bonsai - create 4")

![Create Bonsai.](media/1-9.png "Bonsai - create 5")

7. Navigate to Bonsai (using pop-up after create completes). Search for Bonsai. Select Launch Bonsai Workspace. You might be prompted for a password.  Congratulations, you have now created a Bonsai Service!

![Launch Bonsai.](media/1-10.png "Bonsai - Launch 1")

![Launch Bonsai.](media/1-11.png "Bonsai - Launch 2")

### Task 2: Creating a Brain

Now that we have have the Bonsai Service deployed, we will start with creating a Brain.

1. From the Bonsai UI environment, select Create Brain:

![Create Brain.](media/2-1.png "Create Brain 1")

2. Name your Brain, and select OK.  You will see an empty Brain created and an error that you cannot train the brain.  This is because your Brain is empty :-D.

![Create Brain.](media/2-2.png "Create Brain 2")

![Create Brain.](media/2-3.png "Create Brain 3")

![Create Brain.](media/2-4.png "Create Brain 4")

### Task 3: Adding Inkling Code

Now that we have the Bonsai UI and we have successfully created a Bonsai Brain, let's start with adding some code. Bonsai uses Inkling language.  The idea is to provide a high level language that is easy to understand and use.
1. Define some simulator constants.  A Bonsai Brain has to Learn in order to be able to act later.  In order for it to learn, it uses a Simulator.  We will be adding a Simulator in the next excercise, however we can define the simulator inputs and ouputs in this section.  
 We define:
	i. The desired concentration
	ii. The current concentration
	iii. The current temperature
	iv. The desired temprature
	v. The coolant absolute temprature 
	
We also define some contants for limits on concentration and temprature.
Finally, we define a SimState - this is the structure that will be used as an input for the Brain.
Add the following code outside the graph block, and below the "using" statements:

```text
# Limits for concentration
const conc_max = 12
const conc_min = 0

# Limits for reactor temperature
const temp_max = 800
const temp_min = 10

# State received from the simulator after each iteration
type SimState {
    Cr: number<conc_min .. conc_max>,         # Concentration: Real-time reactor read
    Tr: number<temp_min .. temp_max>,         # Temperature: Real-time reactor read
    Cref: number<conc_min .. conc_max>,       # Concentration: Target reference to follow
    Tref: number<temp_min .. temp_max>,       # Temperature: Target reference to follow
    Tc: number<temp_min .. temp_max>,         # Coolant absolute temperature as input to the simulation
}

```

2. Now, we define the Observable State.  The Brain uses the Observable State as a graph input to make a descision on what action to take.  

```text
# State which are used to train brain
type ObservableState {
    Cr: number<conc_min .. conc_max>,         # Concentration: Real-time reactor read
    Tr: number<temp_min .. temp_max>,         # Temperature: Real-time reactor read
    Cref: number<conc_min .. conc_max>,       # Concentration: Target reference to follow
    Tc: number<temp_min .. temp_max>,         # Coolant absolute temperature as input to the simulation
}

```

3. Let's add some initial code.  Note that this won't compile just yet. The first step is to add a concept.  A concept is the component of a brain that must be learned, imported or programmed. Our first concept is a Learn concept: ModifyConcentration.  Learned concepts specify a curriculum that defines how the AI should be taught. We will define the curriculum by adding a couple of goals. In order to do that, we define a curriculum that encapsulates the two goals we are setting here - to optimize the concentration, and avoid thermal runaway.  Notice the goal to bring the concentratio is to compare the desired concentration vs. the actual, and try to bring it within a 0.25 range.  The second goal is to avoid tempratures above 400.

```text

graph (input: ObservableState) {
    output concept ModifyConcentration(input):SimAction {
        curriculum {

            # The objective of training is expressed as 2 goals
            # (1) drive concentration close to reference
            # (2) avoid temperature going beyond limit
            goal (State: SimState) {
                minimize `Concentration Reference` weight 1:
                    Math.Abs(State.Cref - State.Cr)
                    in Goal.RangeBelow(0.25)
                avoid `Thermal Runaway` weight 4:
                    Math.Abs(State.Tr)
                    in Goal.RangeAbove(400)
            }
        }        
    }
}

```
4. Notice that in our code we indicate that the Graph output is a SimAction. This is the meat of the Brain - to make a sequential descision based on a given observale state.  So let's define a SimAction now, along with some constants.  Tc_adjust tells the simulator adjust the temprature by.
NOTE that this needs to be above the graph block.

```text
const Ts = 0.5 # Sim Period
const coolant_temp_deriv_limit_per_min = 10 # Coolant temperature derivative limit per minute
const coolant_temp_deriv_limit = Ts * coolant_temp_deriv_limit_per_min

# Action provided as output by policy and sent as to the simulator
type SimAction {
    # Delta to be applied to initial coolant temp (absolutely, not per-iteration)
    Tc_adjust: number<-coolant_temp_deriv_limit .. coolant_temp_deriv_limit>
}

```

5. At this time, you should get a warning about the curriculum not having a source.  In order to learn, we need a source (a simulator) to learn from.  Let's go ahead and define that outside the graph block:

```text
simulator CSTRSimulator(Action: SimAction): SimState {
    # Automatically launch the simulator with this registered package name.
    package "placeholder"
}
```

And modify the curriculum by adding the following line in the curriculum block:

```text

source CSTRSimulator

```

6. At this point, you should have inkling code that compiles (no errors) however, if you hit the train button, it should give you a warning, "placeholder" package not found.  We will be adding the simulator in the next section.

![Train Brain.](media/3-1.png "Trian Brain 1")


## Exercise 2: Create a Simulator

Duration: 40 minutes

Now that we have created the Bonsai Service and written some inkling code, let's work wtih the Simulator.  In this case, Contoso Chemicals is using a Mathlab simulator in oder to simulate the conditions within a CSTR process.

**Help references**

|                                       |                                                                        |
| ------------------------------------- | ---------------------------------------------------------------------- |
| **Description**                       | **Link**                                                              |
| What is Training Simulations for Bonsai? | <https://docs.microsoft.com/en-us/bonsai/product/components/simulation> |

### Task 1: Create a Simulator

First, we need to create the Simulator to use with our Brain.  In this case, we will be using an already created Simulator using MatLab.

1. In a web browser, go to the following github repo:

```Text

https://github.com/microsoft/bonsai-cstr

```

2. Select the "Code" -> "Download Zip"

![Create Simulator.](media/4-0.png "Create Simulator 1")

3. From the Bonsai UI, select the Add Simulator button

![Create Simulator.](media/4-1.png "Create Simulator 1")

4. From the poup, select "MathWorks Simulink":

![Create Simulator.](media/4-2.png "Create Simulator 2")

5. Upload the Zip file downloaded in step 2.

![Create Simulator.](media/4-3.png "Create Simulator 3")

6. Make sure to choose a unique and meaningful name.  This name will be used in the inkling code as a reference. You may also, depending on your budget, set the Memory, core requirements and max instances.  Note that this is the data that will be used to stand up instances of simulators while training the brain.

![Create Simulator.](media/4-4.png "Create Simulator 4")

7. After you select the Create Simulator, you should see a new Simulator added that looks something like this:

![Create Simulator.](media/4-5.png "Create Simulator 5")

Note that you should be able to see the definition of SimState, SimAction and SimConfig.  The SimState and SimAction should match exactly with the way we defined it.  The additional SimConfig section needs to be added to the Inkling code.

### Task 2: Connect to Bonsai Brain

Once you have a Simulator setup, you will need to update the inkling code to connect to the "real" simulator. 

1. Navigate to the Brain you created in the previous excercise.  Edit the curricum, change the source to what you named the Simulator as follows:

```text

    package "CSTRSim42"
	
```

2. Add the SimConfig definition from the Simulator code outside the graph block.  Note that the Cref_signal is a numeric value, used by the Simulator.  We define it as a rage between 1 & 5, stepping 1 at a time. The noise_percentage is a rnage between 0 & 100.

```text
# Per-episode configuration that can be sent to the simulator.
# All iterations within an episode will use the same configuration.
type SimConfig {
	# Scenario to be run - 5 scenarios: 1-based INT
	# > 1: Concentration transition --> 8.57 to 2.000 - 0 min delay
	# > 2: Concentration transition --> 8.57 to 2.000 - 10 min delay 
	# > 3: Concentration transition --> 8.57 to 2.000 - 20 min delay
	# > 4: Concentration transition --> 8.57 to 2.000 - 30 min delay
	# > 5: Steady State --> 8.57
	Cref_signal: number<1 .. 5 step 1>,
	noise_percentage: number<0 .. 100>  # Percentage of noise to include
}
```
3. In order to train the brain, we will need to add some additional code in the cooncept to define the parameters of the training like so:

```text
training {
	EpisodeIterationLimit: 90,
	NoProgressIterationLimit: 500000
}
```
Note that Episodes, or how many training iterations are run are limited by EpisodeIterationLimit.  In our case, we set it to 90.  We also define a condition where Trainig will end without desired results to be 500000. 

4. We also add a lesson using Machine Teaching to limit how we iterate over each episode. In other words, 

```text
lesson `Follow Planned Concentration` {
	# Specify the configuration parameters that should be varied
	# from one episode to the next during this lesson.
	scenario {
		Cref_signal: number<1>, # Transition from 8.57 to 2 with no delay
		noise_percentage: number<0 .. 5>,
	}
}    
```
	
5. At this point, you should be able to train the brain by clicking the green button:

![Create Simulator.](media/4-6.png "Create Simulator 6")

## Exercise 3: Assessment and Optimization

Duration: 40 minutes

At this point, we are ready to train the brain and look at some results.    

### Task 1: Training the Brain

In the previous excercise, we hit the "train" button. Now we are ready to explore the Bonsai Platform using the outputs, errors, and assessments.

1. From the Bonsai UI, click on the train button for your Brain (if you haven't already done so in the last excercise):

![Train Brain.](media/4-6.png "Train Brain 1")

Your screen should look like so:

![Train Brain.](media/5-1.png "Train Brain 2")

Note that the training process is creating multiple copies of simulation in order to train the brain. This takes time.  You can use the Erros and Output window to view the progress of the training process.

### Task 2: Using Assessments

In this task, you will review the assessments, and create some custom assessments.

1. While the Brain is training, you can monitor the progress.  One way is to view the Episodes.  Select the "Teach" tab, and scroll to see the progress of each episode:

![Train Brain.](media/5-2.png "Train Brain 3")

2. You can select the Assessments to see the results.  New assesssments sets are created as the Brain Training continues.  Click on the Assessment 0 to see the results:

![Train Brain.](media/5-3.png "Train Brain 4")

3. If you scroll on the Assessment, you can see the results for each goal in the inkling code:

![Train Brain.](media/5-3.png "Train Brain 5")

![Train Brain.](media/5-4.png "Train Brain 6")

![Train Brain.](media/5-5.png "Train Brain 7")

4. After the training completes, which could take more than an hour, you should be able to see the graph indicating the goal optimization:

![Train Brain.](media/5-7.png "Train Brain 8")


### Task 3: Adding Aditional Code to Optimize

We noticed in the last excercise we noticed that one of our goal did not get to 100%.  Let's see how we can improve this, by going back and adding more inkling code. 

1. From the Bonsai UI, navigate to the existing Brain, move to the "Teach" Tab, and insert a new block of code with a new concept such as SteadyState:

```text

    concept SteadyState(input): SimAction {
        curriculum {

            source CSTRSimulator

            training {
                EpisodeIterationLimit: 90
            }
            # The objective of training is expressed as 2 goals
            # (1) drive concentration close to reference
            # (2) avoid temperature going beyond limit
            goal (State: SimState) {
                minimize `Concentration Reference` weight 1:
                    Math.Abs(State.Cref - State.Cr)
                    in Goal.RangeBelow(0.25)
                avoid `Thermal Runaway` weight 4:
                    Math.Abs(State.Tr)
                    in Goal.RangeAbove(400)
            }

            lesson `Lesson 1` {
                scenario {
                    Cref_signal: number<5>, # Steady State of 8.57 kmol/m3
                    noise_percentage: number<0 .. 5>,
                }
            }
        }
    }
	
```

2. Now, let's add a selector Brain as follows:

```text

 output concept SelectStrategy(input): SimAction {
    select SteadyState
    select ModifyConcentration
    curriculum {

        source CSTRSimulator

        training {
            EpisodeIterationLimit: 90,
            NoProgressIterationLimit: 500000
        }
        # The objective of training is expressed as 2 goals
        # (1) drive concentration close to reference
        # (2) avoid temperature going beyond limit
        goal (State: SimState) {
            minimize `Concentration Reference` weight 1:
                Math.Abs(State.Cref - State.Cr)
                in Goal.RangeBelow(0.25)
            avoid `Thermal Runaway` weight 4:
                Math.Abs(State.Tr)
                in Goal.RangeAbove(400)
        }

        lesson `Lesson 1` {
            scenario {
                Cref_signal: number<2 .. 4 step 1>, # Combinations of Steady State and Transient State
                noise_percentage: number<0 .. 5>,
            }
        }
    }
}

```

3. Remove the "output" keyword from the original concept ModifyConcentration.  Note that a brain can only have one output concept.

```text

output concept ModifyConcentration(input):SimAction {

```

4. You should now have the ability to train the brain using eachone of the concepts / curriculums.

### Task 4: Adding a Visualizer

The Bonsai platform allows you to use a visualizer in order to see the experiments being run and make visual observations.  The process of creating a visualizer will not be covered in this workshop.  However, in our case, there is an existing Visualizer we will leverage.

1. 


## After the hands-on lab

Duration: 15 minutes

Now that the lab is complete, we need to tear down the Azure resources that we created.

### Task 1: Tear down Azure Resources

Now that the lab is done, we are done with our Azure resources. It is good practice to tear down the resources and avoid incurring costs for unnecessary resources.

1. Open the `teardown-infrastructure.ps1` PowerShell script in the `infrastructure` folder of your GitHub lab files repository and add the same custom lowercase three-letter abbreviation we used in a previous exercise for `$studentprefix` variable on the first line.

    ```pwsh
    $studentprefix ="Your 3 letter abbreviation here"
    $resourcegroupName = "fabmedical-rg-" + $studentprefix

    az ad sp delete --id "fabmedical-$studentprefix"
    az group delete --name $resourceGroupName
    ```

2. Execute the `teardown-infrastructure.ps1` PowerShell script to tear down the Azure resources for this lab.

You should follow all steps provided *after* attending the Hands-on lab.
