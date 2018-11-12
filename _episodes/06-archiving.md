---
title: "Archiving and DOIs"
teaching: 15
exercises: 0
questions:
- 'How can I archive and obtain DOIs for my project?'
objectives:
- "Show how the `popper` command can be used to upload a snapshot of 
  our repository."
keypoints:
- "Not all the files in a repository can be added to Git, especially 
  if they are large."
- "In addition, input and output files that are part of a particular 
  execution of a pipeline might be better placed elsewhere."
- "The `popper` command integrates with Zenodo and Figshare, two 
  populare archiving services that can be used to upload large(ish) 
  files."
- "In addition, this functionality allows us to publish archives and 
  obtain a DOI for the archive associated to our project."
---

At some point during our research, we will likely reach a milestone 
and will likely want to pin or "timestamp" our project so that we can 
reference it from manuscripts, web content, social media, etc. While 
Github can be used for this purpose (i.e. use link to a particular 
commit in our repository), archival services fulfill this 
necessity and make stronger guarantees on the long-term preservation 
of data. Popular services include [Zenodo](https://zenodo.org), 
[Figshare](https://figshare.com),  [Dryad](https://datadryad.org), 
[Dataverse](https://dataverse.org/), among [many 
others](https://www.nature.com/sdata/policies/repositories). Library 
services from your institution might provide with such services.

The Popper CLI tool integrates with some of these services. So far, we 
have support for Zenodo and are currently working to add more 
services. To get started, we need to create an account on Zenodo and 
generate an API token so that the `popper` command can authenticate 
with the service. To do so, follow these steps (copied from 
[here](http://developers.zenodo.org/#creating-a-personal-access-token)):

 1. [Register](https://zenodo.org/signup) for a Zenodo account if you 
    don’t already have one.
 2. Go to your 
    [Applications](https://zenodo.org/account/settings/applications/), 
    to create a [new 
    token](https://zenodo.org/account/settings/applications/tokens/new/).
 3. Select the OAuth scopes you need (you need at least 
    `deposit:write` and `deposit:actions`).

To archive and generate a DOI for your repository, we first add 
metadata associated to our repository:

```
popper metadata --add title='Your Title'
popper metadata --add author1='First Last, first.last@gmail.com, Affiliation'
popper metadata --add abstract='A short description of the your repo'
popper metadata --add keywords='comma, separated, keywords'
```

The above needs to be modified to reflect the actual information 
related to your repository. After adding the above metadata values and 
committing to Git the changes, do the following:

```bash
export POPPER_ZENODO_API_TOKEN=<your-token>
popper archive --service zenodo
```

where `<your-token>` is the token you obtained in the steps outlined 
above. After this executes, you will have a DOI available for your 
repository that you can use to reference your work.
