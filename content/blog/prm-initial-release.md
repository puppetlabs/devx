---
title: "Puppet Runtime Manager 0.1.0 Release 🚀"
date: 2022-01-31
author: "Michael T. Lombardi"
github_repo: "" # Disable the edit commands
---

We are proud to announce the first release for the new tool for executing arbitrary commands against your code in a Puppet runtime: The **Puppet Runtime Manager (PRM)**.

The **Puppet Runtime Manager** abstracts away the Puppet Ruby development environment to enable you to execute against and validate content for any Puppet Product that you might author!

## Installing PRM 💾

To get started, you can either download the release from the [PRM repo](https://github.com/puppetlabs/prm/releases/tag/0.1.0) or use our installer scripts:

{{< tabpane langEqualsHeader=false >}}
{{< tab header="Unix Systems" lang="Bash" >}}
curl -L https://pup.pt/prm/install.sh | sh
{{< /tab >}}

{{< tab header="Windows Systems" lang="Powershell" >}}
iex "&{ $(irm https://pup.pt/prm/install.ps1); Install-Prm }"
{{< /tab >}}
{{< /tabpane >}}

This will install the latest release of PRM to `~/.puppetlabs/prm`.

{{% alert title="PRM is Experimental!" color="warning" %}}
PRM is currently in an EXPERIMENTAL phase and feedback is encouraged via [our Discussions page on GitHub](https://github.com/puppetlabs/pdkgo/discussions).
{{% /alert %}}

### Telemetry & PRM

By default, PRM collects some telemetry during each run.
This information is non-identifying and does not include any personal or organizational details.

For more information, see [our documentation on Telemetry]({{< ref "/prm/concepts/telemetry.md" >}}).

If you'd like to install PRM _without_ telemetry, you can use these scripts:

{{< tabpane langEqualsHeader=false >}}
{{< tab header="Notel on Unix Systems" lang="Bash" >}}
curl -L https://pup.pt/prm/install.sh | sh -s -- --no-telemetry
{{< /tab >}}

{{< tab header="Notel on Windows Systems" lang="Powershell" >}}
iex "&{ $(irm https://pup.pt/prm/install.ps1); Install-Prm -NoTelemetry}"
{{< /tab >}}
{{< /tabpane >}}

### Prerequisites & Support

In this initial release, PRM only supports one backend for running tools: Docker.
You will need to be able to use Docker locally to pull, build, and run container images for this release (though PRM handles all those steps for you).

Right now, only Linux containers in Docker are supported, but the Docker backend is functional on Windows, Linux, and MacOS systems.

A future release will add a local execution backend, enabling you to just use your locally installed Puppet Agent for the runtime.

If there are other backends you'd like to see supported, please [raise a discussion with us!](https://github.com/puppetlabs/pdkgo/discussions)

## Docs in the Terminal 📃

PRM has a pair of robust help systems built in for reviewing reference, concept, and narrative documentation.

To see the help for any command or subcommand:

{{< tabpane langEqualsHeader=false >}}
{{< tab header="Use the help subcommand" lang="Bash" >}}
prm help      # Displays the help for PRM itself
prm help exec # Displays the help for the prm exec command
{{< /tab >}}

{{< tab header="Use the help flag" lang="Bash" >}}
prm --help      # Displays the help for PRM itself
prm exec --help # Displays the help for the prm exec command
{{< /tab >}}
{{< /tabpane >}}

To read the concept and narrative documentation locally instead of [online]({{< ref "/prm/_index.md" >}}):

{{< tabpane langEqualsHeader=false >}}
{{< tab header="List Available Topics" lang="Bash" >}}
prm explain --list
prm explain # Identical to prm explain --list
{{< /tab >}}

{{< tab header="Filter Available Topics" lang="Bash" >}}
prm explain --category concept             # Only list concept docs
prm explain --tag tools                    # Only list docs about tools
prm explain --category concept --tag tools # Multi-filter
{{< /tab >}}

{{< tab header="Display a Topic" lang="Bash" >}}
prm --help      # Displays the help for PRM itself
prm exec --help # Displays the help for the prm exec command
{{< /tab >}}
{{< /tabpane >}}

For more detailed information on the `explain` subsystem and documentation, see [our narrative document on it]({{< ref "/prm/usage/explain-subsystem.md" >}}).

## Run Tools Against Your Content 🏃🏻‍♀️

**PRM** can run tools against any type of a Puppet Product project.
You can run r10k against Puppet [control repos](https://github.com/puppetlabs/control-repo), validate EPP files in Puppet [modules](https://puppet.com/docs/puppet/7/modules_fundamentals.html), rubocop Bolt [projects](https://puppet.com/docs/bolt/latest/projects.html), and more!

We've shipped with a subset of tools you can use:

- EPP
- Heira EYAML
- metadata-json-lint
- onceover
- puppet-lint
- puppet-strings
- puppet-syntax
- r10k
- ra10ke
- rubocop
- rspec-puppet

These tools are currently maintained by the DevX team in the [fantastic-adventure repository](https://github.com/puppetlabs/fantastic-adventure).
If you'd like to learn more about how they're constructed or how to develop your own, check out our [_Anatomy of a Tool_ guide]({{< ref "/prm/concepts/tool-anatomy" >}}).

Since PRM tools are external to the PRM code base, Puppet Product teams, Partners and the wider OSS Community can publish their own tool packages without input or effort from the DevX team.
This enables a single tool to support many products.

### Example: Generate Reference Docs for puppetlabs-acl

{{% alert color="info" %}}
This example is a shortened version of our [Quick Start Guide]({{< ref "/prm/quick-start.md" >}}), which includes a more detailed walkthrough and includes configuring PRM beyond the defaults.
{{% /alert %}}

Before we generate the reference documents for a Puppet module, we might want to ensure that we have full coverage for our module.

Assuming we've already cloned a copy of [https://github.com/puppetlabs/puppetlabs-acl] locally to `~/code/modules/puppetlabs-acl`, we can run the following command:

```text
prm exec puppetlabs/puppet-strings --codedir ~/code/modules/puppetlabs-acl
```

```text
4:54PM INF Creating new image. Please wait...
4:54PM INF Code path: ~/code/modules/puppetlabs-acl
4:54PM INF Cache path: ~/.pdk/prm/cache
4:54PM INF Additional Args: []
Files:                    5
Modules:                  2 (    0 undocumented)
Classes:                  4 (    0 undocumented)
Constants:               25 (    0 undocumented)
Attributes:               9 (    0 undocumented)
Methods:                 49 (    0 undocumented)
Puppet Data Types:        0 (    0 undocumented)
Puppet Data Type Aliases:     0 (    0 undocumented)
Puppet Classes:           0 (    0 undocumented)
Puppet Types:             1 (    0 undocumented)
Puppet Providers:         1 (    0 undocumented)
Puppet Functions:         0 (    0 undocumented)
Puppet Defined Types:     0 (    0 undocumented)
Puppet Plans:             0 (    0 undocumented)
Puppet Tasks:             0 (    0 undocumented)
 100.00% documented
4:54PM INF Tool puppetlabs/puppet-strings executed successfully
```

Behind the scenes, PRM built a docker container on the fly from the tool definition for `puppet-strings` and then executed it against the specified directory.
The output we see without the PRM log prefix is what the docker container's stdout returned;
in this case, the documentation results for the ACL module.

We can also pass arbitrary arguments to the tool;
to generate the reference documentation, we need to specify that we want to generate the document and set the format to markdown.
This will create (or update if it exists) the `REFERENCE.md` file in the module's folder.

```sh
prm exec puppetlabs/puppet-strings --codedir ~/code/modules/puppetlabs-acl --toolArgs "strings generate --format markdown"
```

```text
4:54PM INF Creating new image. Please wait...
4:54PM INF Code path: ~/code/modules/puppetlabs-acl
4:54PM INF Cache path: ~/.pdk/prm/cache
4:54PM INF Additional Args: [strings generate --format markdown]
Files:                    5
Modules:                  2 (    0 undocumented)
Classes:                  4 (    0 undocumented)
Constants:               25 (    0 undocumented)
Attributes:               9 (    0 undocumented)
Methods:                 49 (    0 undocumented)
Puppet Data Types:        0 (    0 undocumented)
Puppet Data Type Aliases:     0 (    0 undocumented)
Puppet Classes:           0 (    0 undocumented)
Puppet Types:             1 (    0 undocumented)
Puppet Providers:         1 (    0 undocumented)
Puppet Functions:         0 (    0 undocumented)
Puppet Defined Types:     0 (    0 undocumented)
Puppet Plans:             0 (    0 undocumented)
Puppet Tasks:             0 (    0 undocumented)
 100.00% documented
4:54PM INF Tool puppetlabs/puppet-strings executed successfully
```

While the output of Puppet Strings itself isn't any different, we can check the timestamp on the `REFERENCE.md` file and verify that it was just updated (or created if it didn't already exist).

So!
That's how you run a PRM tool against a folder and can send the tool specific arguments, too!

## Coming Soon❗

As mentioned earlier, this is the _initial_ release for PRM;
we're not done!

Our next planned release, `0.2.0`, will add the `validate` functionality you may remember from the PDK.
In short, this will enable you to run multiple tools against your code in parallel and report back to you both pass/fail and detailed failure notes (if any).
We are targeting this release for late March/early April.

After that, our `0.3.0` release will add local execution as a backend, removing the dependency on Docker so long as you have the Puppet Agent installed locally.

In the meantime, we will be improving and adding tools; if you add any yourself, we'd love to hear about it and highlight them in future blog posts!

Til next time!

~ The DevX Team