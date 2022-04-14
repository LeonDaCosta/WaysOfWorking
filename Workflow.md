# Developer Workflow

Developers workflow should be inline when using version control and project management software to effectively collaborate together and reach peak efficiency. Here's some information on the best way teams can work well together while developing.

# Table of Contents

- [Git Flow](#git-flow)
  - [Git Collaboration and Techniques](#git-collaboration-and-techniques)
  - [Writing Git Commit Messages](#writing-git-commit-messages)
- [Pull Requests](#pull-requests)
  - [Self Review](#self-review)
  - [Submitting](#submitting)
  - [Reviewing and Commenting](#reviewing-and-commenting)
  - [Approval and Merging](#approval-and-merging)
- [Code of Conduct](#code-of-conduct)

## Git Flow

Git Flow should be used where acceptable to improve collaboration on projects in the team and make deployments
easier to manage.

More details on Git flow can be found here - https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

### Git Collaboration and Techniques

Git is designed to be used for teams to collaborate and should be used as such. Sometimes companies can fall into the trap
of using git as a fancy tool to `Save` and this can be avoided by remembering to follow these rules.

- Commits should always be small and attempt to contain code that performs only 1 job (Separation of concerns). This will
  help in the future if you need to cherry-pick small portions of code from one branch to another.
- Commits should never contain broken code unless you absolutely have to, in which case it should be prefixed with `WIP:`.
  Although broken code should be avoided in commits you can commit incomplete but working features no problem. For example, a migration with just the `up`
  method as it is an incomplete migration but still works. See the section above https://github.com/PrecisionProcoGroup/WaysOfWorking#commit-only-working-code
- Always push your branch after each commit you make. This assures that if you are taken ill or moved onto another project your work
  can be picked up by another team member immediately with no delay. If you are following the rule above this shouldn't be an issue at all!
- When working on the same branch with a teammate, this can be achieved easily while keeping the git tree clean and in a straight line.
  You do so by making sure to fetch your teammates commits after you have made a commit then rebasing your local branch on the remote. 
  For example if you are checked out on `feature/PPG-123` and you have just fetched; assuming commits were pulled in from the remote then you can 
  run `git rebase origin/feature/PPG-123`. This will put your commits on top of the ones you just fetched keeping you up to date with a clean tree.
- When making commits which make changes from feedback on a PR/MR, make sure to commit each change independently following the commit guidelines,
  do not group changes into a single commit called "PR Feedback" for example as this is not useful to the git history and anyone navigating the git log.
- Try to avoid making commits directly to master or develop as this may cause unforeseen side effects to occur, and will cause
  team members to have to update more often with their target branch making the git tree more untidy.
- Never force push ever, ever, ever, as team members will lose their work!

### Writing Git Commit Messages

The following outlines some guidelines of how to write git commit messages that will make your git tree look amazing, and may possibly end up
helping you in the future.

- All commit messages should be clear and concise with no ambiguity
- A commit message subject should always contain enough context to understand the actions of the developer and the impact
  of the code contained in the commit, for more detail use the commit message body.
- A commit message subject should not contain the word `and`, when it is used it may signify you need a separate commit. This rule should
  not take precedence over the rule of never committing broken code, in that case usage of the word `and` is fine.
- A commit message subject must attempt where possible to finish the sentence of `It`, `It will`, or `It has`. When choosing 1 of the 3 to complete for your work,
  try to maintain consistency. Examples can be seen below where highlighted text would become the commit message subject.
    - It `Fixes my problem`
    - It will `Fix my problem`
    - It has `Fixed my problem`
    - It `Adds a new feature`
    - It will `Add a new feature`
    - It has `Added a new feature`
    - It `Updates my existing feature`
    - It will `Update my existing feature`
    - It has `Updated my existing feature`
- Commit message subjects should never be finished with a period
- A commit message subject should not exceed 50 chars
- All lines of a commit message body should be wrapped at 72 chars
- A commit message body must be seperated from the commit message subject by a single blank line
- Commits should be written in sentence case, see details here - https://en.wikipedia.org/wiki/Letter_case#Sentence_case
- If using JIRA for project management, it is ideal to prefix all commit message subjects in square brackets with the ticket number `[CLC-123]`.
  This will provide a link to the ticket in JIRA directly from the commit.
- All commit messages should have no passive-aggressive context towards other developers or situations in the company.

> *TIP*: set up a default commit message template in your git config to help you adhear to all these rules

## Pull Requests

A development team generally leans heavily on pull requests to assure code quality and to make sure that work is done
on time. Let's see the best way PR's can be managed to keep all the cogs moving.

### Self Review

Before submitting a PR you should be doing a self review of your own code before you consider it final and ready for submission.

There are a number of ways you can do this. You can first submit a draft PR in the browser and then browse the changes you have made in the
browser making notes of any changes you might want to make there, then fix them and once done mark the PR as ready.

You can also use the cli to show you a diff between your branch and the target branch and make changes then before submission, or you could also use
a diff tool with a UI.

Whatever way you choose to view the diff and the changes you made, these are the things you should look out for, some things will need to be done outside the diff:

- **Commented out code** If you need to comment out code for any reason then a TODO comment should be added above the commented out code to explain your reasoning as to why 
  it was commented out instead of being removed and when you will be addressing its removal.
- **Useless doc blocks** Commonly these are doc blocks that either repeat what the code already said (see the section https://github.com/PrecisionProcoGroup/WaysOfWorking#comment-only-what-the-code-cannot-say) 
  or they are doc blocks that are just plain pointless and add no value at all (commonly added by code generator commands from frameworks such as laravel)
- **Pointless constructs and empty methods** Again these are usually added by either copying and pasting template classes or using
  code generator commands from frameworks such as laravel. This method of development should be avoided as it can cause you to spend more time removing
  code and cleaning up than if you were to just write it yourself.
- **Coding Standards** Always do a quick scan for anything like type hinting, trailing commas, indentation, and anything else standards related that might pop out. 
  Never rely on automated standards tools finding everything, things will always find a way through.
- **Architecture** Always run over in your head the architecture of your work as you are scanning your changes to assure you have not made any mistakes that could 
  cause a code smell in the future. https://en.wikipedia.org/wiki/Code_smell
- **Teardown and rebuild from scratch** For large features, especially ones that contain significant changes to the env and database, you should
  tear down your local setup removing the database and env file and rebuild from the readme from scratch to make sure that you don't encounter any fatal errors 
  that will be an immediate blocker to somebody reviewing your work.
- **Visual click through** For features involving changes to the UI or large new UI features, you should do a final click around on the UI throwing all sorts of 
  random data at your feature manually and fairly fast. If you encounter a problem you can fix it there and then before submission.

### Submitting

When submitting a pull request the last thing a developer reviewing it wants is to come to review it and find that the
branch is out of date with the target branch and the description is lacking details of what you have done.

Make sure that you are keeping your PRs up to date with the target branch, until they have been reviewed. To do this
you can do the following:

```
git fetch
git checkout your-branch-in-for-pr
git merge --no-ff origin/target-branch
```

When it comes to a description, it's all very well and good linking to a ticket that was the request for the new feature,
however this could be and generally will be a rather high level description of the request. It's your responsibility to
describe the technical implementation you chose and the reasons behind it. Maybe some limitations as to why you didn't choose
an obvious one and went with something more complex. You should also think about any special requirements for testing
and will the reviewer need to know this. Also, for an audit trail its wise to include a screenshot for any visual changes
you made.

### Reviewing and Commenting

To make sure to keep on top of PR's it is advisable to reserve 30-60 minutes at the end or beginning of each day to review them.
Each PR should be reviewed for coding standards, syntax issues, and of course domain/business logic.

Commenting on PR's can be tricky, too often developers can comment on PRs with little thought or concern for the person
receiving the comment. If the developer has spent a lot of time working on it, some comments can feel quite grating and
can be taken to heart. Due to this, always make sure to do your best to convey tone of voice in a PR comment using emojis,
and if you are trying to explain something particularly complex maybe even follow up the comment with a message on Teams.

Sometimes you may notice a mistake has been made in a PR which may have simply been an oversight and could potentially be
slightly embarrassing to mention publicly in PR comments. This can sometimes then be best to contact the developer directly via
Teams to let them know some improvements they can make before you do an official review.

You can also pair up with the author of a PR on a Team call to go through the PR in person and fix any issues there and then, together.
This can help in staff development and reduce time spent on reviewing code.

All of these things help to avoid any conflict and toxic situations in comments sections of PRs.

### Approval and Merging

This section of PRs should be fairly simple. It is recommended that when there are at least 2 (or the amount the business is happy with)
approvals from reviewers which should come from a collection of developers picked by the company.

Senior developers should then be able to merge it once these requirements have been met. If an update to that PR is made after the approvals' quota
is reached then the quota is reset and the approval process restarts before a merge can be completed.

You should always merge in a way that maintains the hillocks in the git tree, and remove the branch after merging, you should never squash a branch into another unless you need to hide the history.

You can correctly merge a branch like so:

```
git checkout target-branch
git merge --no-ff branch-to-merge
git branch -D branch-to-merge
```

## Code of Conduct

- Generally be good to one another, and don't take life too seriously.
- Have time for your fellow developers, and they will have time for you.
- Respect other developers opinions and they may respect yours.
- Remember that there is always someone out there you can learn from regardless of yours or their level.