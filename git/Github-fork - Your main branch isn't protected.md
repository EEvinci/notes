# Github-fork -> Your main branch isn't protected

Git has no notion of protected branches. They are purely a GitHub/GitLab, etc. concept. You should simply click "Protect this branch" to enable branch protection.

I'm not sure why you're repeatedly trying to change the upstream and push to different branches. I'm assuming you're on the same branch running each of these pushes. But if that's the case then you're changing the upstream and which branch your targeting with each push. Git will protect you, but using `-f` is very destructive since it disables a majority of the existing safety checks including potentially overwriting yours or someone else's work.

Also,

> I figured maybe it's a built-in alarm for when someone's forcefully deleting stuff, but I'd like to be sure. Also, I'm sure you're right on -f, but I'll keep doing it - at least as long as it says so in an SO answer

Just because another SO post claims something is the answer, doesn't mean its the same answer in your situation. Trying the same commands over and over won't solve your issue, it'll only serve to frustrate you.

# What seems to be the problem?

You're receiving an error that there are multiple refspecs with the name `branch_name`. My guess is you have names that collide, such as a tag and a branch name that are the same, etc. As a general rule **never** have tags and branches with the same name. This can cause conflicts with git.

However, let's start simply here. Nowhere do I see any updating of the local refs. Simply updating the refs and then pushing might solve your issue.

## Approach 1: Ensuring your refs are up to date

1. `git fetch` will keep your git client's refs information in sync with remote.
2. `git checkout branch_name`
3. `git push -u origin branch_name`

## Approach 2: Creating a different branch

Let's create a new branch with a name other than `branch_name` since there seems to be some sort of conflict:

1. `git fetch`
2. `git checkout -b my_new_branch branch_name` will create a new branch off of branch_name locally and switch to it.
3. `git push -u origin my_new_branch`

## Approach 3: Trying to fix the refs issue

If you absolutely must have `branch_name` as the name, you can try to resolve the conflicts. I'm not sure if the below will work as its **untested**, based on speculation and I'm unsure how to recreate your scenario.

1. `git fetch` will update the git client's refs so they're aware of changes on remote.
2. `git checkout branch_name` to checkout your local branch
3. Delete any tags that conflict:

- `git tag -d branch_name` will delete the corresponding local tag.
- `git push --delete origin :refs/tags/branch_name` will delete tags on remote that have the conflicting name. You'll get an error if non existent

1. `git push --delete origin branch_name` will permanently delete the remote copy of branch_name. **Before** running this make sure you have all the commits you expect on your local copy. Again, you'll get an error if the branch does not exist.
2. This should clear up any issues with the refs. You should be able to do `git push -u origin branch_name` now.

- Alternatively, you can also try `git fetch --prune` will remove all branch refs that do not exist on remote.

1. `git tag -a new_tag_name -m "tag message" sha1` recreate the release tag we previously deleted. sha1 is the commit hash of the release you previously tagged.
2. `git push origin new_tag_name` pushes the tag to remote and automatically creates a release in GitHub.

I hope one of those solves your issue.





# Github-fork -> 你的主分支不受保护

Git 没有受保护分支的概念。 它们纯粹是一个 GitHub/GitLab 等概念。 您只需单击“保护此分支”即可启用分支保护。

我不确定您为什么反复尝试更改上游并推送到不同的分支。 我假设你在同一个分支上运行这些推送。 但如果是这种情况，那么您将更改上游以及每次推送时您的目标分支。 Git 会保护您，但使用 `-f` 是非常具有破坏性的，因为它会禁用大部分现有的安全检查，包括可能覆盖您或其他人的工作。

还，

> 我想这可能是当有人强行删除东西时的内置警报，但我想确定一下。 另外，我确定你在 -f 上是对的，但我会继续这样做 - 至少只要它在 SO 答案中这样说

仅仅因为另一个 SO 帖子声称某些东西是答案，并不意味着它在您的情况下是相同的答案。 一遍又一遍地尝试相同的命令不会解决您的问题，它只会让您感到沮丧。

# 似乎是什么问题？

您收到一条错误消息，指出存在多个名为“branch_name”的引用规范。 我的猜测是你有冲突的名称，例如相同的标签和分支名称等。作为一般规则，**永远不会**具有相同名称的标签和分支。 这可能会导致与 git 的冲突。

然而，让我们简单地从这里开始。 我在任何地方都看不到本地引用的任何更新。 简单地更新 refs 然后推送可能会解决您的问题。

## 方法 1：确保您的参考文献是最新的

1. `git fetch` 将使您的 git 客户端的 refs 信息与远程同步。
2.`git checkout 分支名称`
3.`git push -u origin branch_name`

## 方法 2：创建不同的分支

让我们创建一个名称不是 branch_name 的新分支，因为似乎存在某种冲突：

1.`git 获取`
2. `git checkout -b my_new_branch branch_name` 将在本地从 branch_name 创建一个新分支并切换到它。
3.`git push -u origin my_new_branch`

## 方法 3：尝试修复 refs 问题

如果您绝对必须使用 branch_name 作为名称，您可以尝试解决冲突。 根据推测，我不确定以下内容是否可以作为其**未经测试**使用，并且我不确定如何重新创建您的场景。

1. `git fetch` 将更新 git 客户端的引用，以便他们知道远程上的更改。
2. `git checkout branch_name` 来检查你的本地分支
3. 删除所有冲突的标签：

- `git tag -d branch_name` 会删除相应的本地标签。
- `git push --delete origin :refs/tags/branch_name` 将删除远程上具有冲突名称的标签。 如果不存在，你会得到一个错误

1. `git push --delete origin branch_name` 将永久删除 branch_name 的远程副本。 **在**运行此之前，请确保您在本地副本上拥有您期望的所有提交。 同样，如果分支不存在，您将收到错误消息。
2. 这应该可以解决裁判的任何问题。 你现在应该可以执行 `git push -u origin branch_name` 了。

- 或者，您也可以尝试 `git fetch --prune` 将删除远程上不存在的所有分支引用。

1. `git tag -a new_tag_name -m "tag message" sha1` 重新创建我们之前删除的发布标签。 sha1 是您之前标记的版本的提交哈希。
2. `git push origin new_tag_name` 将标签推送到远程，并自动在GitHub 中创建一个release。

我希望其中之一可以解决您的问题。