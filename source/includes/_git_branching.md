# Git Branching Protocol
## Git Branch Cheat Sheet

## Developer Workflow

<aside class="notice">
We integrate <a href="https://tree.taiga.io/project/jtarball-mcc/">taiga.io</a> with Github.
</aside>

For more see the following:

- [Github Integration](https://tree.taiga.io/support/integrations/github-integration/)
- [Changing Element Status via Commit Message](https://tree.taiga.io/support/integrations/changing-elements-status-via-commit-message/)

<hr>


- Initially in "Open" status - avoid working on the ticket
- Ticket will move to "Dev ready" status when available to be picked up and worked on
- Pick up the ticket (assign to yourself if not already assigned)
- Set "Start progress" once work begins in earnest on the ticket
    - Merging to B_CI is fine at this point
- When work is completed, set status to "Resolved" with:
    - Resolution: "Fixed" (or some other suitable status as applicable);
    - Documentation: set if required (for customers' info, e.g. API change);
    - "How to Test": to include instructions for a tester where applicable
- Once in a resolved state:
    - Must be merged to B_CI
    - Must be merged to B_FeatureTest
    - Can arrange with QA for testing: status will change to "In Test"; or
    - If not going through QA (i.e. testing to be done internally) status can be left unchanged
- Once testing is complete, status can be changed to "Ready to Release"

> Make sure to replace `meowmeowmeow` with your API key.

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

### Branch Procedure

### Taiga Cheat Sheet Statuses

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
Ready for test | `#ready-for-test` | TF-89 #ready-for-test another commit | <div class="color-box" style="background-color: rgb(245, 121, 0);"></div>
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



```extra
Epics

New new   TF-77 new a very nice commit

User Story

Task 

Issue


```

Create your own feature branch from B_DevBase, in the format 'B_DEV_{JIRA-REF}'. When work is in a stable state, it is merged into B_CI (this can be often). When work is ready for testing, you will be invited to merge your branch into B_FeatureTest. When testing is complete, your branch will be merged by the ops team into the release candidate branch. Eventually the release candidate branch will be merged into release branch.

You must never merge B_CI or B_FeatureTest into your feature branch, or any other branches, and you may only merge your branch into the B_CI branch, unless otherwise invited.

A quick step by step:

1) You should checkout B_DevBase everywhere.

2) On the modules you will be changing (eg sportsbook), you should branch for your feature(git checkout -b B_DEV_xxx). The other modules should remain on B_DevBase.

3) When your development is in a stable state, or you have database changes (stored procedures) you need to be shared you should merge IN TO B_CI.

4) You should never merge any branch apart from B_DevBase into your development branch. There is 1 exception to this. If your feature depends on another feature you can merge that features branch into your own. You must mark this feature as a dependency in jira for your feature.

5) NEVER merge B_CI, B_FeatureTest anywhere.

6) When you have finished your development, mark it as ready to test/resolved in JIRA.

7) When the time comes, QA will ask you to merge your feature branch into B_FeatureTest and upgrade the feature test database. You should also set jira status to 'testing'.

8) If QA find any issues, they must be fixed on the original feature branch B_DEV_xxx and then merged into B_FeatureTest. The reason for this is the feature branch is merged into the release candidate.