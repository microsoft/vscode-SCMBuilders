# Visual Studio Code - Source Control Management

> **TIP:** Our work in progress [API documentation can be found here](https://github.com/Microsoft/vscode-docs/blob/vnext/docs/extensionAPI/api-scm.md).


## TL;DR
Welcome, if you have ever wanted to add an additional source code management (SMC) system to VS Code then you have landed in the right place.  

Here you will find [instructions](instructions.md) on how to create a provider incl. an [API Overview](api-overview.md), pointers to [sample code](https://github.com/Microsoft/vscode-SCMBuilders/wiki), a [list of others] working on providers, and be able to [get help](https://github.com/Microsoft/vscode-SCMBuilders/issues) from the development team.

## Background & Rationale
From day 1 VS Code shipped with [integrated Git support](http://code.visualstudio.com/docs/editor/versioncontrol) but of course not everyone is a Git user.  Right from our initial launch one of the most requested features has been adding a [plugable SCM provider](https://github.com/Microsoft/vscode/issues/2824) model - which would enable other SCM systems to be fully integrated e.g. [Subversion](https://github.com/Microsoft/vscode/issues/206), [Mecurial](https://github.com/Microsoft/vscode/issues/205).

## What's Possible via the API
The short answer is that _anything_ that you could do as a user in the Integrated Git tooling has been exposed as an API.  This includes:

* Committing/Checking in files
* Status bar notifications and actions
* Diffing files (full diff and partial, in-line and side-by-side)
* Change branches/tags
* Conflict resolution
* Full CLI interactions/output visible

Review our documentation page to get an [overview of the Git feature set](http://code.visualstudio.com/docs/editor/versioncontrol) including screen grabs...


## Why Now - Are We Ready
Over the last few months we have been working on creating an extension point in VS Code for this purpose.  Our approach was to ensure that we had a very stable and fully featured API before reaching our to the community.  

We achieved that by [moving our Integrated Git support](https://github.com/Microsoft/vscode/tree/master/extensions/git) over to this model and by working with the Visual Studio Team Services team to add [Team Foundation Version Control (TFVC)](https://github.com/Microsoft/vsts-vscode/tree/master/src/tfvc) support.  

Both of these extensions are open source (see links) and are implemented using the API.  

We have been testing the Git extension for several months both internally and externally via our [Insiders build](http://code.visualstudio.com/insiders), the TFVC extension is also well tested.  

In short the API is mature enough and complete enough for others to build on.

## Next Steps & Roll-out
Today the API is a 'preview' API that can only be used with the Insiders build.  SCM Providers also cannot be published to the marketplace.  But that is all about to change - we plan to take the following steps a part of our next update in early April.

* The full API will move from 'preview' to 'supported'
* This will enable all versions of VS Code i.e. Stable as well as Insiders
* We will allow providers to be uploaded ot the marketplace
* We will show users how to discover other providers and switch between them

Exciting times!





