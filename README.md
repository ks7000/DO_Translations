Hispanohablantes [por favor hagan clic en este enlace](/LEEME.md).

# Statement of intents

The main purpose of this repository is the translation into Spanish of the tutorials published by DO. [Our website](https://www.ks7000.net.ve/), at the time of writing these lines, is hosted on virtual machines called _droplets_ by that company, and we religiously pay for our online publication. Thus, our only interest is the dissemination of knowledge and free software (our blog objective) and thus facilitate the assimilation of new technologies for our country, Venezuela.

With our job we shorten the work, thus eliminating the language barrier, taking into account the various variants that Castilian has, both in Europe and in America. As it had its origin in the Old World we make and/or review each translation first in Spanish (Spain), and then in Spanish (Venezuela).

Each article in this repository is governed by its original license:

https://creativecommons.org/licenses/by-nc-sa/4.0/

You can read the same license in Spanish (Spain) in the following link:

https://creativecommons.org/licenses/by-nc-sa/4.0/deed.es_ES

But wait there is still more! Translating by itself is a job, we give added value by reviewing the instructions and the code in each tutorial. It is extremely rare that we find any error, but we know that, when it has happened, the authors and publishers have been very solicitous and kind in acknowledging their error and have corrected it without any problem. They have also accepted proposals for improvements in the same way; We give special recognition to [Erika Heidi](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-laravel-with-lemp-on-ubuntu-18-04?comment=81516), [Kamal Nasser](https://www.digitalocean.com/community/tutorials/how-to-use-a-remote-docker-server-to-speed-up-your-workflow?comment=82401) and [Brian Boucheron](https://www.digitalocean.com/community/tutorials/how-to-set-up-time-synchronization-on-debian-10?comment=81504), to name only three specific cases.

## Additional considerations

The Castilian language is, unlike the English language, extensive, broad in verbal conjugations and extremely sensitive to redundancies (in fact apologies are offered when we pronounce them, to which our listeners jokingly reply with «forgive the braying» ("redundancia" sounds like "rebuznancia" in Spanish) -¿ what fault do these poor animals always have to bray in the same way, again and again, in a row? -) We prefer to perceive it as a language inclined more towards poetry than towards prose and collides head-on with technical language, so our effort to carry out this work.

If that is not enough reason, we add another: redundancy in translations does not offer a mnemonic handhold, making it difficult to remember the paragraphs. It is better to explore them and associate them with different synonyms and verbs, even if they express the same orders.

## Work method

There are many ways to work in distributed environments with Git, as [Scott Chacon explains in his book "Pro Git 2"](https://git-scm.com/book/es/v2/Git-en-entornos-distribuidos-Flujos-de-trabajo-distribuidos). We have simply chosen to have a main branch (called main) with the necessary presentation, license and code files to automate the work, just that :sparkles:.

For each tutorial (we also call it an **article** or **publication**) we open a branch whose name is the [semantic URL (slug)](https://en.wikipedia.org/wiki/Clean_URL) of the original publication. The Python language is the one selected for:

* Download the content of the article and save with said semantic URL but in [MarkDown format, GitHub version](https://guides.github.com/features/mastering-markdown/) :octocat: and make a commit.
* If the publication already has Spanish translation, copy the previous file with the semantic URL in Spanish as a name and perform a commit.
* Download the official translation and save it in the file of the previous step (overwrite) and perform a commit.
* Copy the official translation by adding to the semantic URL the suffix "-ve" to mean Spanish from Venezuela.
* Make on this last file the necessary changes for the best understanding in our country of the tutorial in question.

These branches, which as we said each one is an article, are not and will not be merged into the main one and we only publish the instructions and the code necessary to make a fork fork, merge them and convert them into HTML in order to publish them without having to have a base of data as a content handler (so, in fact, this repository is the content handler).

## Project structure

We follow the recommendations of mr. Kenneth Reitz about the components and practices necessary for the Python language.
