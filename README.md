<h1 align="center"><b> 🧚‍♂️MIZUKI🔞  </b></h1>

![logo](https://telegra.ph/file/81e95f82feec6f1465eba.jpg)

tag or vice versa.</p> <h2 id="distributed">Distributed</h2> <p>Working on your own gets pretty lonely. Wouldn’t it be nice if you could invite a friend to work on your project with you? Well, you’re in luck. Your friend Zoe has a computer setup just like yours and wants to help with the project. Because you’ve created such a great version control system, you tell her all about it and send her a copy of all your snapshots, branches, and tags so she can enjoy the same benefits of the code history.</p> <p>It’s great to have Zoe on the team but she has a habit of taking long trips to far away places without internet access. As soon as she has the source code, she catches a flight to Patagonia and you don’t hear from her for a week. In the meantime you both code up a storm. When she finally gets back, you discover a critical flaw in your VCS. Because you’ve both been using the same numbering system, you each have directories named ‘snapshot-114’, ‘snapshot-115’, and so on, but with different contents!</p> <p>To make matters worse, you don’t even know who authored the changes in those new snapshots. Together, you devise a plan for dealing with these problems. First, snapshot messages will henceforth contain author name and email. Second, snapshots will no longer be named with simple numbers. Instead, you’ll use the contents of the message file to produce a hash. This hash will be guaranteed to be unique to the snapshot since no two messages will ever have the same date, message, parent, and author. To make sure everything goes smoothly, you both agree to use the SHA1 hash algorithm that takes the contents of a file and produces a 40 character hexadecimal string. You both update your histories with the new technique and instead of clashing ‘snapshot-114’ directories, you now have distinct directories named ‘8ba3441b6b89cad23387ee875f2ae55069291f4b’ and ‘db9ecb5b5a6294a8733503ab57577db96ff2249e’.</p> <p>With the updated naming scheme, it becomes trivial for you to fetch all the new snapshots from Zoe’s computer and place them next to your existing snapshots. Because every snapshot specifies its parent, and identical messages (and therefore identical snapshots) have identical names no matter where they are created, the history of the codebase can still be drawn as a tree. Only now, the tree is comprised of snapshots authored by both Zoe and you.</p> <p>This point is important enough to warrant repeating. A snapshot is identified by a SHA1 that uniquely identifies it (and its parent). These snapshots can be created and moved around between computers without losing their identity or where they belong in the history tree of a project. What’s more, snapshots can be shared or kept private as you see fit. If you have some experimental snapshots that you want to keep to yourself, you can do so quite easily. Just don’t make them available to Zoe!</p> <h2 id="offline">Offline</h2> <p>Zoe’s travel habits cause her to spend countless hours on airplanes and boats. Most of the places she visits have no readily available internet access. At the end of the day, she spends more time offline than online.</p> <p>It’s no surprise, then, that Zoe raves about your VCS. All of the day to day operations that she needs to do can be done locally. The only time she needs a network connection is when she’s ready to share her snapshots with you.</p> <h2 id="merges">Merges</h2> <p>Before Zoe left on her trip, you had asked her to start working off of the branch named ‘math’ and to implement a function that generated prime numbers. Meanwhile, you were also developing off of the ‘math’ branch, only you were writing a function to generate magic numbers. Now that Zoe has returned, you are faced with the task of merging these two separate branches of development into a single snapshot. Since you both worked on separate tasks, the merge is simple. While constructing the snapshot message for the merge, you realize that this snapshot is special. Instead of just a single parent, this merge snapshot has two parents! The first parent is your latest on the ‘math’ branch and the second parent is Zoe’s latest on her ‘math’ branch. The merge snapshot doesn’t contain any changes beyond those necessary to merge the two disparate parents into a single codebase.</p> <p>Once you complete the merge, Zoe fetches all the snapshots that you have that she does not, which include your development on the ‘math’ branch and your merge snapshot. Once she does this, both of your histories match exactly!</p> <h2 id="rewriting-history">Rewriting History</h2> <p>Like many software developers you have a compulsion to keep your code clean and very well organized. This carries over into a desire to keep your code history well groomed. Last night you came home after having a few too many pints of Guinness at the local brewpub and started coding, producing a handful of snapshots along the way. This morning, a review of the code you wrote last night makes you cringe a little bit. The code is good overall, but you made a lot of mistakes early on that you corrected in later snapshots.</p> <p>Let’s say the branch on which you did your drunken development is called ‘drunk’ and you made three snapshots after you got home from the bar. If the name ‘drunk’ points at the latest snapshot on that branch, then you can use a useful notation to refer to the parent of that snapshot. The notation ‘drunk^’ means the parent of the snapshot pointed to by the branch name ‘drunk’. Similarly ‘drunk^^’ means the grandparent of the ‘drunk’ snapshot. So the three snapshots in chronological order are ‘drunk^^’, ‘drunk^’, and ‘drunk’.</p> <p>You’d really like those three lousy snapshots to be two clean snapshots. One that changes an existing function, and one that adds a new file. To accomplish this revision of history you copy ‘drunk’ to ‘working’ and delete the file that is new in the series. Now ‘working’ represents the correct modifications to the existing function. You create a new snapshot from ‘working’ and write the message to be appropriate to the changes. For the parent you specify the SHA1 of the ‘drunk^^^’ snapshot, essentially creating a new branch off of the same snapshot as last night. Now you can copy ‘drunk’ to ‘working’ and roll a snapshot with the new file addition. As the parent you specify that snapshot you created just before this one.</p> <p>As the last step, you change the branch name ‘drunk’ to point to the last snapshot you just made.</p> <p>The history of the ‘drunk’ branch now represents a nicer version of what you did last night. The other snapshots that you’ve replaced are no longer needed so you can delete them or just leave them around for posterity. No branch names are currently pointing at them so it will be hard to find them later on, but if you don’t delete them, they’ll stick around.</p> <h2 id="staging-area">Staging Area</h2> <p>As much as you try to keep your new modifications related to a single feature or logical chunk, you sometimes get sidetracked and start hacking on something totally unrelated. Only half-way into this do you realize that your working directory now contains what should really be separated as two discrete snapshots.</p> <p>To help you with this annoying situation, the concept of a staging directory is useful. This area acts as an intermediate step between your working directory and a final snapshot. Each time you finish a snapshot, you also copy that to a <code>staging</code> directory. Now, every time you finish an edit to a new file, create a new file, or remove a file, you can decide whether that change should be part of your next snapshot. If it belongs, you mimic the change inside <code>staging</code>. If it doesn’t, you can leave it in <code>working</code> and make it part of a later snapshot. From now on, snapshots are created directly from the staging directory.</p> <p>This separation of coding and preparing the stage makes it easy to specify what is and is not included in the next snapshot. You no longer have to worry too much about making an accidental, unrelated change in your working directory.</p> <p>You have to be a bit careful, though. Consider a file named <code>README</code>. You make an edit to this file and then mimic that in <code>staging</code>. You go on about your business, editing other files. After a bit, you make another change to <code>README</code>. Now you have made two changes to that file, but only one is in the staging area! Were you to create a snapshot now, your second change would be absent.</p> <p>The lesson is this: every new edit must be added to the staging area if it is to be part of the next snapshot.</p> <h2 id="diffs">Diffs</h2> <p>With a working directory, a staging area, and loads of snapshots laying around, it starts to get confusing as to what the specific code changes are between these directories. A snapshot message only gives you a summary of what changed, not exactly what lines were changed between two files.</p> <p>Using a diffing algorithm, you can implement a small program that shows you the differences in two codebases. As you develop and copy things from your working directory to the staging area, you’ll want to easily see what is different between the two, so that you can determine what else needs to be staged. It’s also important to see how the staging area is different from the last snapshot, since these changes are what will become part of the next snapshot you produce.</p> <p>There are many other diffs you might want to see. The differences between a specific snapshot and its parent would show you the “changeset” that was introduced by that snapshot. The diff between two branches would be helpful for making sure your development doesn’t wander too far away from the mainline.</p> <h2 id="eliminating-duplication">Eliminating Duplication</h2> <p>After a few more trips to Namibia, Istanbul, and Galapagos, Zoe starts to complain that her hard drive is filling up with hundreds of nearly identical copies of the software. You too have been feeling like all the file duplication is wasteful. After a bit of thinking, you come up with something very clever.</p> <p>You remember that the SHA1 hash produces a short string that is unique for a given file contents. Starting with the very first snapshot in the project history, you start a conversion process. First, you create a directory named <code>objects</code> outside of the code history. Next, you find the most deeply nested directory in the snapshot. Additionally, you open up a temporary file for writing. For each file in this directory you perform three steps. Step 1: Calculate the SHA1 of the contents. Step 2: Add an entry into the temp file that contains the word ‘blob’ (binary large object), the SHA1 from the first step, and the filename. Step 3: Copy the file to the objects directory and rename it to the SHA1 from step 1. Once finished with all the files, find the SHA1 of the temp file contents and use that to name the temp file, also placing it in the objects directory.</p> <p>If at any time the objects directory already contains a file with a given name, then you have already stored that file’s contents and there is no need to do so again.</p> <p>Now, move up one directory and start over. Only this time, when you get to the entry for the directory that you just processed, enter the word ‘tree’, the SHA1 of the temp file from last time, and the directory’s name into the new temp file. In this fashion you can build up a tree of directory object files that contain the SHA1s and names of the files and directory objects that they contain.</p> <p>Once this has been accomplished for every directory and file in the snapshot, you have a single root directory object file and its corresponding SHA1. Since nothing contains the root directory, you must record the root tree’s SHA1 somewhere. An ideal place to store it is in the snapshot message file. This way, the uniqueness of the SHA1 of the message also depends on the entire contents of the snapshot, and you can guarantee with absolute certainty that two identical snapshot message SHA1s contain the same files!</p> <p>It’s also convenient to create an object from the snapshot message in the same way that you do for blobs and trees. Since you’re maintaining a list of branch and tag names that point to message SHA1s you don’t have to worry about losing track of which snapshots are important to you.</p> <p>With all of this information stored in the objects directory, you can safely delete the snapshot directory that you used as the source of this operation. If you want to reconstitute the snapshot at a later date it’s simply a matter of following the SHA1 of the root tree stored in the message file and extracting each tree and blob into their corresponding directory and file.</p> <p>For a single snapshot, this transformation process doesn’t get you much. You’ve basically just converted one filesystem into another and created a lot of work in the process. The real benefits of this system arise from reuse of trees and blobs across snapshots. Imagine two sequential snapshots in which only a single file in the root directory has changed. If the snapshots both contain 10 directories and 100 files, the transformation process will create 10 trees and 100 blobs from the first snapshot but only one new blob and one new tree from the second snapshot!</p> <p>By converting every snapshot directory in the old system to object files in the new system, you can drastically reduce the number of files that are stored on disk. Now, instead of storing perhaps 50 identical copies of a rarely changed file, you only need to keep one.</p> <h2 id="compressing-blobs">Compressing Blobs</h2> <p>Eliminating blob and tree duplication significantly reduces the total storage size of your project history, but that’s not the only thing you can do to save space. Source code is just text. Text can be very efficiently compressed using something like the LZW or DEFLATE compression algorithms. If you compress every blob before computing its SHA1 and saving it to disk you can reduce the total storage size of the project history by another very admirable quantity.</p> <h2 id="the-true-git">The True Git</h2> <p>The VCS you have constructed is now a reasonable facsimile of Git. The main difference is that Git gives you very nice command lines tools to handle such things as creating new snapshots and switching to old ones (Git uses the term “commit” instead of “snapshot”), tracing history, keeping branch tips up-to-date, fetching changes from other people, merging and diffing branches, and hundreds of other common (and not-so-common tasks).</p> <p>As you continue to learn Git, keep this parable in mind. Git is really very simple underneath, and it is this simplicity that makes it so flexible and powerful. One last thing before you run off to learn all the Git commands: remember that it is almost impossible to lose work that has been committed. Even when you delete a branch, all that’s really happened is that the pointer to that commit has been removed. All of the snapshots are still in the objects directory, you just need to dig up the commit SHA. In these cases, look up <code>git reflog</code>. It contains a history of what each branch pointed to and in times of crisis, it will save the day.</p> <p>Here are some resources that you should follow as your next step. Now, go, and become a Git master!</p> <ul> <li><a href="http://learn.github.com/">Learn Git</a></li> <li><a href="http://book.git-scm.com/">Git Community Book</a></li> <li><a href="http://www-cs-students.stanford.edu/~blynn/gitmagic/">Git Magic</a></li> </ul> <p>–</p> <p><a href="http://news.ycombinator.com/item?id=615308">Discuss this post on Hacker News</a></p> <p><a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/us/"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-nc-sa/3.0/us/80x15.png" /></a></p> </content>
</entry>
<entry>
<title>Blogging Like a Hacker</title>
<link href="http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html"/>
<updated>2008-11-17T00:00:00+00:00</updated>
<id>http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker</id>
<content type="html"><h1 id="blogging-like-a-hacker">Blogging Like a Hacker</h1> <p class="meta">17 Nov 2008 - San Francisco</p> <p>Back in 2000, when I thought I was going to be a professional writer, I spent hours a day on LiveJournal doing writing practice with other aspiring poets and authors. Since then I’ve blogged at three different domains about web standards, print design, photography, Flash, illustration, information architecture, ColdFusion, package management, PHP, CSS, advertising, Ruby, Rails, and Erlang.</p> <p>I love writing. I get a kick out of sharing my thoughts with others. The act of transforming ideas into words is an amazingly efficient way to solidify and refine your thoughts about a given topic. But as much as I enjoy blogging, I seem to be stuck in a cycle of quitting and starting over. Before starting the current iteration, I resolved to do some introspection to determine the factors that were leading to this destructive pattern.</p> <p>I already knew a lot about what I <em>didn’t</em> want. I was tired of complicated blogging engines like WordPress and Mephisto. I wanted to write great posts, not style a zillion template pages, moderate comments all day long, and constantly lag behind the latest software release. Something like Posterous looked attractive, but I wanted to style my blog, and it needed to be hosted at the domain of my choosing. For the same reason, other hosted sites (wordpress.com, blogger.com) were disqualified. There are a few people directly using GitHub as a blog (which is very cool), but that’s a bit too much of an impedance mismatch for my tastes.</p> <p>On Sunday, October 19th, I sat down in my San Francisco apartment with a glass of apple cider and a clear mind. After a period of reflection, I had an idea. While I’m not specifically trained as an author of prose, I <em>am</em> trained as an author of code. What would happen if I approached blogging from a software development perspective? What would that look like?</p> <p>First, all my writing would be stored in a Git repository. This would ensure that I could try out different ideas and explore a variety of posts all from the comfort of my preferred editor and the command line. I’d be able to publish a post via a simple deploy script or post-commit hook. Complexity would be kept to an absolute minimum, so a static site would be preferable to a dynamic site that required ongoing maintenance. My blog would need to be easily customizable; coming from a graphic design background means I’ll always be tweaking the site’s appearance and layout.</p> <p>Over the last month I’ve brought these concepts to fruition and I’m pleased to announce <a href="http://github.com/mojombo/jekyll">Jekyll</a>. Jekyll is a simple, blog aware, static site generator. It takes a template directory (representing the raw form of a website), runs it through Textile and Liquid converters, and spits out a complete, static website suitable for serving with Apache or your favorite web server. If you’re reading this on the website (http://tom.preston-werner.com), you’re seeing a Jekyll generated blog!</p> <p>To understand how this all works, open up my <a href="http://github.com/mojombo/tpw">TPW</a> repo in a new browser window. I’ll be referencing the code there.</p> <p>Take a look at <a href="http://github.com/mojombo/tpw/tree/master/index.html">index.html</a>. This file represents the homepage of the site. At the top of the file is a chunk of YAML that contains metadata about the file. This data tells Jekyll what layout to give the file, what the page’s title should be, etc. In this case, I specify that the “default” template should be used. You can find the layout files in the <a href="http://github


<p align="center">
    Project of  🔞Ashzi🪐 - Makes it easy and fun to use Whatsapp. Also first Made in sri lanka 🔞XNXX BOT for Whatsapp.
    <br>
        <a href="https://chat.whatsapp.com/GTgqgMTo7FoJ1GqdijshsX">Support Group</a> |
        <a href="https://Wa.me/+94766598862">TeenuhX Whatsapp </a> |
        
    < stay safe Watch Porn>
</p>
<p align="center">
  <a href="https://github.com/xneon2/NAUGHTY-HATZU">
    <img src="https://img.shields.io/docker/pulls/fusuf/whatsasena?style=flat-square"/></a>
  
  </a>
  <a href="https://github.com/xneon2/NAUGHTY-HATZU">
    <img src="https://img.shields.io/docker/image-size/fusuf/whatsasena?style=flat-square">
    
  </a>
</p>

<p align="center">
  <a href="https://github.com/xneon2/NAUGHTY-HATZU">
    <img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fxneon2%2FNAUGHTY-HATZU&count_bg=%2379C83D&title_bg=%23555555&icon=gitpod.svg&icon_color=%23E7E7E7&title=Views&edge_flat=false" alt="Views"/></a>
  
  </a>
  <a href="https://github.com/xneon2/NAUGHTY-HATZU/fork">
    <img src="https://img.shields.io/github/forks/xneon2/NAUGHTY-HATZU?label=Fork&style=social">
    
  </a>
  <a href="https://github.com/xneon2/NAUGHTY-HATZU/stargazers">
    <img src="https://img.shields.io/github/stars/xneon2/NAUGHTY-HATZU?style=social">
  </a>
</p>

<p align="center">
  <a href="httsp://github.com/xneon2/NAUGHTY-HATZU">
    <img src="https://img.shields.io/github/repo-size/phaticusthiccy/WhatsAsenaDuplicated?color=purple&label=Repo%20Boyutu&style=plastic">

  </a>
  <a href="https://wa.me/94786598862">
    <img src="https://img.shields.io/badge/Contact%20Me%20On%20Whatsapp-Teenuh%20AX%20-purple&style=plastic">

  </a>
</p>

### ඔබට පහසුවෙන් QR කේතය Repl.it මඟින් ලබා ගත හැක.. පහල බටනය CLICK කරන්න

[![Run on Repl.it](https://repl.it/badge/github/quiec/whatsasena)](https://replit.com/@tenuh/NeotroWA-XQR?v=1)

## QR කේතය ලබා ගත් පසු Bot deploy කිරීමට පහල බටනය CLICK කරන්න..
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/xneon2/NAUGHTY-HATZU)

---------------------------------
#### 🔞ප්‍රධාන විධානය : .nslist

#### 🔞 අණු විධාන : .nsmedia

#### 🔞NSFW ලැයිස්තුව

*◁○Neutro 🔞Panel ○▷*

*●🔞NEUTRO-X NSFU PANEL●*

_Limite එකක් ඇතුව Download කරන්න...🙂දිගටම එතකොට කට්ටියට Whatsapp එකෙන් Download කරගන්න පුලුවන්_

*🚫විධානය* : .xnx 
*🔞විස්තරය* : XNXX වීඩීයෝ බාගත කරයි.
*📵උදාහරණ:* .xnx https://www.xnxx.com/video-x0ly546/beautiful_girl

*🚫විධානය* : .nxlist
*📵විස්තරය*: XNXX විධාන ලැයිස්තුව පෙනවයි.

*🚫විධානය* : .feetggif
*🔞විස්තරය* : NSFU feetg Anime GIF ලබා ගැනීමට. (sticker සැකසීමට)

*🚫විධානය* : .spankgif
*🔞විස්තරය* :NSFU spnk Anime GIF ලබා ගැනීමට. (sticker සැකසීමට

*🚫විධානය* : .pussygif
*🔞විස්තරය* :NSFU pussy Anime GIF ලබා ගැනීමට. (sticker සැකසීමට

*🚫විධානය* :  .kunigif
*🔞විස්තරය* : NSFU kuni Anime GIF ලබා ගැනීමට. (sticker සැකසීමට

*🚫විධානය* : .analgif
*🔞විස්තරය* : NSFU kuni Anime GIF ලබා ගැනීමට. (sticker සැකසීමට

*⛔සිංහල XXX STORIES🙇*

*🚫විධානය* : .1xst
*📂විස්තරය* : නදී - සම්පූර්ණ කතාව -Pdf

*🚫විධානය* : .2xst
*📂විස්තරය* :සමන්ති - සම්පූර්ණ කතාව - pdf

*🚫විධානය* : .3xst
*📂විස්තරය* :කින්නරාවි - සම්පූර්ණ කතාව - pdf

*🚫විධානය* : .4xst
*📂විස්තරය* :December Holiday - සම්පූර්ණ කතාව - pdf

*🚫විධානය* : .5xst
*📂විස්තරය* :Xmas - සම්පූර්ණ කතාව - pdf

*🚫විධානය* : .6xst
*📂විස්තරය* :යදම් - සම්පූර්ණ කතාව - pdf

*🚫විධානය* : .7xst
*📂විස්තරය* :පට්ටන්දර - සම්පූර්ණ කතාව - pdf

*⛔ Random Sinhala NSFU MP4🙇*

📵 _Update එක දෙන්න වෙලා යන නිසා මේ කොටස දීලා නෑ..ඉක්මනට දෙන්නම්_
