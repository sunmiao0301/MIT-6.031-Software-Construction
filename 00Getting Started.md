## Getting Started

由于MIT 6.031 spring 21不是完全开源的，**除了本文件，其他内容均转向[spring 16](https://ocw.mit.edu/ans7870/6/6.005/s16/index.html)**

[关于设置Git, MIT的意见见此](http://web.mit.edu/6.031/www/sp21/getting-started/#git-preferences)

这里有一个有用的东西，正常情况下，一般是`git log`得到如下结果：

![image-20221111184610623](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202211111846731.png)

但是MIT推荐创建一个`git lol`方法：`git config --global alias.lol "log --graph --oneline --decorate --color --all"`，在此之后再去`git lol`就能看到更为清楚的log如下：

![image-20221111185003843](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202211111850872.png)

此外，还可以检查你的全部git设置，可以看到刚刚新加的alias已经在里面了

![image-20221111185219670](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202211111852699.png)

### 什么是 Git？

Git 是一个版本控制系统 (VCS)。[*Pro Git*书](http://git-scm.com/book)描述了 Git的用途：

> 版本控制是一个系统，它记录一个文件或一组文件随时间的变化，以便您以后可以调用特定版本。...和更多。使用 VCS 通常还意味着，如果您搞砸或丢失文件，您可以轻松恢复。

一些最重要的 Git 概念：

- **存储库：**包含与项目（例如，6.031 问题集或团队项目）相关的所有文件以及对这些文件的整个*提交*历史的文件夹。
- **提交（或“修订”）：**给定时间点存储库中文件的快照。
- **add（或“stage”）：**在对文件的更改可以*提交*到存储库之前，必须*添加*或*暂存*有问题的文件（在每次提交之前）。这使您可以一次只提交对您选择的某些文件的更改，但如果您不小心忘记在提交之前添加您想要提交的所有文件，也会有点痛苦。
- **克隆：**由于 Git 是一个“分布式”版本控制系统，因此没有集中式 Git“服务器”的概念来保存您代码的最新官方版本。相反，开发人员“克隆”包含他们想要访问的文件的远程存储库，然后提交到他们的本地克隆。只有当他们将本地提交*推*送到原始远程存储库时，其他开发人员才能看到他们的更改。
- **push：**将本地提交发送到远程存储库的行为。同样，在您添加、提交*和*推送您的更改之前，其他人无法看到它们。
- **pull：**检索对远程存储库的提交并将它们写入本地存储库的行为。这就是您在进行初始克隆之后能够看到其他人所做的提交的方式。

### 克隆

通过将远程存储库克隆到计算机上的本地存储库中，您开始在 6.031 中使用 Git 存储库。

为此，请打开终端（在 Windows 上使用 Git Bash）并使用`cd`命令切换到您想要存储代码的目录。然后运行：

```
git clone *URI-of-remote-repo*
```

或者

```
git clone *URI-of-remote-repo* *project-name*
```

替换`URI-of-remote-repo`为远程存储库的位置，并替换`project-name`为适当的项目名称，例如`ps0`. 结果将是一个`project-name`包含存储库内容的新目录。这是您的本地存储库。

克隆存储库后，您应该使用命令提示符导航到存储库`cd`。这使您可以`git`在存储库上运行命令。

### 创建提交

Git 中数据的基本构建块称为“提交”。提交代表对一个或多个文件的一些更改（或创建或删除一个或多个文件）。

当您更改文件或创建新文件时，该更改不是存储库的一部分。添加它需要两个步骤。第一次运行：

`git add file.txt`（`file.txt`要添加的文件在哪里）

您要么需要从与文件相同的目录运行该命令，要么在文件路径中包含目录名称。

这将*暂存*文件。其次，一旦你完成了所有的更改，运行：

```
git commit
```

*这将为您的提交消息*弹出编辑器。当您保存并关闭编辑器时，将创建提交。

### 获取存储库的状态

Git 有一些很好的命令可以查看存储库的状态。

其中最重要的是`git status`. 随时运行它以查看 Git 看到的哪些文件已被修改且仍处于未暂存状态，以及哪些文件已被修改和暂存（这样，如果您`git commit`将这些更改包含在提交中）。

当您有未暂存的更改时，您可以通过运行来查看更改内容（相对于上次提交）`git diff`。

请注意，这*不*包括已暂存（但未提交）的更改。当然，你还可以通过运行来`git diff --staged`查看这些。**如下所示，我刚开始`git diff`和`git diff --staged`是什么都看不到的，直到我将所有修改都add之后，通过`git diff --staged`就可以看到了**

![image-20221111190459330](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202211111904372.png)

### Push

在您进行了一些提交之后，您需要将它们推送到远程存储库。在 6.031 中，您应该只有一个可以推送到的远程存储库，称为`origin`. 要推送它，请运行以下命令：

```
git push origin main
```

**命令中的`origin`指定您正在推送到`origin`远程，也就是意味着，您在哪克隆的远程存储库，就通过`origin`来声明推送回那个远程存储库。**

**`main`指的是分支`main`，我们 Git 存储库中的默认分支。我们不会使用`main`6.031 以外的分支。我们所有的提交都将 on `main`，这就是我们要推送的分支。**

运行此程序后，系统将提示您输入密码，希望一切都会推送。你会得到这样的一行：

```
a67cc45..b4db9b0  main -> main
```

###  Merge

有时，当您尝试推动时，事情会出错。你可能会得到这样的输出：

```
! [rejected]      main -> main (non-fast-forward)
```

这里发生的事情是 Git 不会让你推送到存储库，除非你的所有提交都在远程存储库中已经存在的所有提交之后。**如果您收到这样的错误消息，则意味着您的远程存储库中有一个您在本地存储库中没有的提交（在项目中，可能是因为队友在您之前推送了）。如果您发现自己处于这种情况，则必须先pull，然后再push。**

### Pull

要执行拉动，您应该运行`git pull`. 当你运行它时，Git 实际上做了两件事：

1. 它下载更改并将它们存储在其内部状态中。此时，存储库看起来并没有什么不同，但它知道远程存储库的状态是什么，以及您本地存储库的状态是什么。
2. 它通过合并将远程存储库中的更改*合并*到本地存储库中，**如下所述。**

###  合并（无冲突）

如果您对存储库进行了一些更改，并且您正在尝试合并来自另一个存储库的更改，那么您需要以某种方式将它们合并在一起。在提交方面，实际需要发生的是您必须创建一个特殊的*合并提交*来结合这两个更改。这个过程如何实际发生取决于变化。

**如果幸运的话，您所做的更改和从远程存储库下载的更改不会发生冲突。例如，也许您更改了一个文件，而您的项目合作伙伴更改了另一个文件。在这种情况下，只包含这两个更改是安全的。**

**同样，也许您更改了同一文件的不同部分。在这些情况下，Git 可以自动进行合并。在这种情况下，当你运行时`git pull`，它会弹出一个编辑器，就像你在进行提交一样：这是 Git 自动生成的合并提交的提交消息。保存并关闭此编辑器后，将进行合并提交，您将合并这两项更改。此时，您可以再试`git push`一次。**

### 合并冲突

有时候，你没那么幸运。如果您所做的更改和您提取的更改编辑了同一文件的同一部分，Git 将不知道如何解决它。这称为*合并冲突*。在这种情况下，您将得到一个`CONFLICT`大写字母的输出。如果您运行`git status`，它将显示带有标签的冲突文件`Both modified`。您现在必须编辑这些文件并手动解决它们。

首先，在 Eclipse 中打开文件。有冲突的部分会很明显地用讨厌`<<<<<<<<<<<<<<<<<<`的 , `==================`, 和`>>>>>>>>>>>>>>>>>>`线条来标记。`<<<<`和`====`之间的所有内容都是您所做的更改。`====`和`>>>>`线之间的所有内容都是您git pull所引入的更改。您的工作是弄清楚如何将它们结合起来。答案当然要视情况而定。也许一个变化在逻辑上取代了另一个，或者它们可以以某种方式合并。**您应该对文件进行满意的编辑，并在完成后删除`<<<<`/ `====`/`>>>>`标记。**

一旦解决了所有冲突（请注意，可能有几个冲突文件，每个文件也可能有几个冲突），**`git add`所有受影响的文件，然后`git commit`. 您将有机会编写合并提交消息（您应该在其中描述您是如何进行合并的）。现在你应该可以push了。**

### 避免合并和合并冲突：开始工作前记住先git pull

在你开始工作之前，**总是`git pull`**。这样，您将使用最新版本的代码，并且以后不必执行合并的可能性较小。

我们将在以后的课程中重温 Git 并了解有关版本控制的更多信息。如果您已经安装了软件、设置了 Eclipse 并完成了上面的 GitStream 练习，那么您就可以继续进行[问题集 0](http://web.mit.edu/6.031/www/sp21/psets/ps0/)了。

### 在 6.031 玩得开心！