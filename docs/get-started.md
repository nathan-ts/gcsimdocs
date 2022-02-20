---
sidebar_position: 2
---

# Getting Started

To get started, simply head over to our website at [https://gcsim.app](https://gcsim.app). As of February 19, 2022, we are transition fully into this new web application and will no longer be offering the desktop application (although older version still available for download).

When you first load the page, you will see these options, which we will discuss below:
![](gcsim_starting_page.png)

## Simulator
The simulator is a good starting point for users who are just starting out. This page lets you add characters using an easy to use interface, and then write up your action list from there. For help on getting started with action lists, please see the [Practical Guide](guide/practical_guide.md).

![](adding_character_interface.png)

## Advanced Mode
This is essentially the simulator mode, but without the character adding interface. This is meant for advanced users who are more comfortable with working in a pure text format.

## Viewer
This is where all sim runs get saved to, and where you can find all previous runs that you made in the session (note that they are saved to your browser local storage, so refreshing the page or closing the tab will clear them).

In addition to viewing your results, you can also generate a link to share your results with others in the "Share" tab. Note that shared results are only saved for 7 days due to server constraints, so please make sure to download anything that you want to save.

If you are an advanced user, this is where you can also go to upload the output file to view those results.

## Other Links
We're still working on getting those up and running properly.

# Advanced users

For advanced users, the command line tool is still available and can be built directly from source. The command line tool offers performance boost over the web application as it is not subject to limitations in the browser. The git repo is located [here](https://github.com/genshinsim/gcsim). You will need to have go installed. Use the following command to run the tool:

```shell
cd cmd/gcsim
go run .
```
