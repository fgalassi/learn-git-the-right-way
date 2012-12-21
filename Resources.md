# Git Resources

## People
If you find something written by these people, read it.
* Scott Chacon
 * GitHubber particularly keen on git education. Author of "Pro Git".
* Tom Preston-Werner (mojombo).
 * Github founder. The Git Parable author.
* Jakub Narebski
 * Git committer extremely knowledgeable, kind and vocal in the git community
   (stack overflow, hacker news, mailing lists, etc..).
* Tim Berglund
 * Git trainer for github. Does it professionally, good. Tons of stuff. O'reilly
   master class.

## The DAG
The DAG is the graph of commit objects plus references (branches) to points of
development, that make up a Git repository. Important to understand history and
branching.
* "Pro Git" book. Chapter 9 "Git internals"
 * by Scott Chacon
 * Details of DAG objects, references and more.
 * http://git-scm.com/book
* "The Git Parable" post
 * by Tom Preston-Werner
 * Git design decisions explained with a sweet parable. Almost non-technical.
 * http://tom.preston-werner.com/2009/05/19/the-git-parable.html
* "Unlocking the secrets of Git" talk video
 * by Tom Preston-Werner
 * Mostly same contents of the parable but with details and on the real thing.
 * http://sea.ucar.edu/event/unlocking-secrets-git
* "Git Internals" ebook. "Understanding Git" part
 * by Scott Chacon for PeepCode
 * Very nice explanation of the DAG. Much visual with lots of diagrams.
 * https://peepcode.com/products/git-internals-pdf
* "Git Plumbing" presentation
 * by Scott Chacon
 * Low level git commands to manipulate the DAG
 * https://github.com/schacon/git-plumbing-preso

# The 3 Threes: working dir, index, HEAD
Trees here means file system trees made up of directories and files. These are
the tree of files you're working on, the tree of files in your next commit and
the tree of files in your last commit. You can explain almost all git commands
in terms of these.
* "Reset Demystified" post
 * by Scott Chacon
 * Enlightening post about the nature of these trees and their relationship
 * http://git-scm.com/2011/07/11/reset.html
* "A Tale of Three Threes" talk video
 * by Scott Chacon
 * A later and much more detailed shoot at the topic
 * slides: https://speakerdeck.com/schacon/a-tale-of-three-trees
 * video: http://www.infoq.com/presentations/A-Tale-of-Three-Trees

# Remotes
Remotes are a way to point to other repositories. Refspecs are another important
concept used to map local to remote references back and forth. Remote tracking
branches are local branches mirroring remote branches. Fetch, Push, Pull are the
commands that do the magic.
* Not found anything really compelling about this stuff
* You can peruse git help for fetch, pull and push

# Generic stuff
* "Pro Git" book
 * Best overall book.
* http://git-scm.com/
 * Best site with resources
* http://gitref.org/
 * Good reference
* Github
 * Best git hosting

# History of Git
* http://en.wikipedia.org/wiki/Git\_(software)
* Linus Torvalds on git http://www.youtube.com/watch?v=4XpnKHJAok8 
* https://git.wiki.kernel.org/index.php/GitHistory

# Technical Stuff
* Difference between tracking files (csv) and trees (git)
 * http://stackoverflow.com/questions/7094726/what-are-the-underlying-git-merge-processes-within-the-staging-area
* Recursive merge strategy explained
 * http://codicesoftware.blogspot.com/2011/09/merge-recursive-strategy.html
