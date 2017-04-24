# Git Branching Protocol

## Developer Workflow

<aside class="notice">
We integrate <a href="https://tree.taiga.io/project/jtarball-mcc/">taiga.io</a> with Github.
</aside>

For more see the following:

- [Github Integration](https://tree.taiga.io/support/integrations/github-integration/)
- [Changing Element Status via Commit Message](https://tree.taiga.io/support/integrations/changing-elements-status-via-commit-message/)


<hr>
<pre>
                (TG-<REF> branched off master)
B_Release       -------------------------------------------->
                  |                                      /
master          ----------------------------------------|--->   (master tracks B_Release, and may be updated more frequently than B_Release with new features and bug fixes)
                   \     :   \       :              /  /        (Release candidate is taken from master and eventually merged into B_Release)
B_ReleaseCandidate  \    :    -------------------------
                      \      :       :          /               (your successfully tested branch merged to B_ReleaseCandidate)
TG-<REF>              -+++----+----+------------                    (Update TG-<REF> from master if needed)
                         \  \  \  \   \     \                   #### NEVER MERGE B_FeatureTest into other branches #### 
B_FeatureTest   -------------------------------------------->   (Your branch gets merged to B_FeatureTest for testing)
</pre>

### The Flow
- Ticket when in `"Ready"` status is available to be picked up and worked on. (Note: Task does not have a `"Ready"` status)
- Pick up the ticket (assign to yourself if not already assigned)
- Create a feature branch by forking the repository under your username and creating a feature branch.
    - We basically follow the <a href="https://help.github.com/articles/github-flow/">Github Flow</a> (Possibly tag before delete branch maybe)
- The feature branch should be named based on the taiga.io ticket number (The ticket number should be in the top left)
    - [Example of taiga.io ticket](https://tree.taiga.io/project/jtarball-mcc/task/77)
    - It should be of the form: `TG-<TAIGA_TICKET_NUMBER>` e.g. TG-77
    - Every commit message for this feature branch should start with the branch name e.g. "TG-77"
- Set Taiga ticket to `"In Progress"` (normally but adding #in-progress to commit message <a href="https://tree.taiga.io/support/integrations/changing-elements-status-via-commit-message/">How?</a> and <a href="#taiga-cheat-sheet-statuses">Cheat Sheet</a>)
    - If Taiga fails to change because of a failed webhook response set it manually in Taiga
    - Test locally or with help of the master environment (To be named)
- When your work is ready to be reviewed (Github refers to this as a <a href="https://help.github.com/articles/creating-a-pull-request/">pull request</a>)
    - Click "<a href="https://help.github.com/articles/about-pull-requests/">Create Pull Request</a>" on your github branch
        - Ensure that you are comparing master (main ) with your feature branch (from your fork)
        - Set the assignee
        - Set the reviewers (must be at least two people)
        - In the title remember to start with the branch name i.e. TG-<TAIGA_REF>
        - Add a comment and add some useful information about the change
        - When ready, click create pull request
- When work is completed, reviewed and accepted by all reviewers:
    - Once in a resolved state:
        - Must be merged to **B_FeatureTest**
    - Set `"Ready for test"` in taiga.io
        - Add #ready-for-test to the commit message (If this fails manually change it in taiga.io)
        - Do not set to "ready for test" before you have merged to **b_FeatureTest** 
    - Documentation: set if required 
    - Update "How to Test": to include instructions for a tester where applicable
    - The feature must then go through QA on **B_FeatureTest**.
        - If "Documentation update needed" is set in taiga.io ensure the documentation goes through QA
- Once testing is complete, merge to master and status can be changed to `"Done"` or if a Task to `"Closed"`

### Modified Flow for 'Tasks' Only
<aside class="warning">
You must have a bigger feature branch for this feature (task) to be merged into.
</aside>
<aside class="notice">
Useful for smaller code review / conversations
</aside>
- With taiga.io `tasks` that are part of a complete feature (`User Story`) you can follow the following **MODIFIED** flow:
    - Create the feature branch as normal based on the task
    - Create a pull request against **master** repo
    - Merge into the bigger feature branch (normally going to be the `User Story` Branch)

### Branch Procedure

### Taiga Cheat Sheet Statuses

<aside class="notice">Use the following format to change taiga in the commit message:    TF-{REF} #{SLUG} {COMMIT_MESSAGE}</aside>
<aside class="warning">Do not use semi-colons in the commit message if you want to change the status in taiga</aside>

### Epic

Name | Slug | Example | Colour
--------- | ----------- | --------- |  ---------
New | `#new` | TF-89 #new This is a commit | <div class="color-box" style="background-color: rgb(153, 153, 153);"></div>
Ready | `#ready` | TF-89 #ready | <div class="color-box" style="background-color: rgb(255, 138, 132);"></div>
In progress | `#in-progress` | TF-89 #in-progress | <div class="color-box" style="background-color: rgb(255, 153, 0);"></div>
Ready for test | `#ready-for-test` | TF-89 #ready-for-test another commit | <div class="color-box" style="background-color: rgb(252, 192, 0);"></div>
Done | `#done` | TF-89 #done | <div class="color-box" style="background-color: rgb(102, 153, 0);"></div>

### User Story

Name | Slug | Example | Colour
--------- | ----------- | --------- |  ---------
New | `#new` | TF-89 #new This is a commit | <div class="color-box" style="background-color: rgb(153, 153, 153);"></div>
Ready | `#ready` | TF-89 #ready | <div class="color-box" style="background-color: rgb(245, 121, 0);"></div>
In progress | `#in-progress` | TF-89 #in-progress | <div class="color-box" style="background-color: rgb(114, 159, 207);"></div>
Ready for test | `#ready-for-test` | TF-89 #ready-for-test another commit | <div class="color-box" style="background-color: rgb(78, 154, 6);"></div>
Done | `#done` | TF-89 #done | <div class="color-box" style="background-color: rgb(204, 0, 0);"></div>
Archived | `#archived` | TF-89 #archived | <div class="color-box" style="background-color: rgb(92, 53, 102);"></div>

### Task

Name | Slug | Example | Colour
--------- | ----------- | --------- |  ---------
New | `#new` | TF-89 #new This is a commit | <div class="color-box" style="background-color: rgb(153, 153, 153);"></div>
In progress | `#in-progress` | TF-89 #in-progress | <div class="color-box" style="background-color: rgb(114, 159, 207);"></div>
Ready for test | `#ready-for-test` | TF-89 #ready-for-test This is another commit | <div class="color-box" style="background-color: rgb(245, 121, 0);"></div>
Closed | `#closed` | TF-89 #closed | <div class="color-box" style="background-color: rgb(78, 154, 6);"></div>
Needs Info | `#needs-info` | TF-89 #needs-info | <div class="color-box" style="background-color: rgb(204, 0, 0);"></div>

### Issue

Name | Slug | Example | Colour
--------- | ----------- | --------- |  ---------
New | `#new` | TF-89 #new This is a commit | <div class="color-box" style="background-color: rgb(153, 153, 153);"></div>
In progress | `#in-progress` | TF-89 #in-progress | <div class="color-box" style="background-color: rgb(114, 159, 207);"></div>
Ready for test | `#ready-for-test` | TF-89 #ready-for-test another commit | <div class="color-box" style="background-color: rgb(245, 121, 0);"></div>
Closed | `#closed` | TF-89 #closed | <div class="color-box" style="background-color: rgb(78, 154, 6);"></div>
Needs Info | `#needs-info` | TF-89 #needs-info | <div class="color-box" style="background-color: rgb(204, 0, 0);"></div>
Rejected | `#rejected` | TF-89 #rejected | <div class="color-box" style="background-color: rgb(211, 215, 207);"></div>
Postponed | `#postponed` | TF-89 #postponed | <div class="color-box" style="background-color: rgb(117, 80, 123);"></div>

### Quick Step-by-Step

Create your own feature branch from **master**, in the format '**TG-{TAIGA-REF}**'.


When work is ready for testing, you will be invited to merge your branch into B_FeatureTest.

When testing is complete, your branch will be merged by the ops team into the release candidate branch.

Eventually the release candidate branch will be merged into release branch.

You must never merge **B_FeatureTest** into your feature branch, or any other branches, and you may only merge your branch into the **B_FeatureTest** branch, unless otherwise invited.

A quick step by step:

1) You should checkout **master** everywhere.

2) On the services you will be changing, you should branch for your feature (`git checkout -b TG-xxx`). The other modules should remain on **master**.

3) When your development is in a stable state, or you have database changes (stored procedures) THAT need to be shared you should merge IN TO a new created feature integration branch.

4) You should never merge any branch apart from **master** into your development branch. There is 1 exception to this. If your feature depends on another feature you can merge that features branch into your own. You must mark this feature as a dependency in taiga for your feature.

5) NEVER merge **B_FeatureTest** anywhere.

6) When you have finished your development, mark it as ready to test/resolved in Taiga.

7) When the time comes, QA will ask you to merge your feature branch into **master**.

8) If QA find any issues, they must be fixed on the original feature branch TG-xx and then merged into **B_FeatureTest**. The reason for this is the feature branch is merged into the release candidate.
