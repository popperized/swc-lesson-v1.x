---
title: "Archiving and DOIs"
teaching: 0
exercises: 0
questions:
- 'How can I archive and obtain DOIs for my project?'
objectives:
- ""
keypoints:
- "First key point."
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

To archive and generate a DOI for your repository, after committing to 
Git all your changes, do the following:

```bash
export POPPER_GITHUB_ZENODO_API_TOKEN=<your-token>
popper archive --service zenodo
```

where `<your-token>` is the token you obtained in the steps outlined 
above. After this executes, you will have a DOI available for your 
repository that you can use to reference your work.
