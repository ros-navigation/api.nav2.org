# api.nav2.org

Hosting Nav2 & ROS 2 doxygen in a developer-friendly format.

Totally vibe-coded with Claude Code to the minimum degree required to function.
Read the source code and submit PRs at your own (sanity's) risk.
Contributions welcome, but manual testing is required.

## Updates Note

If any found, put them in the description tables with a detailed description of what they do and an example usage in the C++ and Python examples.


### Claude Update Workflow for a New Distro

1. Review this project in detail to understand what it does and its context

2. Now, I want to add <NEW DISTRO> to the Nav2 and ROS distributions. Also update Rolling Nav2's doxygen, if that's necessary. For now, focus on just the distribution and doxygen parts and copy over the Rolling action/service/topic message APIs to <NEW DISTRO> to start off with (both rolling and <NEW DISTRO> will need updates in another phase). The artwork for Nav2 <NEW DISTRO> release is here: <URL HERE>. The artwork for the ROS 2 <NEW DISTRO> release is here: <URL HERE>. Remove <EOL DISTROS>

3. Next, review the curent nav2 rolling branches messages, services, and topics in nav2_msgs. List all the new messages or new fields to those messages which we need to update on rolling. Then, propose the updates to the page(s) and new pages to cover them in rolling in the plan proposal, including full descriptions you plan to use.

4. Do all of this and also make all of these updates in Rolling and <NEW DISTRO> both, so that they are the same

5. Make sure all actions, srvs, and msgs are alphabetized in order on the index page for rolling and <NEW DISTRO>

6. Make sure all msg/action/srv pages's examples have the python and C++ examples using the new field(s) and ROS interfaces
