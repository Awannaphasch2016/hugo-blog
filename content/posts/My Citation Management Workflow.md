+++
title = "My Citation Management Workflow."
author = ["Anak Wannaphaschaiyong"]
tags = ["citation", "blog"]
draft = false
+++

there are three categories of note taking process

1.  organize files.
2.  write notes on a file.
3.  search files and notes (aka completion in emacs)
4.  organize notes reference to file.

First two are easy to achieve. Put notes and pdf files in folders does the job.
The third condition is arguably not difficult neither. One can search for a file given a file directory quickly which can be done with any of the completion packages (e.g. `ivy`, `helm`, `vertico`) or project management package. (e.g. `projectile`)

The hard (confusing) part is organize notes reference to file. When I says organize notes references, I don't just mean organize collection of citations. What I really mean is to link .bib to PDF file and its notes.

The last part is where advantage of Emacs come to bite me. (This definitely wasn't the first time.)
Emacs are known to be hack-able and extensible. It can be extended to do variety of things. As a results, people invented tools to do the same things in different ways.

Consider this. to make references we need three things; citations, physical files, and notes.
In reality, there are more than one way in which order of the three are retrieved. For example,
citation -&gt; physical file -&gt; note or note -&gt; physical file -&gt; citation.
Now, each of the step can be done in various ways, says, one can manually put citation then later download PDF file (notice that there is no connection between PDF and citation) or, maybe, one can download PDF with Zotero which automatically download citation for you. In the later, there are connection between citation and PDF but Zotero may make mistake about the title of PDF, hence, prevent a file to be searchable by name. (condition 3. search files and notes)

How can we establish consistency between these steps such that we can establish connection between physical files, notes, and citations?


## Establish Standard {#establish-standard}

First thing that come to mind is "standardization." We must enforce certain rules to reduce possible inconsistency.

1.  citation must follow the same convention e.g. author's lastname followed by year.
2.  PDF must be able to search by citation convention establish in point 1.
3.  citation must contains a file key whose value is file location.

The idea of the above standard is to

1.  embed information about file location inside citation entry.
2.  embed information about citation inside note.

With above standard, we guarantee relation as a directed acyclic graph (DAG). In my opinion, this is the safest type of graph we can have to functions required to navigate between components will fail due to faulty of a graph.

We get the following DAG

```nil
FILE <-> citation <-> note
```

Since travel from note can reach FILE, one can implement a function to open FILE from inside the note.


## Utilizing existing packages {#utilizing-existing-packages}

Lets focus our attention back to ours tools to achieve this task.

```nil
citation <-> note
```

Using `citar-open-entry`, we can searches citation from `citar-bibliography`, a .bib file which contains collections of citations. Since we made this connection, citation insertion or jump from citation mentioned in a note to citation entry in `citar-bibliogrpahy` is possible.

By default, if note doesn't yet exist, `citar-open-notes` created a new file with name `[id][file-title].org` and, inside the org file, it produce ID property and ROAM_REFS property whose value is citation link to `citar-bibliography` with file's name as a title of the note file.

```nil
FILE <-> citation
```

I was having a problem open file from citation using citar. I has since found and fixed the problem. To put it simply,

citar looks into citation entry and find entry "file" then simply use this information to open a file. I have check that value contains a valid file path.

Since I am using WSL2, I have to be careful when export citation from Zotero. I run Emacs on Ubuntu in WSL2 which is equivalent of Emacs running on Ubuntu, therefore, it can't understand window file path. Example of window file path generated from Zotero.

```nil
file = {C\:\\Users\\terng\\Zotero\\storage\\37L2SIXA\\Kazemi et al. - Representation Learning for Dynamic Graphs A Surv.pdf}
```

I have to first change file path to valid file path in Linux convention.

```nil
file = {/mnt/c/Users/terng/Zotero/storage/37L2SIXA/Kazemi et al. - Representation Learning for Dynamic Graphs A Surv.pdf}
```


## Bonus {#bonus}

note: Since I have fixed a bug to open allow me to open a file from its citation. I no longer need org-noter as an essential component. Nonetheless, org-noter is still a viable annotator tools. <span class="timestamp-wrapper"><span class="timestamp">&lt;2022-03-12 Sat&gt;</span></span>

Org-noter is an interesting one. It is implemented as a document annotator, so it has no built-in capability to make connection to citation. It is interesting because it allowed the direct connection between FILE and notes. which is not a design that I intended to achieve.

```nil
FILE <-> note
```

Org-noter helps me solve `FILE <-> citation` problem I mentioned earlier.
To fit org-noter in my workflow, I only have an option to open a note first then connect note to a file. Org noter allows one to connect to a note from PDF, but file name must be selected from a fixed options. Since I want flexibility to choose file name, I can't use the later option.
