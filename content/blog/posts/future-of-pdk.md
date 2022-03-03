---
title: "The future of the Puppet Developer Kit (PDK)"
date: 2021-09-14
author: "Dave Armstrong"
github_repo: "" # Disable the edit commands
---

The Puppet Developer Kit was launched in 2017 to help our users develop high quality modules faster and over the years, it has seen regular development towards that goal.

It was designed to be a single install that would provide everything you needed to write, lint, test and publish a Puppet module — and for the most part, that's what it did.

## What worked
The PDK did exactly what it set out to do. It enabled users of Puppet and its ecosystem — regardless of experience level — to create Modules that were testable, deployable, and shareable. It provided functionality to keep those modules running against all supported Puppet versions, as well as the core Gemset to run all the features built into the template.

## What didn’t work
In order for all this to work, the PDK hinged on that single template which was maintained by the Puppet Developer Experience (PDE) team.

Since its launch, the PDK has come to support the creation of more than just modules and classes. With each successive addition, the template and the packaging system had to support more dependencies, and these dependencies needed to be monitored and updated in line with Puppet agent support and things like security fixes. This overhead meant the PDK couldn’t move forward quickly in supporting the wealth of content our users wanted. And every new feature made the template system that much more complex and awkward to customize for your own needs.

## The path forward
The DevX strategy is to build a new PDK while maintaining the existing PDK at version 2.x. What this means is that updates to the PDK 2.x will be limited to bug fixes and updates to support the latest Puppet gem.

We will be designing and building multiple tools to cover the functionality of the existing PDK:

- Content creation
- Linting / Validation
- Testing
- Packaging and sharing
- Runtime management
- Each tool will be released ASAP for early feedback and iteration. They will be designed to work independently of each other, giving you the choice to download and install the parts of the Kit that you need.

## Puppet Content Templates
You may already be aware of the DevX team's first part of this strategy: Puppet Content Templates (PCT).

PCT expands on the original PDK’s “new” functionality enabling Puppet, Puppet content creators, and our customers to create their own templates and share them with their teams. No longer do we have a single one-size-fits-all template. Instead we have many small and composable templates that allow you to mix & match to make your modules everything you want — and only what you want.

If you’re new to Puppet, PCT ships with the common templates:

- Module
- Class
- Type

This functionality was available in PDK, but with our new approach, we’ve been able to quickly build templates for other Puppet content:

- Control Repo
- Resource API Provider
- Bolt Projects
- Bolt Plans
- Bolt Tasks

{{% alert title="Note" color="primary" %}}
At the time of writing, we are in the process of shipping PCT 0.3.0 which adds the ability to package and install new templates. This makes it possible to share the templates with others on your team by just distributing a tarball.
{{% /alert %}}

In the near future we also plan to allow for the publication of templates to the Puppet Forge for sharing, download and installation. If you want all your modules to include GitHub actions for auto-publishing to the Forge when you tag a release, you'd just install that template. If you prefer GitLab or CircleCI instead, you'd choose the appropriate template. And if one doesn't exist that does what you need, then you could write it yourself and contribute it to the community.

{{% alert title="Note" color="primary" %}}
PCT is in active development and is pre-release; therefore it is not recommended for production use at this time.
{{% /alert %}}

To find out more on PCT, you can watch James Pogran’s coverage of it on Pulling the Strings LIVE.

## Technical Choices
To build these new tools, we have consciously chosen to move away from Ruby as a platform and are instead developing these CLIs in Go. This allows us to ship a compiled binary which is faster for you to run, and faster for us to build and test. This results in our team’s ability to iterate faster and ship new rich features more often. It also means that your experience of creating a new module happens before your finger has lifted from the enter key.

Ruby will always be present when testing and validating. Puppet and its ecosystem are built upon it. Our new tooling will include a system that will provide the PDK functionality of a Puppet Runtime sandbox, with you choosing which version of Puppet to install and run our tooling against.

The aim for the new tools is to make them loosely coupled to Puppet, while still providing a clear workflow that allows you to build great Puppet content. This means that you will not be forced to update when the pdk-templates are updated, or to include functionality in your code that you don’t want or need. We hope this approach will provide flexibility for different development choices and will help new users understand wider Puppet concepts without the sometimes intrusive guardrails provided by the current PDK.

Finally, we want the tools to be extensible. With PCT, you can install new templates. With our validation tool, we want content creators to be able to plug in new validators, and to write validation tools for testing their content. And with our Packaging and Sharing tool, we want you to be able to share content to multiple locations, including the Forge.

With this flexible plugin architecture, this could mean eventually supporting Onceover on your control repository before upgrading to a new version of Puppet, or being able to fire up Corey's Puppet Debugger on a previous version of Puppet to figure out the intended behavior of that old module you've inherited.

## Feedback
Feedback is so important to us at this early stage of design and development. The DevX team would love to engage with our community about our roadmap and we hope that you can see yourself using these tools in the future. Your feedback can have a real impact on what we build.

To get in touch, you can find us on the #office-hours channel within Puppet Community Slack every Monday, alternating weekly between about 1pm and 5pm GMT.

Out of those hours, please get involved in our discussions at Discussions · puppetlabs/pdkgo · GitHub.