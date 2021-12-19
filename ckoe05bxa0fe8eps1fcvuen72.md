## Good Commits

Git commits are everywhere, and you might be generating more than 1k commits over a year. So it becomes crucial to understand that commit should be structured and created in a scalable manner.

![commit.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620370751015/SCRWL-P3a.png)

## Why bother?

- Writing better commits can make the difference between your debugging session lasting **1 hour to a few minutes**.

- With good commits, it's easier for anyone to understand the progress of a project and get up to speed. 

- It also allows reviewers to understand your progress during the resolution of an issue clearly.

- Generating good commits will allow you to track back changes/issues to a specific module/file and associate it to the code easily.

- They enable you to understand how the issue crept in the codebase and how you can easily resolve it.

- Good commit messages can save you the hassle while creating release notes

## What are good commits?

### Modular


![Modular Commits](https://cdn.hashnode.com/res/hashnode/image/upload/v1620372512823/nU2KOcvIB.jpeg)

A commit should be **modular** in nature, just like our codebase. Each commit should **encapsulate** a single logical idea only that might span over several changes but as a whole is a single related group of changes.

E.g., add CSS to a component, change the margin of all pages, strong typing your functions, etc.

### Type of Commit

**Categorising** your commits into types also clarifies what type of change it made and can be identified instantly. I usually keep a template file that contains those types so I don't have to remember them :P

Some of the subtypes can be a chore, feat, fix, refactor, style, etc. What meaning does each carry can vary based on your team or you as an individual as well. Below are the types that I use in my commits :

-   feat: new feature
-   fix: bug fix
-   refactor: refactoring production code
-   style: formatting, missing semicolons, etc.; no code change
-   docs: changes to documentation
-   test: adding or refactoring tests no production code change
-   chore: updating dependencies etc. no production code change

### Description

![Perfect Description](https://media.giphy.com/media/kEFa2FuLcG0mn3t0ef/giphy.gif)

A commit message except for the subject line limited to `50` chars should include a description broken into `72` char lines/line. The description is separated from the subject by a blank line. The description should try to cover things like :

- the current behaviour,
- what change are you making?
- why this fix is needed?
- why take the current approach for this change?

Commit message should be in the future tense, i.e. 'Fix' vs 'Fixed.' 

## Bonus Treats


![Treat](https://media.giphy.com/media/Y0UmGpoLtAlrvdrK9Q/giphy.gif)


You can specify a template for your git commits by adding the following config to your `$HOME/.gitconfig`

```bash
[commit]
    template = ~/path/to/template
```

My template looks like this, which allows constraining the number of characters in the subject and description line. I also add the types and just in case I don't remember :'(

```bash
# <type>: <subject>
##### Subject 50 characters ################# -> |


# Body Message
######## Body 72 characters ####################################### -> |

# --- COMMIT END ---
# Type can be
#   feat    : new feature
#   fix     : bug fix
#   refactor: refactoring production code
#   style   : formatting, missing semi colons, etc; no code change
#   docs    : changes to documentation
#   test    : adding or refactoring tests
#             no production code change
#   chore   : updating grunt tasks etc
#             no production code change
```

_**Note**_ : For your template to be prompted, you have to use `git commit`.


