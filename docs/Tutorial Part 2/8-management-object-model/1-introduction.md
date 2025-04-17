---
sidebar_position: 1
---

# Introduction

Consider the Fuel Economy Federation again. The Master federate is responsible for starting and stopping the federation. In our sample federation, there are two different federates that simulate cars. How can the Master federate make sure that the user doesn’t start the scenario before both car simulations have joined? To do this, the federate needs some insight into the federation. The Management Object Model, MOM, which is part of the MIM can help us with this. It provides objects and interactions that enables us to monitor and control the federation. 