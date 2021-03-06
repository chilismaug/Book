# Why Do You Need Code Review Tools?

There is a simple and straightforward way to improve the quality of your code,
pay of some of your technical debt, teach the new members of your team and keep
everyone up to date about what is happening in the project. As you might have
guessed, you just have to start doing regular code reviews. It is that easy.

As outlined in multiple publications, of which I will just mention here the
"Best Kept Secrets of Peer Code Review" by J. Cohen, S. Teleki and E. Brown,
code review can greatly lower the overall cost of development, mostly by
decreasing the number of defects that make their way into later stages of
development, by catching them early. Of course that is just a single benefit,
one that is relatively easy to measure, and one that speaks to the management
best. But there are multiple other benefits for the team and the clients. In
short, you really want to have code reviews.

However, those benefits do come at a cost. Properly performing a formal code
review (or code inspection, how it is often called) requires preparation, skill
and training. The time spent on review has to come from somewhere, and it
usually comes from the time normally used to write that code in the first
place. And you can't just have a dedicated, less skilled person hired specially
to do it -- it has to be the same programmers who are actually writing that
code in the first place -- otherwise you do not get those benefits.

Another problem is that many programmers don't like doing it, and will complain
loudly when forced. After all, they are here to write code, not to sit in
endless meetings. And having your code dissected and publicly analyzed is not
necessarily very pleasant for people with large egos, of whom there are plenty
in this profession. So you will have some resistance here too.

In open source projects that are being developed by volunteers it's even worse
than that. If you force the contributors to jump through too many hoops, they
will just go to some other project that makes better (in their opinion) use of
their time, or do something entirely different than programming.

Fortunately, as many social problems do, this one also has a simple technical
solution. You can minimize the time spent on preparation to code review, guide
the programmers through the review process, so that they don't need special
training, and still keep the experience engaging and pleasant, by using
specialized software. In addition to that, in open source projects, you may
even attract users who don't feel confident enough to write code, but are happy
to review the submitted patches and gradually learn more about the project and
become regular contributors.

A typical code review software lets you submit a patch or a series of patches
with a simple command, usually added as a plugin to your version control
system. Once submitted, the patch appears on a list, and optionally the people
responsible for the project receive notifications. You can also explicitly add
certain people to the review, if you believe they should look at the code
before it is accepted. Programmers can then review the patch by looking at the
changes in context of the whole program, and can also check the modified
version of the program to analyze and test it at run time. They can then easily
comment on the whole patch, individual files or even individual lines of code.
It is common for those comments to grow into whole discussions, especially when
the change being discussed is not particularly important. New versions of the
change can be uploaded for review as the comments are addressed -- either by
the original author, or by anyone else. Finally, after set criteria are met
(enough of the right people voice their approval), the change is accepted. The
criteria may differ depending on the process used in the given project, and the
code may even be merged into the project already or only after acceptance.
Different projects have different styles and the tools are usually flexible
enough to account for that.

The review process is also an excellent place for plugging all sorts of code
analysis and continuous integration tools. If you care about the style of the
code being written, add a linter in there. If you have automated tests, have
them run on each submitted change and attach the result to the patch. Finally,
if you care about certain metrics, this is the place where it's the easiest to
measure them. You can, for instance, tell exactly how much time the programmers
are spending on code review and whether it's worth the increased code quality.

This place is also perfect for adding other sorts of automation. Greeting new
contributors and pointing them to guidelines. Informing programmers about code
freezes. Linking the patches to the information in the bugtracker, and vice
versa. Informing translators and documentation writers about important changes.
And so on -- the possibilities are countless, and each of them saves someone on
your team some time and makes somebody's life easier -- perhaps even enough
time is saved to account for the extra time spent on reviewing the code.

Finally, reviewing the code becomes a much easier and smaller task. You can
review a simple patch in a matter of minutes or even seconds. Certain classes
of bugs are immediately visible even to the original author -- it's common to
re-submit a fixed patch even before anybody else looked at it. Of course,
large, complex, distributed changes are still hard do review, in particular
when they require complicated and specialized environment to test. This didn't
change, and that's why you still need to have your QA team and tests.

For open source project there is an additional benefit. If you make the code
review tool public (and there is no reason why you shouldn't, especially when
you handle security-sensitive patches separately), you suddenly have a great
way to attract, guide and teach newcomers to your project. The tool guides them
through the process, the programmers guide them through the good practices used
in that particular language or project, and they even learn by reading reviews
of patches submitted by other people.

It is possible to achieve some part of that using other tools, or just by
manually following an agreed upon process, but that has considerable drawbacks.
The main drawback is the greater effort required to get through all the hoops.
While experienced members of the team who are used to the process might not
even notice the wasted time, it does become a big problem for beginners and
sporadic contributors. For instance, the Linux kernel community is known for
using e-mail to exchange the patches for code review. What they don't tell you
is that the reviewers themselves have their own tools and script that automate
large part of the process, but are not easily accessible for anyone else.

The CPython project still uses a bug tracker to collect and review the
contributions. At least officially, because in reality a lot of the review
process actually happens out-of-band, through alternate means, such as
discussions on the IRC channels or face-to-face, e-mails, pastebins, etc.  In
fact, it's almost impossible to have one's patch merged by just following the
official process. That is a huge barrier to potential new contributors,
especially if they represent minorities or find it hard to socialize with the
development team for other reasons.

On the other hand, the OpenStack project uses a transparent, public code review
system for its sub-projects. Anybody can jump in any time and start reading the
submitted patches, their comments, and add comments of their own, potentially
catching errors that other reviewers missed. They also become more familiar
with the project and more likely to start contributing themselves. A huge win
for the project.

And what about your project? Do you think it would use some improvements in the
quality of its code, reduction in the number of bugs that get to production and
overall improvement and growth of its community? If you do, please start using
a code review tool, it may be as simple as creating a repository in one of the
popular code hosting services!
